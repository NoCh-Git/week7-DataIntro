# Session 7 — Intro to Data Course

This repository contains the materials for **Session 7** of *Intro to Data Course*.  
- Slides: see [`slides/`](./slides/) folder  
- Notebooks: see [`notebooks/`](./notebooks/) folder 
---

## 📑 Session Outline

This session introduces **Decision Trees** as a third classification approach alongside Logistic Regression and KNN. Decision Tree classifies by asking a sequence of yes/no questions and produces axis-aligned rectangular boundaries rather than a straight line or distance-based vote. From there, the session zooms out to the broader problem of **model complexity**: every model has a "complexity knob" (tree depth, *k*, polynomial degree) and tuning it too high leads to overfitting: perfect training accuracy, poor test accuracy. **Regularisation** is presented as the principled fix: for trees this means constraining depth or leaf size; for linear models it means adding a penalty term (Ridge L2 or Lasso L1) that keeps coefficients small and, in Lasso's case, can drive irrelevant ones to exactly zero. 
The session closes with a brief look under the hood at **gradient descent** — the iterative optimisation procedure that `.fit()` has been running silently in every previous notebook, introducing the general ideas of loss surface, gradient direction, and learning rate.

---

### Part A — Decision Trees & Model Complexity (`00_week7_DecisionTrees_ModelComplexity.ipynb`)

1. **Decision tree fundamentals** — how a tree classifies by asking a sequence of yes/no questions on one feature at a time; anatomy of a node (question, Gini impurity, sample count, majority class)
2. **Gini impurity vs Entropy** — both measure group disorder; Gini is the scikit-learn default because it is cheaper to compute; both produce similar splits in practice
3. **Axis-aligned decision boundaries** — each split creates a rectangular region in feature space; visualising the boundary on a 2-D grid
4. **Depth vs generalisation** — sweeping `max_depth` from 1 to 20; training accuracy rises monotonically to 100 %; test accuracy peaks (around depth 3) then falls — the classic **overfitting** signal
5. **Reading the train/test gap** — a large gap between training and test accuracy indicates a model that has memorised noise rather than learned the underlying pattern

---

### Part B — Regularisation (`01_week7_Regularisation.ipynb`)

6. **Tree regularisation** — constraining trees with `max_depth` and `min_samples_leaf`; fewer leaves = simpler model; trade-off between bias and variance
7. **Ridge regression (L2)** — adds a squared-coefficient penalty; shrinks every coefficient towards zero but never sets any exactly to zero; `alpha` controls penalty strength
8. **Lasso regression (L1)** — adds an absolute-coefficient penalty; can set coefficients **exactly to zero**, performing automatic feature selection (removes `commute_min` and `shoe_size` in the worked example)
9. **Why standardise before penalising** — coefficient size depends on feature units; scaling to the same spread ensures the penalty treats all features fairly
10. **Regularisation path** — plotting coefficients against `alpha`; Ridge curves shrink smoothly; Lasso curves hit zero one by one, dropping irrelevant features first

---
## 🚀 Environment Setup

Before starting, please **fork this repository** and create a fresh Python virtual environment.  
All required libraries are listed in `requirements.txt`.

> ⚠️ If you encounter errors during `pip install`, try removing the version pinning for the failing package(s) in `requirements.txt`.  
> On Apple M1/M2 systems you may also need to install additional system packages (the “M1 shizzle”).

---

### macOS / Linux (bash/zsh)

```bash
# Select Python version (if using pyenv)
pyenv local 3.11.3

# Create and activate virtual environment
python -m venv .venv
source .venv/bin/activate

# Upgrade pip and install dependencies
pip install --upgrade pip
pip install -r requirements.txt
```

### Windows (PowerShell)
```bash
# Select Python version (if using pyenv)
pyenv local 3.11.3

# Create and activate virtual environment
python -m venv .venv
.venv\Scripts\Activate.ps1

# Upgrade pip and install dependencies
python -m pip install --upgrade pip
pip install -r requirements.txt
```

### Windows (Git Bash)
```bash
# Select Python version (if using pyenv)
pyenv local 3.11.3

# Create and activate virtual environment
python -m venv .venv
source .venv/Scripts/activate

# Upgrade pip and install dependencies
python -m pip install --upgrade pip
pip install -r requirements.txt
```

You’re now ready to run the session notebooks!

Deactivate the environment when you’re done:
```bash
deactivate
```
