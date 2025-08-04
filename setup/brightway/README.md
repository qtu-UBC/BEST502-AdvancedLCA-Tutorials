# 🌱 Brightway LCA Tutorials

This repository supports your learning of Life Cycle Assessment (LCA) using the [Brightway2](https://docs.brightway.dev/en/latest/) framework in Python.

---

## 🔧 One-Time Setup (Required for All Students)

Before using the tutorials, you must install the required environment. Do this **only once**.

▶️ [Click here to launch the setup notebook in Jupyter Open](https://open.jupyter.ubc.ca/hub/user-redirect/git-pull?repo=qtu-UBC/BEST502-AdvancedLCA-Tutorials&branch=main&subPath=setup/brightway/brightway_setup.ipynb)

It will:
- Create a Conda environment called `brightway25`
- Install all required packages
- Register a Jupyter kernel called **Brightway 2.5**

---

## 📚 Tutorials

Each tutorial notebook assumes you’ve already completed the one-time setup above.

| Tutorial | Topic | Launch Link |
|----------|-------|-------------|
| 01 | Intro to LCA | Coming soon |
| 02 | Brightway basics | [Launch in Jupyter Open](https://open.jupyter.ubc.ca/hub/user-redirect/git-pull?repo=YOUR_GITHUB_USERNAME/your-course-repo&branch=main&subPath=tutorials/02-brightway/brightway_tutorial.ipynb) |

---

## 🧪 Local Setup (Optional)

If you're running things locally, you can create the environment with:

```bash
mamba env create -f environment/brightway_env.yml
```

Then register the kernel:

```bash
mamba activate brightway25
python -m ipykernel install --user --name brightway25 --display-name "Brightway 2.5"
```

---
*Last updated: August 04, 2025*
