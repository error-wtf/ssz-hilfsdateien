# Quick Start Guide - SSZ Theory

**5-Minute Overview** | Get started with Segmented Spacetime with φ-Scaling

---

## 🎯 What is SSZ?

**Segmented Spacetime with φ-Scaling (SSZ)** is an alternative approach to gravity that:
- Uses discrete spacetime segments instead of continuous curvature
- Incorporates the Golden Ratio φ ≈ 1.618 as a fundamental constant
- Resolves singularities through natural boundaries
- Reproduces General Relativity (GR) (GR) predictions in testable limits

---

## ⚡ Core Concepts (30 seconds each)

### 1. Spacetime Segments
Space is divided into discrete "segments" near massive objects.
- **Like:** Pixels in an image vs continuous canvas
- **Key:** Segments have finite size → no singularities!

### 2. φ-Radius (r_φ)
The characteristic length scale where segmentation becomes important.
- **Formula:** r_φ = φ·(GM/c²)·(1 + Δ/100)
- **For Sun:** r_φ ≈ 2390 m (smaller than Schwarzschild radius)

### 3. Natural Boundary
Spacetime naturally "stops" at r_φ - no infinite densities!
- **Result:** Black holes have finite-size cores
- **Bonus:** Singularity problem solved

### 4. Dual Velocity Invariant
Two complementary velocities that always satisfy: v_esc · v_fall = c²
- **Escape velocity:** How fast to escape gravity
- **Fall velocity:** Complementary infall measure
- **Invariant:** Their product is exactly c²

### 5. GR Compatibility
SSZ matches General Relativity (GR) (GR) where tested:
- **Weak field:** Same as Newton + Einstein
- **Strong field:** Similar predictions with modifications
- **PPN parameters:** β = γ = 1 (like GR)

---

## 🚀 Installation (2 minutes)

```bash
# Clone repository
git clone https://github.com/error-wtf/SSZ-Theory
cd SSZ-Theory

# Install (Windows)
.\install.ps1

# Install (Linux/Mac)
./install.sh

# Run tests
python run_full_suite.py
```

**That's it!** Installation handles dependencies automatically.

---

## 📊 First Analysis (2 minutes)

```python
# Calculate φ-radius for the Sun
from core.physics import calculate_r_phi

M_sun = 1.989e30  # kg
r_phi = calculate_r_phi(M_sun)

print(f"φ-radius: {r_phi:.1f} m")
# Output: φ-radius: 2390.4 m
```

**Compare to Schwarzschild:**
- r_s (GR) = 2953 m
- r_φ (SSZ) ≈ 0.809 × r_s

---

## 🎓 Learning Path

**Choose your journey:**

### For Physicists
1. Read: `docs/PHYSICS_FOUNDATIONS.md`
2. Study: `docs/MATHEMATICAL_FORMULAS.md`
3. Check: Test results in `reports/`

### For Developers
1. Read: `CONTRIBUTING.md`
2. Study: `docs/CODE_IMPLEMENTATION_GUIDE.md`
3. Run: `python run_full_suite.py`

### For Students
1. Start: This Quick Start
2. Next: `README.md`
3. Then: Physics Foundations (section by section)

---

## 🔬 Key Results

**What SSZ predicts:**

| Phenomenon | SSZ Prediction | Status |
|------------|----------------|--------|
| Weak field gravity | Matches GR | ✅ Verified |
| PPN parameters | β=1, γ=1 | ✅ Matches GR |
| Singularities | Resolved at r_φ | 🔬 Testable |
| Black hole core | Finite size | 🔬 Testable |
| Dual velocity | v_esc·v_fall=c² | ✅ Exact |

---

## 📚 Next Steps

**After this guide:**

1. **Understand the Math**
   - Read: `MATHEMATICAL_FORMULAS.md`
   - Focus: Golden Ratio, φ-radius, segments

2. **See the Tests**
   - Run: `python run_full_suite.py`
   - Check: 35 physics tests with interpretations

3. **Explore Data**
   - Location: `data/` directory
   - Examples: Gaia stars, Planck CMB

4. **Contribute**
   - Read: `CONTRIBUTING.md`
   - Join: Development or testing

---

## 💡 FAQs (Quick Answers)

**Q: Is this proven?**
A: SSZ matches GR in all tested regimes. New predictions are testable.

**Q: Why Golden Ratio?**
A: Emerges naturally from segment scaling. Not imposed, but derived.

**Q: Replaces GR?**
A: Alternative approach. Could be complementary or competing.

**Q: Can I test this?**
A: Yes! Code is open-source. Run tests yourself.

**Q: Where to learn more?**
A: Start with README, then Physics Foundations document.

---

## 🆘 Get Help

**Stuck? Try:**
- `TROUBLESHOOTING.md` - Common issues
- `README.md` - Detailed overview
- GitHub Issues - Ask questions

---

## ⏱️ Time Budget

- **5 minutes:** This guide
- **30 minutes:** Run tests + explore
- **2 hours:** Read physics foundations
- **1 day:** Understand core concepts
- **1 week:** Contribute to project

---

**Welcome to SSZ! Let's explore Segmented Spacetime together.** 🚀

© 2025 Carmen Wrede & Lino Casu
