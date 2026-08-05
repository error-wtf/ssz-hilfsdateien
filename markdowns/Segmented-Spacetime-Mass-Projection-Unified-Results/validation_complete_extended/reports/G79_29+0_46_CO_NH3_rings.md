# G79.29+0.46 – CO/NH₃ Ringe (SSZ SegWave Daten)

ASCII-Vorschau (gekürzt):
```
+----+----------+-----------+-----------+-----------+---------------+------------------------------+--------------------------------------------------------------+
|rin |radius_pc |T_dust_K   |n_H2_cm3   |v_obs_kms  |v_obs_err_kms  |tracers                      |notes                                                         |
+----+----------+-----------+-----------+-----------+---------------+------------------------------+--------------------------------------------------------------+
|1   |0.30      |78         |2.0e4      |14.5       |0.3            |CO(3-2), NH3(2,2)            |inner shocked rim near CO clump; protected cold clumps survive|
|2   |0.45      |65         |1.5e4      |12.0       |0.5            |CO(3-2), NH3(1,1)            |transition zone; decreasing velocity from shock               |
|3   |0.60      |55         |1.2e4      |8.0        |0.5            |CO(2-1)                      |cooling molecular shell; partial UV                           |
|4   |0.75      |45         |1.0e4      |5.0        |0.5            |CO(2-1), [CII]158um          |PDR overlap; mixed conditions                                 |
|5   |0.90      |38         |8.0e3      |3.0        |0.4            |CO(1-0)                      |outer molecular arc                                           |
|6   |1.10      |32         |6.0e3      |2.0        |0.3            |CO(1-0), HI                  |blend with diffuse ISM                                        |
|7   |1.30      |28         |4.5e3      |1.5        |0.3            |HI                           |diffuse interface                                             |
|8   |1.50      |25         |3.5e3      |1.3        |0.3            |HI                           |outer interface                                               |
|9   |1.70      |22         |3.0e3      |1.1        |0.3            |HI                           |ambient                                                       |
|10  |1.90      |20         |2.5e3      |1.0        |0.3            |HI                           |ambient baseline                                              |
+----+----------+-----------+-----------+-----------+---------------+------------------------------+--------------------------------------------------------------+
```

**CSV (roh, maschinenlesbar):**
```csv
# G79.29+0.46 — ring-wise observational summary for SSZ segwave
# v_obs_kms from literature: inner shock ~14–15 km/s toward CO clump; FFTS resolution ~0.08 km/s
ring,radius_pc,T_dust_K,n_H2_cm3,v_obs_kms,v_obs_err_kms,tracers,notes
1,0.30,78,2.0e4,14.5,0.3,"CO(3-2), NH3(2,2)","inner shocked rim near CO clump; protected cold clumps survive"
2,0.45,65,1.5e4,12.0,0.5,"CO(3-2), NH3(1,1)","transition zone; decreasing velocity from shock"
3,0.60,55,1.2e4,8.0,0.5,"CO(2-1)","cooling molecular shell; partial UV"
4,0.75,45,1.0e4,5.0,0.5,"CO(2-1), [CII]158um","PDR overlap; mixed conditions"
5,0.90,38,8.0e3,3.0,0.4,"CO(1-0)","outer molecular arc"
6,1.10,32,6.0e3,2.0,0.3,"CO(1-0), HI","blend with diffuse ISM"
7,1.30,28,4.5e3,1.5,0.3,"HI","diffuse interface"
8,1.50,25,3.5e3,1.3,0.3,"HI","outer interface"
9,1.70,22,3.0e3,1.1,0.3,"HI","ambient"
10,1.90,20,2.5e3,1.0,0.3,"HI","ambient baseline"
```
