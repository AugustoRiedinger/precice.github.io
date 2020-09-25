---
title: Step 1 – Preparation
permalink: couple-your-code-preparing-your-solver.html
keywords: api, adapter, library, software engineering, CFD, fluid
summary: "Do you want to build your own adapter? It is not so difficult if you approach it step-by-step! In the first step, we have a look at how you need to prepare the solver you want to couple."
---

Let's say you want to prepare a fluid solver for fluid-structure interaction and that your code looks like this: 

```cpp
turnOnSolver(); //e.g. setup and partition mesh 

double dt; // solver timestep size

while (not simulationDone()){ // time loop
  dt = beginTimeStep(); // e.g. compute adaptive dt 
  computeTimeStep(dt);
  endTimeStep(); // e.g. update variables, increment time
}
turnOffSolver();
```

Probably most solvers have such a structures: something in the beginning (reading input, domain decomposition), a big time loop, and something in the end. Each timestep also falls into three parts: some pre-computations (e.g. computing an adaptive timestep size), the actual computation (solving a linear or non-linear equation system), and something in the end (updating variables, incrementing time). Try to identify these parts in the code you want to couple.

In the following steps, we will slowly add more and more calls to the preCICE API in this code snippet. Some part of the preCICE API is briefly described in each step. More precisely (no pun intended :grin:), we use the `C++` API of preCICE. The API is, however, also available in other scientific programming languages: plain `C`, `Fortran`, `Python`, and `Matlab` (see [Application Programming Interface](couple-your-code-prerequisites#application-programming-interface)).

{% include tip.html content="Also have a look at the [definite C++ API documentation](https://www.precice.org/doxygen/master/classprecice_1_1SolverInterface.html.)" %}

{% include note.html content="This example refers to preCICE v2.x: [see the differences from preCICE v1.x](couple-your-code-porting-adapters.html)." %}

TODO: adapter vs adapted code
