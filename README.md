# Terrain-Mesh-Optimization
Research code (Jupyter Notebook) for a hybrid **geometry-aware PSO + ODT-style relaxation** terrain meshing workflow. The optimized mesh is intended for simulation-driven pipelines (e.g., **CFD / FEM** preprocessing over complex terrain), with a geometry-aware density that prioritizes terrain-feature regions.


下面是一份**投稿级、可复现导向**的 `README.md` 成品，你直接复制到仓库根目录的 `README.md` 就行（把尖括号里的占位符换成你的信息即可）。我按 EMS 的要求把 **demo 数据、原始数据不可共享说明、运行步骤、输入输出、关键参数、引用与许可** 都写全了。

````md
# Hybrid Geometry-Aware PSO–ODT for Terrain Meshing in Complex Terrain

Open-source research code for a simulation-driven terrain meshing workflow based on a hybrid
geometry-aware PSO and ODT-style mesh relaxation. The optimized mesh is intended for
CFD and FEM preprocessing over complex terrain.

This repository accompanies the manuscript:
Hybrid Geometry-Aware PSO–ODT for Terrain Meshing in Complex Terrain
submitted to Environmental Modelling and Software.

## Features
- Geometry-aware objective and density construction for terrain-feature preservation
- PSO-driven global search with ODT-style local mesh regularization
- End-to-end reproducible workflow in a single Jupyter Notebook
- Demo terrain dataset included for reviewer reproducibility

---

## Quick start

### 1. Create environment
Python 3.10 or newer is recommended.

```bash
python -m venv .venv
# Windows:
.venv\Scripts\activate
# macOS/Linux:
source .venv/bin/activate

pip install -U pip
pip install -r requirements.txt
````

### 2. Run the notebook

```bash
jupyter lab
```

Open and run all cells:

* notebooks/CkringPso_1.0.ipynb

---

## Repository layout

Recommended structure:

```
.
├── notebooks/
│   └── CkringPso_1.0.ipynb
├── data/
│   └── demo_terrain.xlsx
├── outputs/
│   └── coordinates_3d.xlsx
├── requirements.txt
├── LICENSE
└── README.md
```

---

## Input data

### Demo data

A demo terrain raster is provided at:

* data/demo_terrain.xlsx

The notebook reads a regular grid raster from Excel, for example:

```python
file_path = "data/demo_terrain.xlsx"
df = pd.read_excel(file_path, skiprows=5)
Z = df.to_numpy()
```

Notes:

* skiprows=5 is assumed by default. Adjust it if your Excel layout differs.
* The raster is assumed to be a regular grid of numeric elevations.

### Using your own terrain

Replace file_path with your own raster grid in the same format.
If your DEM is GeoTIFF, ASC, or CSV, convert it to a numeric grid or adapt the loader cell.

Grid spacing:

* The notebook currently maps grid indices to physical coordinates using a fixed spacing factor.
* If your terrain resolution differs, update the spacing factor used to build x and y coordinates.

---

## Outputs

The notebook produces:

* Mesh and diagnostic plots inside the notebook
* Optimized 3D node coordinates exported to Excel

Default export file:

* outputs/coordinates_3d.xlsx

The exported table contains x, y, z for each optimized node.
If triangle connectivity is needed for downstream workflows, you can export it from the Delaunay
triangulation object, for example tri.simplices.

---

## Key parameters for reproducibility

The runtime depends on terrain size and optimization settings.

Common parameters:

* n_particles: number of PSO particles
* n_iterations: number of optimization iterations

Reviewer friendly quick run:

* n_particles = 10
* n_iterations = 30

If random initialization is used, set a fixed seed for repeatability:

* np.random.seed(0)

The notebook may include a raster subset for quick testing. To run the full terrain, disable the subset.

---

## Data availability

* Included: a public demo terrain dataset in data/1test.xlsx for full reproducibility.
* Not included: the original terrain dataset used in the manuscript cannot be shared due to data access
  restrictions and lack of redistribution permission.
* Reproducibility path: users can rerun the workflow on their own terrain by providing a raster grid in the
  same input format and updating file_path.

This enables transparent verification of the method while respecting data sharing constraints.

---

## Dependencies

Core packages used:

* numpy
* pandas
* scipy
* matplotlib
* pywavelets
* openpyxl
* pyKriging



## Citation

If you use this code, please cite:

Hybrid Geometry-Aware PSO–ODT for Terrain Meshing in Complex Terrain
Environmental Modelling and Software, submitted.

BibTeX:

```bibtex
@article{
  title   = {Hybrid Geometry-Aware PSO--ODT for Terrain Meshing in Complex Terrain},
  author  = {Jianxin Xu},
  journal = {Environmental Modelling \& Software},
  year    = {2026},
  note    = {submitted}
}
```

---

## License

Apache-2.0

---

## Contact

For questions and reproducibility issues:

* Corresponding author: sansanoubu@gmail.com

```

