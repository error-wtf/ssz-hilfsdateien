# Contributing to SSZ Projection Suite

**Thank you for your interest in contributing!**

---

## 📋 Table of Contents

1. [Code of Conduct](#code-of-conduct)
2. [Getting Started](#getting-started)
3. [Development Setup](#development-setup)
4. [Making Changes](#making-changes)
5. [Testing](#testing)
6. [Documentation](#documentation)
7. [Submitting Changes](#submitting-changes)

---

## 📜 Code of Conduct

**Anti-Capitalist Software License v1.4**

This project is licensed under the ANTI-CAPITALIST SOFTWARE LICENSE v1.4. By contributing, you agree that your contributions will be licensed under the same license.

**Key Points:**
- Free for personal, educational, and non-commercial research use
- Prohibited for commercial use without explicit permission
- Must preserve license in all derivatives
- No warranty provided

---

## 🚀 Getting Started

### ⚠️ IMPORTANT: Repository Access

**You CANNOT push directly to this repository.**

This repository is **restricted to owners only** (Carmen Wrede, Lino Casu). All external contributions **must** go through:
1. **Fork** this repository to your account
2. **Make changes** in your fork
3. **Create Pull Request** from your fork

**Any attempt to `git push` to the main repository will fail with 403 Forbidden error.**

For details, see [REPOSITORY_SECURITY_PERMISSIONS.md](REPOSITORY_SECURITY_PERMISSIONS.md)

### Prerequisites

- Python 3.8 or higher
- Git
- Basic knowledge of physics/astrophysics (helpful but not required)
- GitHub account (for forking and PRs)

### Areas We Need Help

**High Priority:**
- 🐛 Bug fixes
- 📊 Data quality improvements
- 🧪 Additional test cases
- 📖 Documentation improvements (especially bilingual DE/EN)

**Medium Priority:**
- ✨ New features
- 🎨 Visualization improvements
- ⚡ Performance optimizations

**Low Priority:**
- 🌐 Web interface development
- 📱 Mobile/tablet compatibility

---

## 🛠️ Development Setup

### 1. Fork and Clone

```bash
# Fork on GitHub first, then:
git clone https://github.com/YOUR-USERNAME/Segmented-Spacetime-Mass-Projection-Unified-Results.git
cd Segmented-Spacetime-Mass-Projection-Unified-Results

# Add upstream
git remote add upstream https://github.com/error-wtf/Segmented-Spacetime-Mass-Projection-Unified-Results.git
```

### 2. Create Virtual Environment

```bash
# Windows
python -m venv .venv
.venv\Scripts\activate

# Linux/Mac
python3 -m venv .venv
source .venv/bin/activate
```

### 3. Install Dependencies

```bash
pip install -r requirements.txt

# For development
pip install pytest pytest-cov black flake8
```

### 4. Run Tests

```bash
# Quick check
python run_full_suite.py

# Or with pytest
pytest tests/ -v
```

---

## 📝 Making Changes

### Branch Naming

```bash
# Feature
git checkout -b feature/your-feature-name

# Bug fix
git checkout -b fix/issue-description

# Documentation
git checkout -b docs/what-you-document
```

### Coding Standards

**Python:**
- Follow PEP 8
- Use type hints where possible
- Add docstrings to all functions
- UTF-8 encoding for all files

```python
#!/usr/bin/env python3
# -*- coding: utf-8 -*-
"""
Module description

© 2025 Carmen Wrede & Lino Casu
Licensed under the ANTI-CAPITALIST SOFTWARE LICENSE v1.4
"""

def example_function(param: float) -> float:
    """
    Brief description.
    
    Args:
        param: Description of parameter
        
    Returns:
        Description of return value
    """
    return param * 2
```

**Markdown:**
- Use consistent heading levels
- Add language tags to code blocks
- Use relative links for internal references

### Commit Messages

**Format:**
```
Type: Brief description (50 chars max)

Longer explanation if needed (wrap at 72 chars).

- Bullet points for details
- Reference issues: #123
```

**Types:**
- `feat:` New feature
- `fix:` Bug fix
- `docs:` Documentation
- `test:` Tests
- `refactor:` Code refactoring
- `perf:` Performance improvement
- `chore:` Maintenance

**Examples:**
```bash
git commit -m "fix: Resolve UTF-8 encoding issue on Windows

- Add explicit UTF-8 encoding to subprocess calls
- Update documentation
- Fixes #42"

git commit -m "docs: Add bilingual glossary (EN/DE)

- German/English term mapping
- Symbol definitions
- Usage examples"
```

---

## 🧪 Testing

### Running Tests

```bash
# All tests
python run_full_suite.py

# Specific test file
python tests/test_ppn_exact.py

# With pytest
pytest tests/test_energy_conditions.py -v
```

### Writing Tests

**Test Structure:**
```python
def test_your_feature():
    """Test description"""
    # Arrange
    input_data = prepare_test_data()
    
    # Act
    result = your_function(input_data)
    
    # Assert
    assert result is not None
    assert result > 0
    
    # Physical interpretation
    print("\n" + "="*80)
    print("TEST: Your Feature")
    print("="*80)
    print(f"Result: {result:.6f}")
    print("\nPhysical Interpretation:")
    print("  • What this means physically")
    print("="*80)
```

### Test Coverage

```bash
# Check coverage
pytest --cov=. --cov-report=html tests/

# View report
open htmlcov/index.html
```

---

## 📖 Documentation

### What to Document

- **All new functions:** Docstrings with examples
- **All new scripts:** README with usage
- **All new features:** Update relevant markdown files
- **Bug fixes:** Update CHANGELOG.md

### Documentation Standards

**German/English:**
- Core scientific docs should be bilingual
- Add language switcher to bilingual docs:
  ```markdown
  **🌐 Languages:** [🇬🇧 English | 🇩🇪 Deutsch
  ```

**Structure:**
- Use clear headings
- Add table of contents for long docs
- Include examples
- Add cross-references

### Bilingual Documentation Synchronization ⚠️ IMPORTANT

**For EN/DE bilingual files, ALWAYS update both versions:**

```bash
# Example: When updating theory docs
# 1. Edit English version
vim docs/PHYSICS_FOUNDATIONS.md

# 2. Edit German version
vim docs/PHYSICS_FOUNDATIONS_DE.md

# 3. Keep structure identical
# - Same headings
# - Same examples  
# - Same formulas
# - Only language differs
```

**Checking bilingual coverage:**
```bash
# Run bilingual coverage check
python scripts/tools/analyze_bilingual_coverage.py

# Shows:
# - Missing translations
# - Outdated translations
# - Coverage percentage
```

**Current bilingual docs (must be kept in sync):**
- `PHYSICS_FOUNDATIONS.md` / `PHYSICS_FOUNDATIONS_DE.md`
- `MATHEMATICAL_FORMULAS.md` / `MATHEMATICAL_FORMULAS_DE.md`
- `CODE_IMPLEMENTATION_GUIDE.md` / `CODE_IMPLEMENTATION_GUIDE_DE.md`
- `EXAMPLES_AND_APPLICATIONS.md` / `EXAMPLES_AND_APPLICATIONS_DE.md`
- `THEORY_AND_CODE_INDEX.md` / `THEORY_AND_CODE_INDEX_DE.md`
- `DATA_IMPROVEMENT_ROADMAP.md` / `DATA_IMPROVEMENT_ROADMAP_EN.md`
- `DATA_IMPROVEMENT_STATUS_REPORT.md` / `DATA_IMPROVEMENT_STATUS_REPORT_EN.md`
- `TODO_DATA_INTEGRATION.md` / `TODO_DATA_INTEGRATION_EN.md`
- `TEST_SUITE_VERIFICATION.md` / `TEST_SUITE_VERIFICATION_EN.md`

**Translation Tips:**
- Use [Technical Glossary](docs/improvement/TERMINOLOGY_GLOSSARY.md) for consistent terminology
- Preserve all code blocks exactly
- Keep LaTeX formulas identical
- Maintain same formatting/structure

**Community Help Welcome:**
We appreciate help keeping translations synchronized! If you find outdated translations, please open an issue or PR.

---

## 🔄 Submitting Changes

### Before Submitting

**Checklist:**
- [ ] Tests pass (`python run_full_suite.py`)
- [ ] Code follows style guide
- [ ] Documentation updated
- [ ] Commit messages follow format
- [ ] Branch is up to date with upstream

```bash
# Update your branch
git fetch upstream
git rebase upstream/main
```

### Create Pull Request

1. Push to your fork:
   ```bash
   git push origin your-branch-name
   ```

2. Go to GitHub and create Pull Request

3. Fill out PR template:
   - **Title:** Clear, concise description
   - **Description:** What and why
   - **Testing:** How you tested
   - **Screenshots:** If relevant

4. Link related issues: `Fixes #123`

### PR Review Process

**What we check:**
- Code quality
- Test coverage
- Documentation completeness
- Physical correctness (for physics code)
- License compliance

**Typical timeline:**
- Initial response: 1-3 days
- Full review: 3-7 days
- Merge: After approval + CI pass

---

## 🐛 Reporting Bugs

**Use GitHub Issues**

**Include:**
- OS and Python version
- Full error message
- Minimal reproduction steps
- Expected vs actual behavior

**Template:**
```markdown
## Bug Description
Brief description of the bug

## Steps to Reproduce
1. Step one
2. Step two
3. ...

## Expected Behavior
What should happen

## Actual Behavior
What actually happens

## Environment
- OS: Windows 10 / Ubuntu 22.04 / macOS 13
- Python: 3.10.5
- SSZ Version: 1.2.3

## Error Message
```
Paste full error here
```

## Additional Context
Any other relevant information
```

---

## 💡 Feature Requests

**Use GitHub Issues with `enhancement` label**

**Include:**
- Clear use case
- Why it's useful
- Proposed implementation (optional)
- Willingness to contribute

---

## 🎓 Physics Contributions

**For physics-related contributions:**

- **Cite sources:** Reference papers, equations
- **Physical interpretation:** Explain what results mean
- **Unit tests:** Verify physical limits (c → ∞, M → 0, etc.)
- **Comparison:** Compare with GR predictions

**Example:**
```python
def test_ppn_limit():
    """Test that SSZ reduces to GR in weak field limit"""
    # Test PPN parameters β = γ = 1
    beta, gamma = calculate_ppn_parameters(weak_field=True)
    
    np.testing.assert_allclose(beta, 1.0, rtol=1e-10)
    np.testing.assert_allclose(gamma, 1.0, rtol=1e-10)
    
    print("✅ SSZ matches GR in weak field limit")
```

---

## 📞 Getting Help

**Questions about contributing?**

1. Check existing documentation
2. Search closed issues/PRs
3. Ask in GitHub Discussions
4. Contact maintainers

**Maintainers:**
- Carmen Wrede
- Lino Casu

---

## 🙏 Thank You!

Every contribution helps make this project better. Whether it's:
- Fixing a typo
- Adding a test
- Implementing a feature
- Improving documentation

**Your contribution matters!** 🌟

---

**Last Updated:** 2025-10-20  
**Version:** 1.0

© 2025 Carmen Wrede & Lino Casu  
Licensed under the ANTI-CAPITALIST SOFTWARE LICENSE v1.4
