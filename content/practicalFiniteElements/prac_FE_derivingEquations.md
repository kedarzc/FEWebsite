---
title: Theory of Finite Elements
---
## Table of contents
1. [Derivation of the basic equation]({{< ref "prac_FE_derivingEquations.md#derivation-of-basic-equation" >}})
    1. [Fundamentals]({{< ref "prac_FE_derivingEquations.md#fundamentals" >}})
    2. [How to calculate stresses due to applied loads?]({{< ref "prac_FE_derivingEquations.md#how-to-calculate-stresses-due-to-applied-loads" >}})
    3. Dynamics and non-linear analysis

### Derivation of basic equation

#### Fundamentals
Let us consider a 3D body of volume V. It has an external surface S, with points on the body that are defined by co-ordinates `$x, y, z$`. A portion of he body `$S_{u}$` is constrained as shown below. A distributed force per unit area `$f_{s}$` acts on a portion of the boundary surface `$S_{fs}$`.

Let's assume that the body deforms under the action of this force. Then the deformation of any point in the body is given by the three components of it's displacement as

`$$\{{u}\} = \begin{bmatrix} u \\ v \\ w \end{bmatrix}$$`

where, `$u,v,w$` are displacements in the `$x,y,z$` directions.

A distributed force per unit volume `$f_{b}$` may act on the body. This is given by

`$$\{{f^{b}}\} = \begin{bmatrix} f_{x}^b \\ f_{y}^b \\ f_{z}^b \end{bmatrix}$$`

Examples of `$f^b\rightarrow$` gravity loads.

The surface loads is given by it's components as

 `$$\{{f^{s}}\} = \begin{bmatrix} f_{x}^s \\ f_{y}^s \\ f_{z}^s \end{bmatrix}$$`

Examples of `$f^s\rightarrow$` pressure loads, contact forces.

Point load `$f$` acting at a point `$i$` is given by

 `$$\{{f^{i}}\} = \begin{bmatrix} f_{x}^i \\ f_{y}^i \\ f_{z}^i \end{bmatrix}$$`

 The resulting stresses and strains are given by
 `$$\{{\sigma}\} = \begin{bmatrix} \sigma_{xx} \\ \sigma_{yy}  \\ \sigma_{zz}  \\ \tau_{xy} \\ \tau_{xz} \\ \tau_{yz} \end{bmatrix}$$`

 `$$\{{\epsilon}\} = \begin{bmatrix} \epsilon_{xx} \\ \epsilon_{yy}  \\ \epsilon_{zz}  \\ \gamma_{xy} \\ \gamma_{xz} \\ \gamma_{yz} \end{bmatrix}$$`

 We can relate the strains to displacement using

 `$$\{{\epsilon}\} = \begin{bmatrix} \frac{\delta u}{\delta x} \\ \frac{\delta v}{\delta x}  \\ \frac{\delta w}{\delta x}  
  \\ \frac{\delta v}{\delta x} + \frac{\delta u}{\delta y} \\ \frac{\delta v}{\delta x} + \frac{\delta u}{\delta z}  \\ \frac{\delta w}{\delta y} + \frac{\delta v}{\delta z} \end{bmatrix}$$`

Let's keep the material simply. Let us assume the material is linear elastic. Then, we can related the stress to strain as

`$$\sigma=\begin{bmatrix} D \end{bmatrix} \begin{bmatrix} \epsilon \end{bmatrix}$$`

#### How to calculate stresses due to applied loads

If you carefully look at equations above, you shall notice that if we can *somehow* calculate the displacements `$u,v,w$` then we can compute the strains. If we know the strains, then we can compute the resulting stresses using the material behavior defined by `$D$`.

So long story short, to get to the stresses, we need to compute the displacements due to the applied loads.

There are many different methods to get to the displacements. We will use the principle of *Minimum Potential Energy* here. It states that, as long as the system is stable, the total potential energy `$\Pi$` of that system is zero.

`$$\frac{\delta \Pi}{\delta U}= 0$$`

The total potential energy of a system is given by the sum of the strain energy and the sum of work done by external forces. Thus, `$\Pi = $` strain energy + external work

For a linear elastic body, the strain energy per unit volume is given by

`$$\pi_{s} = \frac{1}{2}\{\sigma\}^T \{\epsilon\}$$`

Thus total strain energy for the volume is

`$$\Pi_{s} = \frac{1}{2}\int_{V} \{\sigma\}^T \{\epsilon\} dV$$`

The total external work is the work done by all external forces as

`$$\Pi_w = - \int_{V} \{u\}^T \{f^b\} dV - \int_{S} \{u\}^T \{f^s\} dS - \Sigma_{i}\{U_{i}\}^T \{{f^i\} }$$`

Collecting everything, we can the expression for the total potential energy as,

`$$\Pi= \frac{1}{2}\{\sigma\}^T \{\epsilon\} dV - \int_{V} \{u\}^T \{f^b\} dV - \int_{S} \{u\}^T \{f^s\} dS - \Sigma_{i}\{U_{i}\}^T \{{f^i\} }$$`

In finite element analysis we divide the problem into a discrete parts that are represented by a number of finite elements. These elements are interconnected at nodes on the element boundaries. In the finite element approach the displacements measured within each element are assumed to be a function of the displacements of the nodes. Thus, the displacement within the element is related to the displacement of the nodes via an interpolation function known as a shape function. Thus the displacement can be further represented as

`$$\{ u \}_{e} = \begin{bmatrix} S \end{bmatrix}_{e} \{U\}_{nodal} $$`

where, `$\begin{bmatrix} S \end{bmatrix}_{elem}$` is the shape function matrix for the element, `$\{U\}_{nodal}$` is the nodal point displacement vector of the element. For clarity, the displacement within an element for an element with two nodes and four nodes is shown below.

For an element with two nodes `$i$` and `$j$` (Eg. Spring element)

`$$\{ u \}_{e} = \begin{bmatrix} S_{i} & S_{j} \end{bmatrix} \begin{Bmatrix} U_{i} \\ U_{j} \end{Bmatrix} $$`

For an element with 4 nodes `$i,j, k, l$`

`$$\{ u \}_{e} = \begin{bmatrix} S_{i} & S_{j} & S_{k} & S_{l} \end{bmatrix} \begin{Bmatrix} U_{i} \\ U_{j} \\ U_{k} \\ U_{l} \end{Bmatrix} $$`
