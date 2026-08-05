# Tools & Software Used in This Repository

**Complete inventory of all tools, software, and platforms used for development, analysis, and documentation.**

---

## 🤖 AI-Assisted Development Tools

### ChatGPT (OpenAI)
- **Purpose:** Code review, documentation assistance, theoretical discussions
- **Usage:** Algorithm optimization, documentation writing, scientific explanation refinement
- **Version:** GPT-4 and GPT-3.5-turbo
- **Contribution:** Helped refine mathematical explanations and documentation structure

### Windsurf (Codeium)
- **Purpose:** AI-powered IDE with Cascade agent for pair programming
- **Usage:** Code development, debugging, test writing, documentation creation
- **Features:** Real-time code suggestions, multi-file editing, terminal integration
- **Contribution:** Major contributor to v1.3.1 documentation overhaul and testing suite

### Ollama
- **Purpose:** Local LLM deployment for privacy-sensitive code review
- **Usage:** Offline code analysis, local documentation generation
- **Models:** Llama 2, Code Llama, Mistral
- **Contribution:** Local validation of scientific computations

---

## 💻 Programming Languages & Core Tools

### Python 3.10+
- **Purpose:** Primary language for all analysis, modeling, and testing
- **Version:** 3.10, 3.11, 3.12 (cross-version tested)
- **Usage:** All scripts, tests, data processing, visualization

**Key Libraries:**
- **NumPy** (1.24+) - Numerical computing, array operations
- **SciPy** (1.10+) - Scientific computing, optimization, statistical tests
- **Pandas** (2.0+) - Data manipulation, CSV handling, DataFrame operations
- **Matplotlib** (3.7+) - Plotting, visualization, figure generation
- **Astropy** (5.3+) - Astronomical calculations, units, coordinates
- **pytest** (7.4+) - Test framework, assertions, fixtures
- **decimal** - High-precision arithmetic for φ calculations

### MATLAB
- **Purpose:** Supplementary analysis and validation
- **Usage:** Independent verification of numerical results
- **Scripts:** Comparison scripts for cross-validation
- **Note:** Not required for repository use, Python is primary

---

## 📊 Data Sources & Acquisition Tools

### NASA/IPAC NED (NASA/IPAC Extragalactic Database)
- **Purpose:** Primary astronomical data source
- **URL:** https://ned.ipac.caltech.edu/
- **Data:** 284 continuum spectrum observations (M87, Sgr A*)
- **Access:** Web interface + bulk download
- **Citation:** Required for all NED data usage

### SIMBAD (Strasbourg Astronomical Data Center)
- **Purpose:** Stellar and emission line data
- **URL:** http://simbad.u-strasbg.fr/simbad/
- **Data:** Emission line observations, stellar parameters
- **Access:** Web interface + TAP service
- **Citation:** Required for all SIMBAD data

### ESA Gaia Archive
- **Purpose:** High-precision stellar astrometry
- **URL:** https://gea.esac.esa.int/archive/
- **Data:** Stellar positions, parallaxes, proper motions
- **Scripts:** `src/fetch_gaia.py`, `scripts/fetch_gaia_data.py`
- **Access:** ADQL queries via TAP service

### ESA Planck Legacy Archive
- **Purpose:** CMB power spectrum data
- **URL:** https://pla.esac.esa.int/
- **Data:** COM_PowerSpect_CMB-TT-full_R3.01.txt (2 GB)
- **Scripts:** `scripts/fetch_planck.py`
- **Download:** Automated fetch with progress bar

### VizieR (CDS Strasbourg)
- **Purpose:** Catalog cross-matching and planetary data
- **URL:** http://vizier.u-strasbg.fr/
- **Data:** Solar System body catalogs, orbital elements
- **Access:** Astroquery interface

---

## 🔬 Scientific Computing Tools

### Jupyter Notebook
- **Purpose:** Interactive analysis, prototyping, documentation
- **Version:** JupyterLab 4.0+
- **Files:** `*.ipynb` notebooks for demonstrations
- **Usage:** Google Colab integration, local development

### Google Colab
- **Purpose:** Zero-installation cloud execution
- **URL:** https://colab.research.google.com/
- **Features:** Free GPU/TPU, integrated with GitHub
- **Notebooks:** `SSZ_Full_Pipeline_Colab.ipynb`

---

## 📈 Visualization & Plotting

### Matplotlib
- **Purpose:** Primary plotting library
- **Version:** 3.7+
- **Usage:** All scientific plots, publication figures
- **Resolution:** 300 DPI for publication quality

### Plotly
- **Purpose:** Interactive 3D visualizations
- **Version:** 5.14+
- **Usage:** 3D spacetime mesh visualization, interactive dashboards
- **Features:** WebGL rendering, real-time parameter adjustment

### LaTeX (via Matplotlib)
- **Purpose:** Mathematical typesetting in plots
- **Backend:** matplotlib.mathtext
- **Usage:** Axis labels, equations, annotations

---

## 🧪 Testing & Quality Assurance

### pytest
- **Purpose:** Primary testing framework
- **Version:** 7.4+
- **Usage:** 71 tests (69 automated + 2 smoke)
- **Features:** Fixtures, parameterization, coverage reporting

### pytest-cov (Coverage.py)
- **Purpose:** Code coverage analysis
- **Usage:** Test coverage metrics, gap identification

### GitHub Actions
- **Purpose:** Continuous Integration/Continuous Deployment (CI/CD)
- **Configuration:** `.github/workflows/`
- **Testing:** 6 configurations (2 OS × 3 Python versions)
- **Platforms:** Ubuntu-latest, Windows-latest

---

## 💾 Version Control & Collaboration

### Git
- **Purpose:** Version control system
- **Version:** 2.40+
- **Usage:** All code changes, branching, history tracking
- **Best Practices:** Semantic commit messages, atomic commits

### GitHub
- **Purpose:** Repository hosting, collaboration, CI/CD
- **URL:** https://github.com/error-wtf/Segmented-Spacetime-Mass-Projection-Unified-Results
- **Features:** Issues, pull requests, releases, actions
- **Access:** Public repository under ANTI-CAPITALIST SOFTWARE LICENSE v1.4

---

## 📝 Documentation Tools

### Markdown
- **Purpose:** All documentation format
- **Flavor:** GitHub-flavored Markdown (GFM)
- **Usage:** 312+ documentation files
- **Tools:** Markdown linters, preview tools

### Pandoc
- **Purpose:** Document conversion (Markdown ↔ PDF/HTML)
- **Usage:** Academic paper formatting, PDF generation
- **Formats:** MD → PDF, MD → LaTeX, MD → HTML

### MkDocs
- **Purpose:** Static documentation site generation
- **Theme:** Material for MkDocs
- **Usage:** Potential future documentation website

---

## 🖥️ Development Environments

### VS Code (Visual Studio Code)
- **Purpose:** Primary IDE
- **Extensions:** Python, Jupyter, Markdown, Git
- **Features:** IntelliSense, debugging, integrated terminal

### Windsurf IDE
- **Purpose:** AI-enhanced development environment
- **Features:** Cascade agent, real-time suggestions, pair programming
- **Usage:** Majority of v1.3.1 development and documentation

### PyCharm (optional)
- **Purpose:** Alternative Python IDE
- **Usage:** Scientific tools, debugging, profiling

---

## 🐧 Operating Systems & Platforms

### Tested and Supported:
- **Windows 10/11** - PowerShell, UTF-8 configured
- **Ubuntu Linux** (20.04, 22.04, 24.04) - Native, fastest
- **WSL (Windows Subsystem for Linux)** - Auto-detected
- **macOS** (11+) - Unix-like, Homebrew supported
- **Google Colab** - Ubuntu-based, cloud environment

### Cross-Platform Testing:
- CI/CD on GitHub Actions: Ubuntu + Windows
- Manual testing: All 5 platforms verified

---

## 📦 Package Management

### pip
- **Purpose:** Python package manager
- **Usage:** All dependencies in `requirements.txt`
- **Commands:** `pip install -r requirements.txt`

### Conda/Mamba (optional)
- **Purpose:** Alternative environment manager
- **Usage:** Scientific computing environments
- **Benefits:** Binary packages, faster resolution

### Homebrew (macOS)
- **Purpose:** macOS package manager
- **Usage:** Installing system dependencies
- **Packages:** Python, Git, LaTeX tools

---

## 🔧 Utility Tools

### PowerShell 7+
- **Purpose:** Windows scripting and automation
- **Scripts:** `install.ps1`, automated installers
- **Features:** Cross-platform compatible

### Bash/Zsh
- **Purpose:** Linux/macOS scripting
- **Scripts:** `install.sh`, test runners
- **Features:** POSIX-compliant

### curl/wget
- **Purpose:** Data download utilities
- **Usage:** Fetching Planck data, API requests
- **Scripts:** Integrated in `fetch_*.py` scripts

### ripgrep (rg)
- **Purpose:** Fast code search
- **Usage:** Searching codebase, grep replacement
- **Speed:** Much faster than traditional grep

---

## 📐 Mathematical Tools

### SymPy
- **Purpose:** Symbolic mathematics
- **Usage:** Analytical derivations, equation verification
- **Features:** LaTeX output, simplification

### mpmath
- **Purpose:** Arbitrary-precision arithmetic
- **Usage:** High-precision φ calculations
- **Features:** Beyond float64 precision

### Python decimal module
- **Purpose:** Exact decimal arithmetic
- **Usage:** φ = (1+√5)/2 to 50 decimal places
- **Features:** Avoids floating-point errors

---

## 🎨 Design & Formatting Tools

### Black (Python formatter)
- **Purpose:** Consistent Python code formatting
- **Style:** PEP 8 compliant
- **Usage:** Automatic code formatting

### isort
- **Purpose:** Import statement organization
- **Usage:** Alphabetized, grouped imports

### Ruff (Python linter)
- **Purpose:** Fast Python linter
- **Usage:** Code quality checks, best practices

---

## 📊 Data Formats & Standards

### CSV (Comma-Separated Values)
- **Usage:** All tabular data
- **Encoding:** UTF-8 with BOM (cross-platform)
- **Libraries:** pandas read_csv/to_csv

### JSON
- **Usage:** Configuration files, metadata
- **Files:** GAIA cone configs, metadata.json
- **Libraries:** Python json module

### YAML
- **Usage:** Configuration files (alternative)
- **Files:** CI/CD configs, settings
- **Libraries:** PyYAML

### FITS (Flexible Image Transport System)
- **Usage:** Astronomical data (Planck, GAIA)
- **Libraries:** Astropy.io.fits

---

## 🔐 Security & Privacy Tools

### .gitignore
- **Purpose:** Exclude sensitive/large files from git
- **Configuration:** Comprehensive 529-line file
- **Patterns:** API keys, temp files, large data

### Environment Variables
- **Purpose:** Secure credential storage
- **Files:** .env (not tracked), .env.example (template)
- **Usage:** API keys, database credentials

---

## 📚 Reference & Citation Tools

### BibTeX
- **Purpose:** Citation management
- **Usage:** Academic paper citations
- **Format:** Standard BibTeX entries

### Zotero (optional)
- **Purpose:** Reference management
- **Usage:** Organizing sources, generating citations
- **Export:** BibTeX format

---

## 🌐 Web Tools & APIs

### Astroquery
- **Purpose:** Python interface to astronomical databases
- **Services:** NED, SIMBAD, VizieR, Gaia
- **Usage:** Automated data queries
- **Documentation:** https://astroquery.readthedocs.io/

### ADQL (Astronomical Data Query Language)
- **Purpose:** SQL-like queries for astronomical data
- **Usage:** Gaia TAP service queries
- **Syntax:** SQL-based with astronomical extensions

### TAP (Table Access Protocol)
- **Purpose:** VO (Virtual Observatory) data access
- **Usage:** Gaia Archive, other VO services
- **Implementation:** PyVO library

---

## 🔬 Scientific Validation Tools

### WolframAlpha
- **Purpose:** Independent mathematical verification
- **Usage:** Cross-checking analytical results
- **Access:** Web interface + API

### SageMath (optional)
- **Purpose:** Open-source mathematics software
- **Usage:** Symbolic computations, alternative to Mathematica
- **Integration:** Can interface with Python

---

## 📖 Documentation Standards

### Keep a Changelog
- **Purpose:** Changelog format standard
- **URL:** https://keepachangelog.com/
- **Usage:** CHANGELOG.md structure

### Semantic Versioning
- **Purpose:** Version numbering standard
- **URL:** https://semver.org/
- **Format:** MAJOR.MINOR.PATCH (1.3.1)

### Markdown Style Guide
- **Purpose:** Consistent documentation formatting
- **Rules:** Headers, lists, code blocks, links
- **Linting:** markdownlint

---

## 🏗️ Build & Packaging Tools

### setuptools
- **Purpose:** Python package building
- **Files:** setup.py, pyproject.toml
- **Usage:** Creating distributable packages

### wheel
- **Purpose:** Python wheel format
- **Usage:** Binary distribution format
- **Benefits:** Faster installation than source

### Debian packaging
- **Purpose:** .deb package creation
- **Files:** debian/ directory structure
- **Platform:** Linux (Debian, Ubuntu)

---

## 💡 IDE Extensions & Plugins

### VS Code Extensions:
- **Python** (Microsoft) - Language support
- **Pylance** - Fast language server
- **Jupyter** - Notebook support
- **GitLens** - Enhanced Git integration
- **Markdown All in One** - Markdown tools
- **Code Spell Checker** - Typo detection

### Windsurf Plugins:
- **Cascade Agent** - AI pair programming
- **Multi-file editing** - Simultaneous edits
- **Terminal integration** - Embedded shell

---

## 🎯 Performance & Profiling

### cProfile
- **Purpose:** Python profiling
- **Usage:** Performance analysis, bottleneck identification
- **Output:** Function call statistics

### line_profiler
- **Purpose:** Line-by-line profiling
- **Usage:** Identifying slow code lines
- **Decorator:** @profile for targeted profiling

### memory_profiler
- **Purpose:** Memory usage analysis
- **Usage:** Tracking memory consumption
- **Features:** Line-by-line memory tracking

---

## 📊 Summary Statistics

**Total Tools Used:** 50+  
**AI Tools:** 3 (ChatGPT, Windsurf, Ollama)  
**Programming Languages:** 2 (Python primary, MATLAB supplementary)  
**Data Sources:** 5 (NED, SIMBAD, Gaia, Planck, VizieR)  
**Testing Platforms:** 5 (Windows, Linux, macOS, WSL, Colab)  
**Python Libraries:** 15+ core libraries  
**Development Tools:** 10+ IDEs and editors  

---

## 🙏 Acknowledgments

This project benefited from the open-source community, astronomical databases maintained by ESA/NASA/IPAC, and AI-assisted development tools. All tools used are properly credited and comply with their respective licenses.

**Special Thanks:**
- ESA Gaia mission for high-precision astrometry
- NASA/IPAC for NED database maintenance
- CDS Strasbourg for SIMBAD and VizieR services
- OpenAI for GPT models
- Codeium for Windsurf IDE
- Python Software Foundation and all library maintainers

---

## 📝 Tool Usage Best Practices

1. **AI Tools:** Used for assistance, not replacement of human expertise
2. **Data Sources:** Always cited, provenance tracked
3. **Open Source:** Preferred when possible
4. **Cross-Platform:** Tested on multiple platforms
5. **Documentation:** Every tool documented with purpose
6. **Licensing:** All usage compliant with tool licenses
7. **Reproducibility:** Tool versions specified for reproducibility

---

## 🔗 Useful Links

- **Python:** https://www.python.org/
- **NumPy:** https://numpy.org/
- **SciPy:** https://scipy.org/
- **Matplotlib:** https://matplotlib.org/
- **Astropy:** https://www.astropy.org/
- **GitHub:** https://github.com/
- **Windsurf:** https://codeium.com/windsurf
- **OpenAI:** https://openai.com/
- **NED:** https://ned.ipac.caltech.edu/
- **Gaia Archive:** https://gea.esac.esa.int/

---

**Last Updated:** 2025-10-20  
**Repository Version:** v1.3.1

© 2025 Carmen Wrede, Lino Casu  
Licensed under the ANTI-CAPITALIST SOFTWARE LICENSE v1.4
