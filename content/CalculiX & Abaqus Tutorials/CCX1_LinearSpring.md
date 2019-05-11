---
title: "Single Linear Spring"
date: 2019-04-18T20:39:46-05:00
---
### Problem Statement

Find the change in length of a spring that is \\(1.25m\\) under a concentrated force of \\(25N\\). The spring stiffness can be taken as \\(12.5 \frac{N}{m}\\).
The spring is shown in the figure below.

<center><img src="/CalculiX & Abaqus Tutorials/images/ccx1_LinearSpring_image.svg" style="max-width:100%;min-width:40px;float:middle;"/></center>

### Solution
Let's try to calculate the displacement of the spring using hand calculations. The force needed in node 2 to extend the spring with original length \\(L_0\\) to a final length \\(L\\) is given by $$F=k(L_0 -L)n$$ where \\(k\\) is the spring stiffness and \\(\boldsymbol{n}\\) is a unit vector pointing from node 1 to node 2. Since the force acts in the axial direction of the spring the above formula can be simplified as

$$F=k\Delta x$$

And we can solve for the displacement as shown below

$$25N=12.5 \frac{N}{m} \Delta x$$
$$ \Delta x = 2m$$

The input file for solving the above problem is shown below which is followed by the finite element results.

<pre>
**
** Structure: spring.
** Test objective: static calculation of a linear spring.
**
** Node Definition
** ---------------
*NODE,NSET=NALL
1,0.00, 0.0, 0.0
2,1.25, 0.0, 0.0
** Element Definition
** ------------------
*ELEMENT,TYPE=SPRINGA,ELSET=EALL
1,1,2
** Element stiffness
** -----------------
*SPRING,ELSET=EALL
12.5
** Boundary Conditions
** -------------------
*BOUNDARY
1,1,3
2,2,3
** Start Step
** ----------
*STEP
*STATIC
** Apply concentrated load
** -----------------------
*CLOAD
2,1,25.0
** Request results
* ----------------
*NODE PRINT,NSET=NALL
U
*NODE FILE
U
*EL FILE
S
** End Step
** ----------
*END STEP
</pre>

The finite element results are shown below

ccx1_LinearSpring_image_RESULTS.png
<center><img src="/CalculiX & Abaqus Tutorials/images/ccx1_LinearSpring_image_RESULTS.png" style="max-width:100%;min-width:40px;float:middle;"/></center>
