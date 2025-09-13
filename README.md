# 🧩 Adaptive FEM in Python — Error-Driven Mesh Refinement (2D Poisson)

This project implements an **Adaptive Finite Element Method (FEM)** for the **2D Poisson equation** using **error-driven mesh refinement (AMR)**.  
It demonstrates the full loop: **mesh → assemble sparse K → solve Ku = b → a-posteriori error (ZZ) → bulk mark → longest-edge bisection → repeat**, with visualizations at every cycle.

The study shows how **initial mesh resolution**, **marking fraction (θ)**, and **number of refinement cycles** affect **accuracy**, **mesh density**, and **convergence**.

---

## 📁 Contents
- **Code.ipynb** — Jupyter/Colab notebook with the full adaptive pipeline and plots  
- **adaptive_poisson_2d.py** — Single-file Python script (same logic as the notebook)  
- **1.png**, **2.png** — Example figures (mesh/solution/error/convergence)  
- **AMR_Report.pdf** — *(optional)* short write-up with background and results

---

## 🧰 Tools & Libraries
- **Python** — core implementation  
- **NumPy / SciPy (sparse)** — FEM assembly and linear solves  
- **Matplotlib** — 2D visualizations (mesh, fields, convergence)  
- **Pandas** — export/inspect results

---

## 🔍 Key Highlights
- **End-to-end AMR** for the 2D Poisson problem on \([0,1]^2\) with **P1 triangles**  
- **Zienkiewicz–Zhu (ZZ)** a-posteriori error estimator via gradient recovery  
- **Dörfler (bulk) marking**: refine the smallest set covering ~θ of total estimated error  
- **Longest-edge bisection** with neighbor conformity (no hanging nodes)  
- **Convergence**: estimated error **decreases** as DOFs increase; refinement clusters where the physics needs resolution

---

## 📈 Output Visuals
Includes:
- **Mesh (cycle i)** — shows where triangles concentrate as refinement proceeds  
- **Solution field \(u(x,y)\)** — filled contours; \(u=0\) on the boundary  
- **Estimated error (cycle i)** — heatmap that **drives** where we refine next  
- **Convergence curve** — log–log plot of estimated error vs. DOFs (nodes)

---

## 🧪 Method (short)
1. **Problem**  
   \[
   -\Delta u = f(x,y)\ \text{ in } (0,1)^2,\quad u=0\ \text{ on } \partial\Omega,
   \]
   with \( f(x,y)=10\sin(\pi x)\sin(\pi y) \).

2. **Discretize** — uniform grid split into triangles (P1 basis).  
3. **Assemble** — element \(K_e = |T|\,(B^\top B)\) and centroid load → scatter into global **sparse CSR** matrix \(K\).  
4. **Apply BCs** — Dirichlet \(u=0\) by overwriting rows.  
5. **Solve** — \(Ku=b\) via SciPy’s sparse solver.  
6. **Estimate error (ZZ)** — compare element gradient to recovered nodal gradient; sum per-element indicators.  
7. **Mark & refine** — Dörfler bulk marking (fraction θ) + **longest-edge bisection**; fix neighbors for conformity.  
8. **Repeat** — reassemble, resolve, re-estimate; plot results each cycle.

---

## ▶️ How to Run
### Notebook
1. Open **Code.ipynb** (works in Jupyter or Google Colab).  
2. Run all cells — you’ll see the mesh, solution, error heatmaps, and convergence plots.

## 📬 Contact
Created by **Sourabh More**.  
Feel free to connect or reach out with questions or collaboration ideas!



