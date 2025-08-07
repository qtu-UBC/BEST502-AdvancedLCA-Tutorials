# 🌱 BEST502 Brightway Tutorials

This repository supports learning how to perform Life Cycle Assessment (LCA) using the Brightway2.5 framework in Python.

---

## 🚀 Setup Instructions

### ✅ If you're using **UBC Jupyter Open**
Use the **Brightway setup notebook** to install packages and register the kernel:

▶️ [Click here to launch the setup notebook in Jupyter Open](https://open.jupyter.ubc.ca/jupyter/user-redirect/git-pull?repo=https://github.com/qtu-UBC/BEST502-AdvancedLCA-Tutorials&branch=main&subPath=setup/brightway/brightway_setup.ipynb)

This will:
- Install `brightway25`, `bw2io`, and related packages using pip
- Register a new Jupyter kernel called **Brightway 2.5**
- Let you run future notebooks with this kernel

---

### 🧪 If you're setting up **locally**
Use the Conda environment file located at:

```bash
environments/brightway_env.yml
```

Create the environment with:

```bash
mamba env create -f environments/brightway_env.yml
```

Then register the kernel:

```bash
mamba activate brightway25
python -m ipykernel install --user --name brightway25 --display-name "Brightway 2.5"
```

---

## 📚 Tutorials

Once setup is complete, you can run the following tutorials:

| Tutorial | Description | Kernel |
|----------|-------------|--------|
| `brightway_setup_refined.ipynb` | Environment setup for Jupyter Open | base Python |
| `brightway_tutorial.ipynb`     | Basic Brightway project setup & database | Brightway 2.5 |

---

## ❓ FAQ

**Q: Why two setup methods?**  
Because UBC Jupyter Open doesn't support full `conda` environment creation, we use `pip` in a notebook for that platform.

**Q: Do I need to run setup every time?**  
No. Once the environment is installed and the kernel is registered, you only need to select `"Brightway 2.5"` in the kernel menu.

---

*Last updated: August 07, 2025*
