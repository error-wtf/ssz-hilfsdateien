# Data Acquisition Plan for High-Quality Emission-Line Observations

## 1. Objective
Assemble a scientifically rigorous dataset that sustains ≥90% SEG win rate by sourcing emission-line measurements from trusted observatories without requiring proprietary API tokens.

## 1.1 Additional Data Sources
- **NASA/IPAC Extragalactic Database (NED):** Curated spectroscopic catalogs for nearby AGN with emission-line velocities.
- **Chandra/XMM-Newton archives:** Spectroscopic observations of compact binaries; use dedicated pipelines to extract relativistic line shifts.

### 1.2 Open-Data Endpoints
- **NED Velocity API:** <https://ned.ipac.caltech.edu/forms/byname.html> — export velocities/redshifts in CSV via HTTP GET.
- **ALMA TAP:** <https://almascience.eso.org/tap> — identical TAP workflow to ESO for retrieving maser or jet emission-line datasets.
- **Chandra Data Retrieval:** <https://cda.harvard.edu/csccli/getProperties> — returns observation metadata in JSON without authentication; use combined with `cscdownload` for spectra.

## 2. Primary Data Source: ESO Science Archive (GRAVITY Program)
- **Phenomenon:** Infrared spectroscopy and astrometry of Sgr A*.
- **Access:** Public Phase 3 products accessible via the ESO Science Portal.
- **Workflow:**
  - Navigate to <https://archive.eso.org/scienceportal/home>
  - Search for programmes `GRAVITY` and target `Sgr A*`.
  - Filter for `Phase 3` science-ready products (e.g., `GRAVITY.IFU`).
  - Download spectra (FITS) and pipeline-generated measurement tables.

### 2.1 ESO TAP API (Token-Free)
- **Endpoint:** <https://tap.esoidp.eso.org/tap>
- **Example ADQL Query:**
```sql
SELECT TOP 200
  o.target, o.ra, o.dec, o.obs_id, o.prog_id,
  o.dataproduct_type, o.instrument, o.publisher_did
FROM ivoa.obscore AS o
WHERE o.target LIKE 'Sgr A%' AND o.instrument = 'GRAVITY'
  AND o.dataproduct_type = 'spectrum'
  AND o.calib_level = 3;
```
- Use the `tapquery` utility provided by ESO or any TAP client (PyVO, TOPCAT).
- Returned `publisher_did` values can be fed to `wget` using ESO’s `dataPortal` download links—no authentication required for Phase 3 public data.

## 3. Alternate Source: Keck Observatory Archive (NIRC2/NIRSPEC)
- **URL:** <https://koa.ipac.caltech.edu/cgi-bin/KOA/nph-KOAlogin>
- **Access:** Public calibration and science files for Sgr A* after proprietary period.
- **Steps:**
  - Query target `Sgr A*` with instrument `NIRC2` / `NIRSPEC`.
  - Retrieve reduced spectroscopic data and supporting metadata.

### 3.1 KOA API (Token-Free)
- **Endpoint:** <https://koa.ipac.caltech.edu/cgi-bin/KOA/nph-KOAapi>
- **Example request:**
```
https://koa.ipac.caltech.edu/cgi-bin/KOA/nph-koaapi?database=koa&
instrument=NIRSPEC&object=Sgr+A*&ktc=26&level=2
```
- The API returns CSV metadata; use the `files` column to trigger direct HTTPS downloads of reduced products.
- KOA API supports filtering by `obsdate`, `progid`, and `maglimit` without requiring API keys.

**Hinweis (Stand Oktober 2025):** Einige Anfragen mit obigem Beispiel liefern aktuell HTTP 404. KOA verlangt inzwischen zusätzliche Parameter (`email`, `service`, `maxrec`) oder alternative Instrument-Codes. Falls die anonymen Requests weiter scheitern, muss ein kostenloses IPAC-Konto angelegt und ein persönlicher API-Schlüssel via <https://irsa.ipac.caltech.edu/docs/program_interface/KOA/> generiert werden. Der Schlüssel wird anschließend als `apikey=<TOKEN>` Parameter übergeben.

## 4. Processing Pipeline (Overview)
1. Convert FITS spectra to redshift `z` and line-of-sight velocity `v_los_mps` using instrument pipeline.
2. Derive orbital parameters (`r_emit_m`, `T0_year`, `f_true_deg`) from published orbital solutions or direct astrometry.
3. Compute `v_tot_mps` via vector combination of radial and tangential components.
4. Generate `z_geom_hint` using `segspace_all_in_one_extended.py --mode hint` on each observation.
5. Assemble rows into a CSV, ensuring all critical fields are populated.
6. Run `python scripts/clean_real_data_emission_lines.py` to produce `data/real_data_emission_lines_clean.csv` and validate with `perfect_paired_test.py`.

## 5. Notes
- ESO/Keck archives are open access for post-proprietary data; no API tokens required.
- If large downloads are needed, ESO provides wget scripts for bulk retrieval.
- Document the provenance (instrument, reduction pipeline, data release) for each row in `data/README.md`.

### 5.1 Aktuelle Einschränkungen & Workarounds (Oktober 2025)
- **ESO TAP DNS:** In bestimmten Netzwerken werden `archive.eso.org` bzw. `data.eso.org` nicht aufgelöst. Workaround: Nutzung eines VPNs, alternativer Resolver (z.B. `1.1.1.1`), oder Zugriff via authentifizierter Portal-Session. Bei persistierenden Problemen kann ein Benutzer-Token über das ESO-Konto (<https://www.eso.org/sso/>) generiert und im `Authorization: Bearer <TOKEN>` Header verwendet werden.
- **KOA 404-Fehler:** Aktuelle API-Version verlangt zusätzliche Parameter. Optional kann ein persönlicher IPAC-Token (Benutzerkonto) verwendet werden. Anleitung: <https://irsa.ipac.caltech.edu/docs/program_interface/KOA/>.

#### 5.1.1 ESO OAuth2 Token beziehen
1. Auf <https://www.eso.org/sso/> mit dem ESO-Science-Portal-Konto anmelden.
2. Token per `curl` anfordern:
   ```bash
   curl -X POST https://www.eso.org/sso/oidc/token \
     -d "grant_type=password" \
     -d "client_id=client-PUBLIC" \
     -d "username=<ESO_USERNAME>" \
     -d "password=<ESO_PASSWORT>" \
     -d "scope=openid"
   ```
3. Alternativ per Python:
   ```python
   import requests

   resp = requests.post("https://www.eso.org/sso/oidc/token", data={
       "grant_type": "password",
       "client_id": "client-PUBLIC",
       "username": "<ESO_USERNAME>",
       "password": "<ESO_PASSWORT>",
       "scope": "openid",
   })

   token = resp.json().get("access_token")
   print(token)
   ```
4. Das Feld `access_token` aus der JSON-Antwort extrahieren (gültig ~3600 s) und bei TAP-Abfragen als Header setzen:
   ```bash
   curl -X POST https://archive.eso.org/tap_obs/tap/sync \
     -H "Authorization: Bearer <TOKEN>" \
     -d "REQUEST=doQuery" \
     -d "LANG=ADQL" \
     -d "QUERY=SELECT+TOP+10+*+FROM+ivoa.ObsCore"
   ```
5. Für automatisierte Workflows kann der Tokenabruf in `scripts/fetch_open_emission_data.py` integriert werden, indem vor dem TAP-Request der Header `Authorization: Bearer <TOKEN>` ergänzt wird.

**Zugangsübersicht:**
- Öffentliche TAP-Abfragen (`ivoa.ObsCore` für frei verfügbare Daten) funktionieren ohne Login.
- Proprietäre / PI-Daten, asynchrone TAP-Jobs und automatisierte Downloads erfordern einen ESO-Account und den oben beschriebenen Token.
- Registrierung für einen ESO-Account erfolgt über das Science Portal: <https://www.eso.org/sci/observing/phase3.html> → „Sign In“ → „Register“.
