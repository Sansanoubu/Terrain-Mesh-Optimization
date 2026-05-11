# Terrain-Mesh-Optimization

Research code for the manuscript:

**Hybrid Geometry-Aware PSO–ODT for Terrain Meshing in Complex Terrain**  
Submitted to *Environmental Modelling and Software*.

This repository provides a reproducible Jupyter Notebook implementation of a geometry-aware terrain mesh optimization workflow. The method combines Particle Swarm Optimization (PSO) with an Optimal Delaunay Triangulation (ODT)-style mesh-quality objective. The optimized terrain mesh is intended for simulation-driven workflows, such as CFD or FEM preprocessing over complex terrain.

## Main features

- Geometry-aware terrain-density construction for terrain-feature preservation.
- PSO-driven global search combined with ODT-style local mesh regularization.
- Projection–optimization–reconstruction workflow for terrain mesh generation.
- Kriging-based reconstruction from optimized 2D points to 3D terrain.
- Demo terrain dataset included for reproducibility.

## Repository structure

```text
.
├── notebooks/
│   └── CkringPso_1.0.ipynb
├── data/
│   └── demo_terrain.xlsx
├── requirements.txt
├── LICENSE
└── README.md
```

## Reproduction workflow

The original terrain dataset used in the manuscript cannot be publicly shared due to data access and redistribution restrictions. To support reproducibility, a demo terrain dataset is provided in:

```text
data/demo_terrain.xlsx
```

The main workflow can be reproduced as follows.

### 1. Create the Python environment

Python 3.10 or newer is recommended.

```bash
python -m venv .venv
```

Activate the environment.

For Windows:

```bash
.venv\Scripts\activate
```

For macOS or Linux:

```bash
source .venv/bin/activate
```

Install the required packages:

```bash
pip install -U pip
pip install -r requirements.txt
```

### 2. Open the main notebook

Start Jupyter Lab:

```bash
jupyter lab
```

Open the notebook:

```text
notebooks/CkringPso_1.0.ipynb
```

Run the notebook cells in order. The notebook contains the essential steps of the workflow:

1. terrain data loading;
2. 3D-to-2D projection;
3. terrain-density function construction;
4. PSO–ODT mesh optimization;
5. Kriging-based 3D reconstruction;
6. mesh-quality evaluation;
7. result visualization and export.

### 3. Input data setting

The demo file is read in the data-loading cell of the notebook. The default input path is:

```python
file_path = "data/demo_terrain.xlsx"
```

The demo file is an Excel-based regular elevation grid. By default, the notebook reads the elevation values using:

```python
df = pd.read_excel(file_path, skiprows=5)
Z = df.to_numpy()
```

If your Excel layout is different, update the `skiprows` value in the data-loading cell.

### 4. Using a new terrain dataset

To apply the workflow to another terrain case, replace the demo input file with a user-provided elevation grid and update the input path in the notebook:

```python
file_path = "data/your_terrain_file.xlsx"
```

The input file should contain a regular grid of numeric elevation values in the same format as the demo dataset.

If the original terrain data are stored as GeoTIFF, ASC, CSV, or another DEM format, users should either convert the data into the Excel grid format used by the demo file or modify the data-loading cell accordingly.

The notebook maps grid indices to physical coordinates using a spacing factor. If the terrain resolution differs from the demo case, update the spacing factor in the coordinate-generation cell.

## Key parameters

The main parameters are defined in the parameter cells near the beginning of:

```text
notebooks/CkringPso_1.0.ipynb
```

Important parameters include:

- `n_particles`: number of PSO particles;
- `n_iterations`: maximum number of optimization iterations;
- PSO coefficients controlling individual, global, and geometry-guided search terms;
- grid spacing used to convert raster indices into physical coordinates;
- mesh-quality evaluation settings.

For a quick reviewer-friendly test, the following reduced settings can be used:

```python
n_particles = 10
n_iterations = 30
```

For repeatable results, set a fixed random seed before optimization:

```python
np.random.seed(0)
```

The notebook may use a subset of the terrain grid for quick testing. To run the full terrain case, disable the subset operation in the data-preprocessing cell.

## Outputs

The notebook produces:

- terrain mesh visualization;
- optimization diagnostic plots;
- mesh-quality evaluation results;
- reconstructed 3D terrain points;
- exported optimized node coordinates.

The default output file is:

```text
outputs/coordinates_3d.xlsx
```

The exported table contains the optimized node coordinates:

```text
x, y, z
```

If triangle connectivity is required for downstream workflows, it can be exported from the Delaunay triangulation object, for example:

```python
tri.simplices
```

## Data availability

Included in this repository:

```text
data/demo_terrain.xlsx
```

This demo dataset can be used to reproduce the main computational workflow.

Not included:

The original terrain dataset used in the manuscript cannot be publicly shared due to data access and redistribution restrictions.

Reproducibility path:

Users can reproduce the workflow using the provided demo dataset or apply the method to their own terrain by replacing the input elevation grid and updating the input path in the notebook.

## Dependencies

Core Python packages include:

- `numpy`
- `pandas`
- `scipy`
- `matplotlib`
- `openpyxl`
- `pyKriging`
- `PyWavelets`

All required packages are listed in:

```text
requirements.txt
```

## Citation

If you use this code, please cite:

```text
Xu J. Hybrid Geometry-Aware PSO–ODT for Terrain Meshing in Complex Terrain. Environmental Modelling and Software, submitted.
```

BibTeX:

```bibtex
@article{xu2026terrainmesh,
  title   = {Hybrid Geometry-Aware PSO--ODT for Terrain Meshing in Complex Terrain},
  author  = {Xu, Jianxin},
  journal = {Environmental Modelling and Software},
  year    = {2026},
  note    = {Submitted}
}
```

## License

This repository is released under the Apache-2.0 License.

## Contact

For questions related to reproducibility, please contact:

```text
sansanoubu@gmail.com
```
