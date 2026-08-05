# Contributing to G79 Segmented Spacetime Tests

Thank you for your interest in this project! 

## 🎯 Project Scope

This repository contains the **complete validation suite** for the paper:

**"Segmented Spacetime and the Origin of Molecular Zones in Expanding Nebulae"**

Current status: **Publication-ready** (Section 5.6 complete, 100% tests passing)

---

## 📚 How to Contribute

### 1. Reporting Issues

If you find bugs or have suggestions:

- Check existing [Issues](https://github.com/error-wtf/g79-cygnus-tests/issues)
- Open a new issue with:
  - Clear description
  - Steps to reproduce
  - Expected vs actual behavior
  - Python version & OS

### 2. Suggesting Features

We welcome:
- ✅ Additional test cases
- ✅ Alternative analysis methods
- ✅ Data processing improvements
- ✅ Documentation enhancements
- ✅ Visualization tools

### 3. Code Contributions

#### Setup Development Environment

```bash
# Fork and clone
git clone https://github.com/YOUR_USERNAME/g79-cygnus-tests.git
cd g79-cygnus-tests

# Create branch
git checkout -b feature/your-feature-name

# Install dependencies
pip install -r requirements.txt

# Run tests to verify setup
python RUN_ALL_TESTS_COMPLETE.py
```

#### Code Style

- Follow PEP 8
- Use meaningful variable names
- Add docstrings to functions
- Include comments for complex physics
- UTF-8 encoding for all files

#### Testing

**All contributions must pass existing tests:**

```bash
python RUN_ALL_TESTS_COMPLETE.py
# Must show: 14/14 tests passing
```

Add new tests for new features in `scripts/`.

#### Commit Messages

Use conventional commits:

```
feat: Add new velocity analysis method
fix: Correct temperature calculation in model
docs: Update README with new results
test: Add validation for hot ring prediction
```

### 4. Pull Requests

1. Ensure all tests pass (100% success rate)
2. Update documentation if needed
3. Add your changes to CHANGELOG.md
4. Submit PR with clear description

**PR Template:**

```markdown
## Description
Brief description of changes

## Type of Change
- [ ] Bug fix
- [ ] New feature
- [ ] Documentation
- [ ] Test improvement

## Testing
- [ ] All existing tests pass
- [ ] New tests added (if applicable)
- [ ] Manual testing completed

## Checklist
- [ ] Code follows project style
- [ ] Documentation updated
- [ ] CHANGELOG.md updated
```

---

## 🔬 Scientific Contributions

### Physics & Theory

If proposing new physics interpretations:

1. Provide mathematical formulation
2. Compare with observations
3. Cite relevant literature
4. Add validation test

### Data Analysis

For new analysis methods:

1. Document methodology
2. Validate against known results
3. Provide example output
4. Compare with paper predictions

### Predictions

For testable predictions:

1. Derive from segmented spacetime framework
2. Specify observable quantities
3. Suggest observational tests
4. Add to predictions list

---

## 📖 Documentation

Good documentation is crucial! Help us by:

- Clarifying existing docs
- Adding usage examples
- Writing tutorials
- Improving code comments
- Translating to other languages

---

## 🚫 What We Don't Accept

- ❌ Changes conflicting with paper physics
- ❌ Breaking existing tests
- ❌ Proprietary dependencies
- ❌ Code without tests
- ❌ Uncommented complex algorithms

---

## 🎓 Academic Use

### Citation

If you use this work in research:

```bibtex
@article{wrede2025ssz,
  title={Segmented Spacetime and the Origin of Molecular Zones 
         in Expanding Nebulae},
  author={Wrede, Carmen N. and Casu, Lino P. and Bingsi},
  journal={Astronomy \& Astrophysics (submitted)},
  year={2025},
  note={Code: github.com/error-wtf/g79-cygnus-tests}
}
```

### Collaboration

For scientific collaborations:
- Contact: (see AUTHORS.md)
- Discuss: Open an issue first
- Agree on authorship before major work

---

## 📜 License

All contributions fall under:

**ANTI-CAPITALIST SOFTWARE LICENSE (v 1.4)**

By contributing, you agree:
- ✓ Code is free for research/education
- ✗ No commercial use
- ✗ No military/surveillance use

See [LICENSE.md](LICENSE.md) for details.

---

## 🙏 Recognition

Contributors will be:
- Listed in CONTRIBUTORS.md
- Acknowledged in paper (if significant)
- Thanked in release notes

---

## 💬 Communication

- **Issues:** Bug reports, feature requests
- **Discussions:** General questions, ideas
- **Email:** For sensitive/private matters

---

## 🎯 Priority Areas

Currently seeking contributions in:

1. **Testing**
   - Additional validation cases
   - Edge case coverage
   - Performance benchmarks

2. **Documentation**
   - Usage tutorials
   - Theory explanations
   - API documentation

3. **Data Processing**
   - FITS handling improvements
   - Catalog parsers
   - Visualization tools

4. **Analysis**
   - Alternative fitting methods
   - Uncertainty quantification
   - Comparison tools

---

## ✅ Getting Started Checklist

New contributors should:

- [ ] Read README.md completely
- [ ] Review PAPER_SECTION_5.6_FINAL.md
- [ ] Run test suite successfully
- [ ] Understand segmented spacetime basics
- [ ] Check existing issues/PRs
- [ ] Join discussions

---

## 📊 Contribution Statistics

We value:
- Quality over quantity
- Scientific rigor
- Clear documentation
- Reproducible results

**Thank you for contributing to advancing segmented spacetime physics!** 🚀

---

**Last Updated:** 2025-11-06  
**Status:** Publication preparation phase  
**Contact:** See AUTHORS.md
