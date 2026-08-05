# Contributing to BEAM-SSZ

Thank you for your interest in contributing to BEAM-SSZ!

## Development Setup

1. Fork the repository
2. Clone your fork
3. Run the installation script:
   ```bash
   bash scripts/install.sh
   ```

## Making Changes

1. Create a feature branch
2. Make your changes
3. Add tests for new functionality
4. Ensure all tests pass:
   ```bash
   python -m pytest tests/ -v
   ```
5. Update documentation if needed

## Code Standards

- Follow PEP 8 style guidelines
- Add docstrings to all public functions
- Include type hints where appropriate
- Maintain test coverage

## Testing

All new code must include tests:

```bash
# Run specific test file
python -m pytest tests/test_your_module.py -v

# Run with coverage
python -m pytest tests/ --cov=src/beam_ssz
```

## Documentation

Update relevant documentation in `docs/`:
- API changes → Update `19_api_reference.md`
- New features → Add to appropriate doc file
- Usage examples → Add to `examples/`

## Pull Request Process

1. Update the README.md with details of changes if applicable
2. Update documentation
3. Ensure all tests pass
4. Submit PR with clear description

## Questions?

Open an issue for discussion before major changes.

---

© 2025-2026 Carmen N. Wrede, Lino P. Casu
