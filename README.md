A Brief Instruction to *GRP_Solver* -- an implementation of the GRP solver
===

How to use
---

  1. Enter the directory 'GRP_solver/'.
  2. Run 'make'.
  3. Include the header 'GRP_solver/inc/Riemann_solver.h' in the file call the solvers.
  4. Link to the library 'GRP_solver/GRP_Solver.a' when compiling your programm.

Introduction
---

In this package we mainly implement the GRP solver for the two-dimensional Euler equations of the polytropic gases. The codes are in the file './src/system_GRP_solver.c'. The definition of the API can be also found in the file 'GRP_solver/inc/Riemann_solver.h'.


They rely on the Riemann solver. Here we implement an exact Riemann solver in './src/Riemann_solver_exact.c'.

The classical HLL solver is also implemented in './src/HLL.c'.

GRP sovlers for some particular scalar equations are implemented in './src/scalar_GRP_solver.c'.


Numerical Experiments
---

The non-linear GRP solver (by disabling the acoustic case) is tested by the transported of the sine wave and the isentropic flow.

|  m  | L_1 error | L_1 order | L_\infty error | L_\infty order |
|:---:|:---------:|:---------:|:--------------:|:--------------:|
|  20 |  9.85e-6  |           |     3.86e-5    |                |
|  40 |  2.86e-6  |    1.79   |     1.30e-5    |       1.58     |
|  80 |  7.52e-7  |    1.93   |     3.46e-6    |       1.90     |
| 160 |  1.92e-7  |    1.97   |     8.87e-7    |       1.97     |
| 320 |  4.86e-8  |    1.98   |     2.24e-7    |       1.99     |
| 640 |  1.22e-8  |    1.99   |     5.60e-8    |       2.00     |
|1280 |  3.06e-9  |    2.00   |     1.39e-8    |       2.00     |
|2560 |  7.64e-10 |    2.00   |     3.14e-9    |       2.03     |

The acoustic case codes are also tested by the same experiments and the results are almost the same which is reasonable since the flow is smooth.

Applied in the two-stage fourth-order GRP scheme, the numerical results for the same problme are listed in the folowing table.

|  m  | L_1 error | L_1 order | L_\infty error | L_\infty order |
|:---:|:---------:|:---------:|:--------------:|:--------------:|
|  20 |  1.52e-6  |           |     1.48e-5    |                |
|  40 |  1.11e-7  |   3.78    |     1.19e-6    |        3.63    |
|  80 |  7.18e-9  |   3.95    |     7.77e-8    |        3.94    |
| 160 |  4.53e-10 |   3.99    |     5.00e-9    |        3.96    |
| 320 |  5.54e-11 |   3.03    |     4.08e-10   |        3.62    |
| 640 |  5.01e-11 |   0.15    |     1.19e-10   |        1.77    |
|1280 |  4.99e-11 |   0.01    |     1.01e-10   |        0.24    |
|2560 |  4.99e-11 |   0.00    |     1.00e-10   |        0.02    |

It seems that the numerical error quickly goes to the round-off error of the present program, i.e. $1e-10$. Therefore it stops to go down further when the computational mesh is more than 320.
