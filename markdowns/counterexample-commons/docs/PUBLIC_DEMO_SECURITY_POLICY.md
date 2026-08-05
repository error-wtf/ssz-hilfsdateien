# Public Demo Security Policy

## Default public demo mode guarantees

- **No paid model APIs** are called in public demo mode
- **No secrets** are loaded or accessible
- **No Google Drive mount** is performed
- **No unrestricted filesystem access** is available
- **Only safe export** of user-generated session artifacts is permitted
- **No arbitrary filesystem download** through the UI

## Gradio share links

A Gradio share link is accessible to anyone who receives the link.
Public demo mode intentionally disables external AI API calls and secret use.

## Colab runtime

Google Colab runtimes are temporary. Users must save sanitized outputs before
ending the session. The Colab runtime's `localhost` refers to the Colab VM,
not the user's personal computer.

## What is exposed in public demo

- Problem overview and mathematical context
- Exact baseline computations (line, grid)
- Custom coordinate validation (exact arithmetic)
- Read-only claim registry
- Safe report export (sanitized)

## What is disabled in public demo

- AI Candidate Lab (all providers)
- Provider Comparison
- Secret/credential configuration
- Claim registry editing
- Arbitrary filesystem access
