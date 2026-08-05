# SSZ <-> GR Bridge Report

## Correlation Overview
- omega=0.10, m=2
  - corr(normalized_gain, S) = 0.9199879764259129
  - corr(segment_proxy, S) = -0.36066819772142755
  - mean normalized gain = -4.381927342236211
  - std normalized gain = 5.890111887197748

- omega=0.20, m=3
  - corr(normalized_gain, S) = 0.9072142345350515
  - corr(segment_proxy, S) = -0.36066819772142755
  - mean normalized gain = -3.193869576911604
  - std normalized gain = 4.358144731137711

- omega=0.30, m=4
  - corr(normalized_gain, S) = 0.8997101106983385
  - corr(segment_proxy, S) = -0.36066819772142755
  - mean normalized gain = -2.5145838016660673
  - std normalized gain = 3.461915146349182

## Top Stabilizing Configurations
- lambda_A=0.05, lambda_phi=0.00, K=64, Omega0=0.20
  - S = -10.524147235276015
  - avg normalized gain = -25.031801114331817
  - segment proxy = 0.0

- lambda_A=0.05, lambda_phi=0.01, K=64, Omega0=0.20
  - S = -10.524147235276015
  - avg normalized gain = -25.031801114331817
  - segment proxy = 0.64

- lambda_A=0.05, lambda_phi=0.02, K=64, Omega0=0.20
  - S = -10.524147235276015
  - avg normalized gain = -25.031801114331817
  - segment proxy = 1.28

## Top Destabilizing Configurations
- lambda_A=0.00, lambda_phi=0.05, K=64, Omega0=0.40
  - S = 0.0
  - avg normalized gain = 0.0
  - segment proxy = 3.2000000000000006

- lambda_A=0.00, lambda_phi=0.05, K=64, Omega0=0.30
  - S = 0.0
  - avg normalized gain = 0.0
  - segment proxy = 3.2000000000000006

- lambda_A=0.00, lambda_phi=0.05, K=64, Omega0=0.20
  - S = 0.0
  - avg normalized gain = 0.0
  - segment proxy = 3.2000000000000006
