# Contributing to SSZ-Schumann

Thank you for your interest in contributing to SSZ-Schumann! This document provides guidelines for contributing to the project.

## Table of Contents

1. [Code of Conduct](#code-of-conduct)
2. [How to Contribute](#how-to-contribute)
3. [Development Setup](#development-setup)
4. [Code Style](#code-style)
5. [Testing](#testing)
6. [Pull Request Process](#pull-request-process)
7. [License](#license)

---

## Code of Conduct

This project adheres to the principles of the **Anti-Capitalist Software License v1.4**. By contributing, you agree that your contributions will be licensed under the same terms.

### Our Values

- **Open Science**: Scientific knowledge should be freely accessible
- **Collaboration**: We welcome contributions from researchers worldwide
- **Ethical Use**: This software must not be used for military, surveillance, or exploitative purposes

---

## How to Contribute

### Reporting Bugs

1. Check if the bug has already been reported in [Issues](https://github.com/error-wtf/ssz-schumann/issues)
2. If not, create a new issue with:
   - Clear title describing the bug
   - Steps to reproduce
   - Expected vs actual behavior
   - Python version and OS
   - Relevant error messages

### Suggesting Features

1. Open an issue with the `[Feature Request]` prefix
2. Describe the feature and its use case
3. Explain how it relates to SSZ theory or Schumann resonance analysis

### Contributing Code

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/your-feature`)
3. Make your changes
4. Add tests for new functionality
5. Ensure all tests pass
6. Submit a pull request

---

## Development Setup

### Prerequisites

- Python 3.10+
- Git

### Installation

```bash
# Clone your fork
git clone https://github.com/YOUR_USERNAME/ssz-schumann.git
cd ssz-schumann

# Create virtual environment
python -m venv .venv
source .venv/bin/activate  # Linux/Mac
# or: .venv\Scripts\activate  # Windows

# Install dependencies
pip install -r requirements.txt

# Install package in development mode
pip install -e .
```

### Download Test Data

```bash
# Fetch sample data for testing
python scripts/fetch_data.py --all
```

---

## Code Style

### Python Style

- Follow [PEP 8](https://pep8.org/) guidelines
- Use meaningful variable names
- Maximum line length: 100 characters
- Use type hints where appropriate

### Documentation

- All functions must have docstrings (NumPy style)
- Include parameter types and return values
- Add examples for complex functions

### Example

```python
def compute_delta_seg(frequencies: np.ndarray, f_ref: float) -> np.ndarray:
    """
    Compute SSZ segmentation parameter from frequency shifts.
    
    Parameters
    ----------
    frequencies : np.ndarray
        Measured Schumann resonance frequencies [Hz]
    f_ref : float
        Reference frequency [Hz]
        
    Returns
    -------
    np.ndarray
        Segmentation parameter delta_seg (dimensionless)
        
    Examples
    --------
    >>> freqs = np.array([7.83, 14.1, 20.3])
    >>> delta = compute_delta_seg(freqs, 7.83)
    """
    return (f_ref - frequencies) / frequencies
```

---

## Testing

### Running Tests

```bash
# Run all tests
pytest tests/ -v

# Run specific test file
pytest tests/test_models.py -v

# Run with coverage
pytest tests/ --cov=ssz_schumann
```

### Writing Tests

- Place tests in the `tests/` directory
- Name test files `test_*.py`
- Name test functions `test_*`
- Include both positive and edge case tests

---

## Pull Request Process

### Before Submitting

1. ✅ All tests pass (`pytest tests/ -v`)
2. ✅ Code follows style guidelines
3. ✅ New functions have docstrings
4. ✅ New features have tests
5. ✅ Documentation is updated if needed

### PR Template

```markdown
## Description
Brief description of changes

## Type of Change
- [ ] Bug fix
- [ ] New feature
- [ ] Documentation update
- [ ] Performance improvement

## Testing
- [ ] All existing tests pass
- [ ] New tests added for new functionality

## Related Issues
Closes #XX (if applicable)
```

---

## Areas for Contribution

### High Priority

- [ ] Additional Schumann data sources (other ELF stations)
- [ ] Improved space weather correlation analysis
- [ ] Real-time data streaming support
- [ ] Multi-station coherence analysis

### Medium Priority

- [ ] Extended documentation and tutorials
- [ ] More comprehensive test coverage
- [ ] Visualization improvements
- [ ] Performance optimizations

### Research Contributions

- [ ] Alternative SSZ signatures in ELF data
- [ ] Long-term trend analysis
- [ ] Solar cycle correlation studies
- [ ] Ionospheric modeling improvements

---

## Data Sources

If you have access to additional Schumann resonance data, we welcome contributions! Please ensure:

1. Data is properly licensed for scientific use
2. Data format is documented
3. A loader module is provided in `ssz_schumann/data_io/`

---

## Contact

- **Email**: [mail@error.wtf](mailto:mail@error.wtf)
- **GitHub**: [github.com/error-wtf](https://github.com/error-wtf)
- **Issues**: [github.com/error-wtf/ssz-schumann/issues](https://github.com/error-wtf/ssz-schumann/issues)

---

## License

By contributing to SSZ-Schumann, you agree that your contributions will be licensed under the **Anti-Capitalist Software License v1.4**.

See [LICENSE](LICENSE) for the full license text.

---

© 2025 Carmen Wrede & Lino Casu

**Thank you for contributing to SSZ-Schumann!**
