Json files
----------

Complete example
```json
{
    "mesh": " ",                    "Mesh path"
    "bc_tag": " ",                  "Path to the boundary tag file, each face/edge is associated with an unique number (you can use bc_setter for setting them in 3d)"
    "normalize_mesh": true,         "Normalize mesh such that it fits in the [0,1] bounding box"

    "n_refs": 0,                    "Number of uniform refinement"
    "refinenemt_location": 0.5,     "Refiniement location of polyhedra"

    "scalar_formulation": "Laplacian",
    "tensor_formulation": "LinearElasticity",
    "mixed_formulation": "Stokes",

    "count_flipped_els": false,     "Count (or not) flipped elements"

    "iso_parametric": false,        "Force isoparametric elements"
    "discr_order": 1,               "Dicretization order, supports P1, P2, P3, P4, Q1, Q2"

    "pressure_discr_order": 1,      "Pressure dicrezation order, for mixed formulation"

    "output": "",                   "Output json path"

    "problem": "Franke",            "Problem to solve"
    "problem_params": {},           "Problem specific parameters"

    "n_boundary_samples": 6,        "number of boundary samples (Dirichelt) or quadrature points (Neumann)"
    "quadrature_order": 4,          "quadrature order"

    "export": {                     "Export options"
        "full_mat": "",             "Stiffnes matrix without boundary conditions"
        "iso_mesh": "",             "Isolines mesh"
        "nodes": "",                "FE nodes"
        "solution": "",             "Solution vector"
        "spectrum": false,          "Spectrum of the stiffness matrix"
        "stiffness_mat": "",        "Stiffmess matrix after setting boundary conditions"
        "vis_boundary_only": false, "Exports only the boundary of volumetric meshes"
        "vis_mesh": "",             "Path for the vtu mesh"
        "wire_mesh": ""             "Wireframe of the mesh"
    },

    "use_spline": false,            "Use spline for quad/hex elements"
    "fit_nodes": false,             "Fit nodes for spline basis"

    "integral_constraints": 2,      "Number of constraints for polygonal basis 0, 1, or 2"
    "n_harmonic_samples": 10,       "Number of face/line samples for harmonic bases for polyhedra"

    "B": 3,                         "User provided parameter for pref tolerance"
    "use_p_ref": false,             "Enable prefinement for badly shaped simplices"
    "discr_order_max": 4,           "Maximum allowed dicrezation oder, used in p pref"
    "h1_formula": false,            "Use pref formula for h1 bound"

    "solver_type": "Pardiso",       "Library for linear solver"
    "precond_type": "Eigen::DiagonalPreconditioner",
    "solver_params": {},            "solver specific parameters"

    "nl_solver": "newton",          "Non linear solver"
    "line_search": "armijo",        "Line search for newton solver"
    "nl_solver_rhs_steps": 1,       "Number of incremental load steps"
    "save_solve_sequence": false,   "Save all incremental load steps"

    "params": {                     "Material parameter"
        "k": 1.0,                   "Constant in helmolz"

        "elasticity_tensor": {},    "Elasticity tensor, used in hooke and saint ventant"

        "E": 1.5,                   "Young modulus"
        "nu": 0.3,                  "Poisson's ratio"

        "lambda": 0.329670329,      "Lame parameter, E, nu have priority"
        "mu": 0.384615384,
    },


    "tend": 1,                      "End time for time dependent simulations"
    "time_steps": 10,               "Number of time steps for time dependent simulations"

    "vismesh_rel_area": 1e-05       "Relative resolution of the output mesh"
}
```

### Optionals

* **scalar_formulation**: Helmholtz, Laplacian
* **tensor_formulation**: HookeLinearElasticity, LinearElasticity, NeoHookean, Ogden, SaintVenant
* **mixed_formulation**: IncompressibleLinearElasticity, Stokes

* **problem**: CompressionElasticExact, Cubic, DrivenCavity, Elastic, ElasticExact, ElasticZeroBC, Flow, Franke, GenericTensor, Gravity, Kernel, Linear, LinearElasticExact, MinSurf, PointBasedTensor, Quadratic, QuadraticElasticExact, Sine, TestProblem, TimeDependentFlow, TimeDependentScalar, TorsionElastic, Zero_BC


* **solver_type**: Eigen::BiCGSTAB, Eigen::ConjugateGradient, Eigen::GMRES, Eigen::MINRES, Eigen::SimplicialLDLT, Eigen::SparseLU, Hypre,Pardiso
* **nl_solver**: lbfgs, newton
* **line_search**: armijo, armijo_alt, bisection, more_thuente


Problems
--------
Each problem has a specific set of optional `problem_params` described here.

### CompressionElasticExact
**Has exact solution**: true<br/>
**Time dependent**: false<br/>
**Form**: tensor<br/>
**Description**: solve for<br/>
$\begin{align}
f_{2D}(x,y) &= -\begin{bmatrix}(y^3 + x^2 + xy)/20\\ (3x^4 + xy^2 + x)/20\end{bmatrix}\\
f_{3D}(x,y,z) &= -\begin{bmatrix}(xy + x^2 + y^3 + 6z)/14\\ (zx - z^3 + xy^2 + 3x^4)/14\\ (xyz + y^2z^2 - 2x)/14\end{bmatrix}
\end{align}$

### Cubic
**Has exact solution**: true<br/>
**Time dependent**: false<br/>
**Form**: scalar<br/>
**Description**: solve for<br/>
$f(x,y,z) = (2y-0.9)^4 + 0.1$

### DrivenCavity
**Has exact solution**: false<br/>
**Time dependent**: false<br/>
**Form**: mixed<br/>
**Description**: solve for zero right-hand side, and 0.25 for boundary id 1<br/>

### Elastic
**Has exact solution**: false<br/>
**Time dependent**: false<br/>
**Form**: tensor<br/>
**Description**: solve for zero right-hand side, -0.25 for boundary id 1/5, 0.25 for id 3/6<br/>

### ElasticExact
**Has exact solution**: true<br/>
**Time dependent**: false<br/>
**Form**: tensor<br/>
**Description**: solve for<br/>
$\begin{align}
f_{2D}(x,y) &= \begin{bmatrix}(y^3 + x^2 + xy)/50\\ (3x^4 + xy^2 + x)/50\end{bmatrix}\\
f_{3D}(x,y,z) &= \begin{bmatrix}(xy + x^2 + y^3 + 6z)/80\\ (xz - z^3 + xy^2 + 3x^4)/80\\ (xyz + y^2 z^2 - 2x)/80\end{bmatrix}
\end{align}$

### ElasticZeroBC
**Has exact solution**: false<br/>
**Time dependent**: false<br/>
**Form**: tensor<br/>
**Description**: solve for [0, 0.5, 0] right-hand side and zero boundary condition<br/>

### Flow
**Has exact solution**: false<br/>
**Time dependent**: false<br/>
**Form**: mixed<br/>
**Description**: solve for zero right-hand side, [0.25, 0, 0] for boundary id 1/3, [0, 0, 0] for 7<br/>

### Franke
**Has exact solution**: true<br/>
**Time dependent**: false<br/>
**Form**: scalar<br/>
**Description**: solves for the 2D and 3D Franke function

### GenericTensor
**Has exact solution**: false<br/>
**Time dependent**: false<br/>
**Form**: tesor<br/>
**Description**: solves for generic tensor problem with zero body forces<br/>
**Options**:
```json
"use_mixed_formulation": false,     "Use mixed formulation"
"dirichlet_boundary": [             "List of Dirichelt boundaries"
{
    "id": 1,                        "Boundary id"
    "value": [0, 0, 0],             "Boundary vector value"
    "dimension": [                  "Which dimension are Dirichelt"
            true,
            true,
            false                   "In this case z is free"
        ]
},
{
    "id": 2,                        "Boundary id"
    "value": ["sin(x)+y", "z^2", 0],"Formulas are supported"
}],
"neumann_boundary": [               "List of Neumann boundaries"
{
    "id": 3,                        "Boundary id"
    "value": [0, 0, 0],             "Boundary vector value"
},
{
    "id": 4,                        "Boundary id"
    "value": ["sin(x)+y", "z^2", 0],"Formulas are supported"
}]
```

### Gravity
**Has exact solution**: false<br/>
**Time dependent**: true<br/>
**Form**: tensor<br/>
**Description**: solves for 0.1 body force in y direction and zeor for boundray 4

### Kernel
**Has exact solution**: true<br/>
**Time dependent**: false<br/>
**Form**: scalar/tensor<br/>
**Description**: solves the omogenous PDE with `n_kernels` kernels placed on the bounding box at `kernel_distance`<br/>
**Options**: `n_kernels` sets the number of kernels, `kernel_distance` sets the distance from the bounding box

### Linear
**Has exact solution**: true<br/>
**Time dependent**: false<br/>
**Form**: scalar<br/>
**Description**: solve for<br/>
f(x,y,z) = x

### LinearElasticExact
**Has exact solution**: true<br/>
**Time dependent**: false<br/>
**Form**: tensor<br/>
**Description**: solve for<br/>
$\begin{align}
f_{2D}(x,y) &= \begin{bmatrix}-(y + x)/50\\ -(3x + y)/50\end{bmatrix}\\
f_{3D}(x,y,z) &= \begin{bmatrix}-(y + x + z)/50\\ -(3x + y - z)/50\\ -(x + y - 2z)/50\end{bmatrix}\\
\end{align}$

### MinSurf
**Has exact solution**: false<br/>
**Time dependent**: false<br/>
**Form**: scalar<br/>
**Description**: solve for -10 for rhs, and zero Dirichelt boundary condition

### PointBasedTensor
**Has exact solution**: false<br/>
**Time dependent**: false<br/>
**Form**: tesor<br/>
**Description**: solves for point-based boudary conditions<br/>
**Options**:
```json
"scaling": 1,               "Scaling factor"
"rhs": 0,                   "Right-hand side"
"translation": [0, 0, 0]    "Translation"
"boundary_ids": [           "List of Dirichelt boundaries"
{
    "id": 1,                "Boundary id"
    "value": [0, 0, 0]      "Boundary vector value"
},
{
    "id": 2,
    "value": {              "Rbf interpolated value"
        "function": "",     "Function file"
        "points": "",       "Points file"
        "rbf": "gaussian",  "Rbf kernel"
        "epsilon": 1.5,     "Rbf epsilon"
        "coordinate": 2,    "Coordinate to ignore"

        "dimension": [      "Which dimension are Dirichelt"
            true,
            true,
            false           "In this case z is free"
        ]
    }
},
,
{
    "id": 2,
    "value": {              "Rbf interpolated value"
        "function": "",     "Function file"
        "points": "",       "Points file"
        "triangles": "",    "Triangles file"
        "coordinate": 2,    "Coordinate to ignore"
    }
}]
```

### Quadratic
**Has exact solution**: true<br/>
**Time dependent**: false<br/>
**Form**: scalar<br/>
**Description**: solve for<br/>
$f(x,y,z) = x^2$

### QuadraticElasticExact
**Has exact solution**: true<br/>
**Time dependent**: false<br/>
**Form**: tensor<br/>
**Description**: solve for<br/>
$\begin{align}
f_{2D}(x,y) &= \begin{bmatrix} -(y^2 + x^2 + xy)/50\\ -(3x^2 + y)/50\end{bmatrix}\\
f_{3D}(x,y,z) &= \begin{bmatrix}-(y^2 + x^2 + xy + yz)/50\\ -(3x^2 + y + z^2)/50\\ -(xz + y^2 - 2z)/50\end{bmatrix}
\end{align}$

### Sine
**Has exact solution**: true<br/>
**Time dependent**: false<br/>
**Form**: scalar<br/>
**Description**: solve for<br/>
$\begin{align}
f(x,y) &= \sin(10x)\sin(10y)\\
f(x,y,z) &= \sin(10x)\sin(10y)\sin(10z)
\end{align}$

### TestProblem
**Has exact solution**: true<br/>
**Time dependent**: false<br/>
**Form**: scalar<br/>
**Description**: solve for extreme problem to test errors for high order discretizations

### TimeDependentFlow
**Has exact solution**: false<br/>
**Time dependent**: true<br/>
**Form**: mixed<br/>
**Description**: solve for zero right-hand side, [0.25, 0, 0] for boundary id 1/3, [0, 0, 0] for 7, and zero inital velocity<br/>

### TimeDependentScalar
**Has exact solution**: false<br/>
**Time dependent**: true<br/>
**Form**: scalar<br/>
**Description**: solve for one right-hand side, zero boundary condition, and zero time boundary<br/>

### TorsionElastic
**Has exact solution**: false<br/>
**Time dependent**: false<br/>
**Form**: tensor<br/>
**Description**: solve for zero body forces, `fixed_boundary` fixed (zero displacement), `turning_boundary` rotating around `axis_coordiante` for `n_turns`<br/>
**Options**: `fixed_boundary` id of the fixed boundary, `turning_boundary` id of the moving boundary, `axis_coordiante` coordinate of the rotating axis, `n_turns` number of turns

### Zero_BC
**Has exact solution**: true<br/>
**Time dependent**: false<br/>
**Form**: tensor<br/>
**Description**: solve for<br/>
$\begin{align}
f_{2D}(x,y) &= (1 - x)  x^2 y (1-y)^2\\
f_{3D}(x,y,z) &= (1 - x)  x^2 y (1-y)^2 z (1 - z)
\end{align}$