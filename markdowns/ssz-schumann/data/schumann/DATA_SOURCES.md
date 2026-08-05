# Schumann Resonance Data Sources

## 1. Sierra Nevada ELF Station (Zenodo)

**DOI:** 10.5281/zenodo.6348930
**URL:** https://zenodo.org/records/6348930
**Period:** March 2013 - February 2017
**Size:** 26.5 GB (raw data)
**Resolution:** ~1 hour

### Download Command:
```bash
# Download full dataset (26.5 GB)
wget https://zenodo.org/records/6348930/files/2013_2017.zip

# Or use the fetch script:
python scripts/fetch_zenodo_schumann.py --year 2016
```

### Data Format:
- Raw time-domain ELF measurements
- Two sensors: NS and EW orientation
- Requires processing to extract f1, f2, f3

### Reference:
Salinas, A. et al. (2022). Schumann resonance data processing programs 
and four-year measurements from Sierra Nevada ELF station. 
Computers & Geosciences, 165, 105148.

---

## 2. HeartMath GCI (Live Data)

**URL:** https://www.heartmath.org/gci/gcms/live-data/
**Stations:** 6 worldwide (California, Saudi Arabia, Lithuania, Canada, New Zealand, South Africa)
**Data:** Live spectrograms, not downloadable as CSV

---

## 3. GeoCenter.info (Live Monitor)

**URL:** https://geocenter.info/en/monitoring/schumann
**Data:** Live monitoring, limited historical data

---

## Recommended Approach

For SSZ analysis, use:
1. **Synthetic data** for validation (already implemented)
2. **Sierra Nevada data** for real-world testing (requires download)
3. **Space weather proxies** (F10.7, Kp) for correlation analysis

The synthetic data generator creates realistic Schumann frequencies with
configurable SSZ signals, which is sufficient for method validation.

---

Generated: 2025-12-08T10:21:57.121074
