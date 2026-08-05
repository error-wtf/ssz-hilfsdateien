# PSD Welch Estimation Report
Generated: {NOW}

## Method
- Estimator: Welch
- Window: Hann
- nperseg: {PSD_NPERSEG}
- Overlap: 50%
- Off-source offset: {OFFSOURCE_OFFSET_S} s before trigger
- Off-source duration: {OFFSOURCE_DUR_S} s

## Results
- PSD bins: {len(freqs_psd)}
- Frequency range: {freqs_psd[1]:.3f} – {freqs_psd[-1]:.1f} Hz
- PSD median [20–800 Hz]: {np.median(psd[band_m]):.3e} 1/Hz
- PSD min [20–800 Hz]:    {psd[band_m].min():.3e} 1/Hz
- PSD max [20–800 Hz]:    {psd[band_m].max():.3e} 1/Hz

## Anti-Circularity
- Posterior PSD used: NO
- Source: raw H1 strain off-source segment

## Status
**PASS** — PSD estimated from raw strain only
