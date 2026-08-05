# Gradio UI Architecture

## Overview

The Counterexample Commons UI is built with Gradio and provides a tabbed
research dashboard for exact mathematical validation and controlled AI
experimentation.

## Shared Core vs UI

```
counterexample_commons/        (Python package — shared core)
├── validators/                (exact arithmetic validators)
├── providers/                 (normalized AI provider interface)
├── config.py                  (AppMode enum, capability matrix)
└── claims.py                  (claim registry data model)

app/                           (Gradio UI layer)
├── main.py                    (build_app entry point)
├── tabs/                      (one module per tab)
└── public_demo.py             (public-demo-only builder)
```

## Tabs

| Tab | Public Demo | Private Research | Function |
|-----|-------------|------------------|----------|
| Overview | ✅ | ✅ | Problem statement, mathematical context |
| Exact Baselines | ✅ | ✅ | Line and grid edge-count validators |
| Configuration Explorer | ✅ | ✅ | Custom point-set exact validation |
| AI Candidate Lab | ❌ | ✅ | Single-provider candidate generation |
| Provider Comparison | ❌ | ✅ | Multi-provider same-task comparison |
| Claim Registry | Read-only | Full | Claim status tracking |
| Reports & Export | Safe only | Full | Sanitized artifact download |
| Settings & Security | Display only | Configurable | Mode, providers, security state |

## Execution Modes

| Mode | Constant | Providers | Share | Auth |
|------|----------|-----------|-------|------|
| `local-private` | `AppMode.LOCAL_PRIVATE` | All configured | No (localhost) | Optional |
| `colab-public-demo` | `AppMode.COLAB_PUBLIC_DEMO` | None | Yes | None |
| `colab-private` | `AppMode.COLAB_PRIVATE` | Secrets-configured | Yes | Required |

## Intentionally Exposed API Endpoints

In public-demo mode, only these Gradio API-named endpoints are safe:

- `validate_line_configuration`
- `validate_grid_configuration`
- `validate_custom_configuration`

All provider-generation endpoints are unnamed/hidden in public-demo mode.

## Service Layer

The UI does not perform mathematical computation directly. All validation
calls go through the shared `counterexample_commons.validators` module,
which uses SymPy for exact rational arithmetic.
