Some notes and references regarding the study of elastic plates with FvK equations:

Derivation from [Landau&Lifshitz Vol7](Landau_Lifshitz_Vol7_Elasticity.pdf) - 14. Large deflection on plates

Wikipedia articles:
[FvK equations:](https://en.wikipedia.org/wiki/F%C3%B6ppl%E2%80%93von_K%C3%A1rm%C3%A1n_equations)
[Bending of pla](https://en.wikipedia.org/wiki/Bending_of_plates)
[Plate theory](https://en.wikipedia.org/wiki/Plate_theory)

Check some of these papers...
[[ciarletta-et-al-the-föppl-von-kármán-equations-of-elastic-plates-with-initial-stress.pdf]]

How Matthias group used these equations in a recent problem:
[[Swelling-induced_patterning_soft-microchannels.pdf]]

Check Aidan's thesis: [[Aidan_Retallick_thesis.pdf]]

Check write-up from Rupinder work: [[precompiled-writeup.pdf]]

Check several interesting papers on wrinkles, crumples, draping, buckling, et al.
[[Wrinkles]]


## Nondimensional form

We start with the dimensional FvK equations:

$$ 
\frac{Eh^3}{12(1-\nu^2)}\nabla^4w - h\frac{\partial}{\partial x_\beta}\bigg(\sigma_{\alpha\beta}\frac{\partial w}{\partial x_\alpha}\bigg) = P\ ,
$$
^eq1

$$
\frac{\partial \sigma_{\alpha\beta}}{\partial x_\beta} = 0 \ .
$$
^eq2


Equation [[#^eq1]] can be derived from kinematics assumptions and constitutive relations for the elastic plate (cf. [Landau&Lifshitz](Landau_Lifshitz_Vol7_Elasticity.pdf)) while equations in [[#^eq2]] (note $\alpha$ and $\beta$ takes values 1 and 2) correspond with the momentum conservation law.

	Be aware: No assumption on constitutive relation model such as neo-Hookean makes sense here! Note that these equations are precisely the ones that tell us how is the relation between deformation and stress in elastic plates subject to large (non-linear) deformations.

We can now rewrite equation [[#^eq1]] in terms of nondimensional variables,

$$
x = \hat{x}\ l_0\ , \quad w = \hat{w}\ l_0\ , \quad \sigma = \hat{\sigma}\ \sigma_0 \ ,
$$

being $l_0$ a characteristic length, and $\sigma_0$, some characteristic stress (in a dimensional sense). For an elastic plate of radius $R$ and Young modulus $E$ we can choose $l_0 = R$ and $\sigma_0 = E$, as characteristic dimensional variables. 

On the other hand, we are going to consider an elastic plate horizontally placed in a gravitational field, so the pressure will be simply $P=\rho g h$, with $\rho$ the homogeneous density, $g$ the acceleration of the gravity field and $h$ the thickness of the plate.

Applying the above considerations,

$$
\frac{E(h/R)^3}{12(1-\nu^2)}\widehat{\nabla}^4\hat{w} - \frac{Eh}{R}\frac{\partial}{\partial \hat{x}_{\beta}}\bigg(\hat{\sigma}_{\alpha\beta}\frac{\partial\hat{w}}{\partial\hat{x}_\alpha}\bigg) = \rho g h \ ,
$$
which can be simplified to,
$$
\widehat{\nabla}^4
\hat{w} - \eta\frac{\partial}{\partial \hat{x}_{\beta}}\bigg(\hat{\sigma}_{\alpha\beta}\frac{\partial\hat{w}}{\partial\hat{x}_\alpha}\bigg) = \frac{\rho g R}{E}\eta \ ,
$$
^eq-nondim

with the nondimensional parameter $\eta$ defined as,

$$
\eta = \bigg[\frac{(h/R)^2}{12(1-\nu^2)}\bigg]^{-1} \ .
$$

Equation will be great if we had only $\eta$ as control parameter, however the quotient $\rho g R/E$ arise due to the nondimensional choice. Computationally, this is not going to be problematic, but in terms of extrapolate results from a experimental point of view it would be easier if we could just control system dimensions with $\eta$. 

>Typically, one will have membranes with $E$ and $\rho$ known, and $h$ can be simply fixed. Note that $R$ should not be understood as a *control parameter*, as it changes the physical (and numerical) domain. Experimentally, it is always possible to use disks with different sizes and analyse the effect of $R$ on the steady solution, but we would be actually doing different experiments. We normally use geometrical constants to non-dimensionalise a system. Control parameters should are the nondimensional quantities that arise in the final non-dimensional form of the equations.

Another option will be using a characteristic radius $R_0$ to non-dimensionalise lengths such that $\rho g R_0/E = 1$, this way:

$$
\widehat{\nabla}^4
\hat{w} - \eta\frac{\partial}{\partial \hat{x}_{\beta}}\bigg(\hat{\sigma}_{\alpha\beta}\frac{\partial\hat{w}}{\partial\hat{x}_\alpha}\bigg) = \eta \ , 
$$ 

where $\eta$ is now defined as,

$$
\quad \eta = 12(1-\nu^2)\bigg(\frac{R_0}{h}\bigg)^2, \quad R_0 = E/(\rho g)\ .
$$

Alternatively, we can relate the radius of the disk and the characteristic length by a factor $\lambda \in \mathbb{R}^+$ which we can in principle vary continuously to try different geometries.

Then we write,

$$
\quad \eta = 12(1-\nu^2)\bigg(\frac{R}{\lambda h}\bigg)^2,
$$

^eta-lambda

where $\lambda$ is the *non-dimensional radius* that we choose for our simulations. We could then numerically compute $\hat{\omega}_\lambda$ (not unique, as we have multi-stability...) for each value of $\eta$, which would be the continuation parameter once we have fixed the $\lambda$ (geometry of the system). Then, given $\lambda$, it would be possible to reproduce the numerical results experimentally, just using the appropriate physical quantities in 

## Experimental data and first simulations
Some numbers to see which orders of magnitud should we expect in the non-dimensional parameters. Following Draga's observations:

- Size (square side):
	$L_{exp} = 2R_{exp} = 14 \ {\rm cm}$ --> [U-shape](ushape.jpeg)
	$L_{exp}= 2R_{exp} = 20 \ {\rm cm}$ --> draping [(3-mode)](triangle.jpeg)
	$h_{exp} = 0.8 \ \rm{mm}$
- Material:
	$\nu = 0.5$
	$E = 1.44 \ \rm{MPa}$
	$\rho = 900 \ {\rm kg/m^3}$
- Physical constants:
	$g = 9.8 \ {\rm m/s^2}$ 

### First attempt - $R_0$
Using this values we get $R_0 = 1.63 \cdot 10^{2} \ {\rm m}$ which is too big compared with $R_{exp} = 10^{-1} {\rm m}$ to be considered as a characteristic. Nondimensionalising lengths with $R_0$ leads to a system with high values of $\eta$ in equation [[#^eq-ndim2]] 
$$ 
\eta = 3.75 \cdot 10^{11}
$$
and Newton method gets hard to converge. Note that the non-dimensional radius is $\lambda = 6.13 \cdot 10^{-4}$, so $R_0$ doesn't seem to be a good mesure for the system length.

**Second attempt - $R$**
So we go back to the first non-dimensional equation [[#^eq-nondim]] and try to do some simulations using parameters with more physical sense. Now the system is governed by two non-dimensional parameters:
$$ 
\eta = 12(1-\nu^2)\bigg(\frac{R}{h}\bigg)^2 \ , \ \gamma = \frac{\rho g R}{E},
$$
using the experimental data above for the (expected) draping case ($R_{exp}=10 {\rm cm}$)
$$ 
\boxed{\eta = 1.41 \cdot {10^5} \ , \ \gamma = 6.13 \cdot 10^{-4}}
$$
 so the non-dimensional pressure, RHS of equation [[#^eq-nondim]], will be
 $$
\boxed{\hat{P} = \gamma \ \eta = 86.23}
$$
 apparently easier to deal with numerically than the value of $\eta$ obtained with $R_0$ as characteristic length.
 
 Anyway, the numerical method does not converge directly, (note that $\eta$ appears also on the LHS) so we need to start with a lower value of $\eta$ which is expected to be our continuation parameter, and then increase it gradually until reaching the experimental value. For this purpose, we start with $\eta_0 = 1.41 \cdot 10 ^{3}$, which could be interpreted as increasing the experimental thickness one order of magnitud, so $h = 8 \ {\rm mm}$.

We increment $\eta$  in the following manner:
$$
\eta = \eta + \eta_{\rm inc} \ ,
$$
with
$$
\eta_{\rm inc} = \alpha \ \eta_0.
$$

Let's see some numerical results obtained with these parameters:

1. Comparing two simulations where $\eta$ has been incremented using different factors, $\alpha_1 = 10$ and $\alpha_2 = 1$, starting from $\eta_0 = 1.41 \cdot 10^3$ until reaching $\eta = 1.55 \cdot 10^{4}$ 

Separate animations:
$\alpha_1 = 10$
```
paraview RunTest_circle_ea05_RHS_Eta_if10/Case_straight_rotated_coords_no_t_shape_fvk_free/RESLT/soln.pvd
```
> Note: using finer mesh (element_area = 0.25) is not possible to converge this same solution. Requieres finer step...

$\alpha_2 = 1$
```
paraview RunTest_circle_ea05_RHS_Eta_if1/Case_straight_rotated_coords_no_t_shape_fvk_free/RESLT/soln.pvd
```

Comparing same $\eta$
```
paraview RunTest_circle_ea05_RHS_Eta_if10/Case_straight_rotated_coords_no_t_shape_fvk_free/RESLT/soln1.vtu RunTest_circle_ea05_RHS_Eta_if1/Case_straight_rotated_coords_no_t_shape_fvk_free/RESLT/soln10.vtu 
```

2. Comparing two simulations using different dimensional radius and same $h = 8 {\rm mm}$
$R_1 = 0.1 {\rm m}; \ \eta_0 = 1.41 \cdot 10^{3}; \ \gamma = 6.13 \cdot 10^{-4}$  
$R_2 = 0.2 {\rm m}; \ \eta_0 = 5.63 \cdot 10^{3}; \ \gamma = 1.23 \cdot 10^{-3}$
using different increments (same $\alpha$, but $\eta_0$ is different) until reaching $\eta = 2.25 \cdot 10^5$ 

```
paraview RunTest_circle_ea05_RHS_Eta_if1/Case_straight_rotated_coords_no_t_shape_fvk_free/RESLT/soln15.vtu RunTest_circle_ea05_RHS_Eta_if1_R02/Case_straight_rotated_coords_no_t_shape_fvk_free/RESLT/soln3.vtu
```

 >Note: we would be comparing two solutions with the same value of $\eta = 2.25 \cdot 10^{4}$ but different $\hat{P}$ due to the different value of $\gamma$. The idea is that we would have different curves $\hat{\omega}_\gamma(\eta)$ for each $\gamma$ (similar to $\lambda$ in [[#^eta-lambda]]).
 
__________________________
>Note: previous results make reference to files that are now probably at home directory - take a look. Anyway, maybe not that relevant...
____________________

## Curviline internal boundary - (Non reliable)
We have seen numerically that the system collapses into draped geometry (mode-6?) or U-shape, depending on: the pressure step, the number of elements of the mesh. Let's see some examples and main results.
#### Simulation 1: coarse mesh
- Parameters:
	$\eta = 1.41 \cdot 10^5, \ p_{\rm inc} = 1$
- Mesh:
	Element_area = 0.5, n_segment = 4 [view](eta141e5_pinc1_ea05_ns4_mesh.png)
	
The systems drapes with N=6, after few steps ($P_{\rm mag} = 3$)  [view](eta141e5_pinc1_ea05_ns4_N6.png)
```
paraview paraview_sesions/eta141e5_pinc1_ea05_ns4.pvsm
```
*Output file:*
```
grep P_mag RESLT_egh/Run_ea05_nseg4_Eta_141e5_pinc1_Pend/Case_straight_rotated_coords_no_t_shape_fvk_free/OUTPUT 
```

**Note:** see what happens if we use the more accurate parameter $\eta = 140625$. Now the Newton method breaks after two steps ($P_{\rm mag} = 2$), on an axisymmetric solution [view](eta140625_pinc1_ea05_ns4_axi.png)
```
paraview paraview_sesions/eta140625_pinc1_ea05_ns4.pvsm
```
*Output file:*
```
grep P_mag RESLT_egh/Run_ea05_nseg4_Eta_140625_pinc1/Case_straight_rotated_coords_no_t_shape_fvk_free/OUTPUT
```
Try with a smaller step

#### Simulation 2: finer mesh
- Parameters:
	$\eta = 1.41 \cdot 10^5, \ p_{\rm inc} = 1$
- Mesh:
	Element_area = 0.05, n_segment = 4 [view](eta141e5_pinc1_ea005_ns4_mesh.png)

The system drapes with N=11 when reaching $P_{\rm mag} = 12$ [view](eta141e5_pinc1_ea005_ns4_N11.png)
```
paraview paraview_sesions/eta141e5_pinc1_ea005_ns4.pvsm
```
*Output file*
```
grep P_mag RESLT_egh/Run_ea005_nseg4_Eta_141e5_pinc1_Pend/Case_straight_rotated_coords_no_t_shape_fvk_free/OUTPUT
```

#### Simulation 3: even finer mesh 
- Parameters:
	$\eta = 1.41 \cdot 10^5, \ p_{\rm inc} = 1$ 
- Mesh:
	Element_area = 0.005, n_segment = 4 [view](eta141e5_pinc1_ea0005_ns4_mesh.png)

The system drapes with N=10 for $P_{\rm mag} = 9$ [view](eta141e5_pinc1_ea0005_ns4_N11.png) | Note: N=10 --> N=5 ??
```
paraview paraview_sesions/eta141e5_pinc1_ea0005_ns4.pvsm
```
*Output file*
```
grep P_mag RESLT_egh/Run_ea0005_nseg4_Eta_141e5_pinc1_Pend/Case_straight_rotated_coords_no_t_shape_fvk_free/OUTPUT
```

#### Comparison with axisymmetric solutions
Let's see if the 2D solutions agree with the axisymmetric ones.  

We calculate the displacement along $N_{\varphi} = 105$ radial lines, each of them with $N_r = 50$ points, leading to the following decomposition:
$$
w(r_j,\varphi_i) = \bar{w}(r_j) + \tilde{w}(r_j,\varphi_i), \quad (i = 1\dots N_r, \ j=1\dots N_{\varphi})
$$
^eq-axi-pert

where the axisymmetric part is:
$$
\bar{w}(r_j) = \sum_{i}^{N_\varphi}w(r_j,\varphi_i),
$$

and so we simply get the perturbation along each line as
$$
\tilde{w}(r_j,\varphi_i) = w(r_j,\varphi_i) - \bar{w}(r_j). 
$$
##### Mesh convergence
Now we plot $\bar{w}(r)$ at $P_{\rm mag} = 2$, (just before coarse mesh drapes to N=6) for the three meshes shown above, and compare it with the axisymmetric solution: [view](axi_compare_p2_eta141e5.png)

*gnuplot:* (into julia_projects/report)
```
plot "axi_sol_P2.000_Eta1.410e+05.dat" u 2:9 title "axi solution" w l, "average_eta141e5_p2_ea05.dat" u 1:5 every ::1::50 title "average ea05" w l, "average_eta141e5_p2_ea005.dat" u 1:5 every ::1::50 title "average ea005" w l, "average_eta141e5_p2_ea0005.dat" u 1:5 every ::1::50 title "average ea0005" w l
```

##### Linear stability
Now we can take a look in more detail, analysing the buckling pressure of the three modes shown above (N=6, 11, 10) according to the axisymmetric results.

- These are the buckling pressures expected for modes N=4-15 [view](critical_pressure_N4-15.png)
	$N=6; \ P^{(6)}_{\rm axi} = 32.90$
	$N=11; \ P^{(11)}_{\rm axi} = 56.69$
	$N=10; \ P^{(10)}_{\rm axi} = 49.70$

Let's plot the three [solutions](critical_sols_N6-11-10.png) and their respective [eigenfunctions](critical_eigenfuns_N6-11-10.png). We can also plot it on [paraview](axi_critic_sols_N6-11-10.png):
```
paraview paraview_sesions/axi_critic_sols_N6_11_10.pvsm
```

We can also take a look to the predicted axisymmetric critical solution, and compare it with the 2D-solution. For $N=6; \ P^{(6)}_{\rm axi} = 32.90$ and coarse mesh:
```
paraview paraview_sesions/eta141e5_pinc1_ea05_ns4_P32.90_axi.pvsm
```

##### Perturbations
Now we wonder if we can extract any information on how perturbations are developed by plotting $\tilde{w}(r,\varphi)$ from equation [[#^eq-axi-pert]]. We plot the perturbation just before and after the 2D-solution buckles:
###### 1. Coarse mesh
- Parameters:
	$\eta = 1.41 \cdot 10^5, \ P_{\rm mag} \in [2,3]$
- Mesh:
	Element_area = 0.5, n_segment = 4 [view](eta141e5_pinc1_ea05_ns4_mesh.png)

Is N=6 perturbation actually induced by mesh geometry? [view](eta141e5_pinc1_ea05_ns4_P3_axi.png)
```
paraview paraview_sesions/eta141e5_pinc1_ea05_ns4_P2-3_axi.pvsm
```

###### 2. Finer mesh 
- Parameters:
	$\eta = 1.41 \cdot 10^5, \ P_{\rm mag} \in [11,12]$
- Mesh:
	Element_area = 0.05, n_segment = 4 [view](eta141e5_pinc1_ea005_ns4_mesh.png)

Check: the perturbation happens to be rotated [view](eta141e5_pinc1_ea005_ns4_P11-12_axi.png)
```
paraview paraview_sesions/eta141e5_pinc1_ea005_ns4_P11-12_axi.pvsm
```

Doubt: `Rotate_coordinates_on_all_curvilinear_boundaries=true` line 236

###### 3. Even finer mesh 
- Parameters:
	$\eta = 1.41 \cdot 10^5, \ P_{\rm mag} \in [8,9]$
- Mesh:
	Element_area = 0.005, n_segment = 4 [view](eta141e5_pinc1_ea005_ns4_mesh.png)

Check: perturbation rotated again [view](eta141e5_pinc1_ea005_ns4_P8-9_axi.png)
```
paraview paraview_sesions/eta141e5_pinc1_ea0005_ns4_P8-9_axi.pvsm
```



#### Pitchfork bifurcation track
The most unstable mode predicted by the linear stability analysis happens to be the one with N=6. Let's see if we can force the 2D-solutions to drape into this shape, applying a pressure field of the form:

$$
P(r,\varphi) = P_{\rm mag} + P_{\cos} r^2 \cos(N\varphi),
$$
^eq-pressure-pitchfork
where $P_{\rm mag}$ and $P_{\cos}$ are two constants that we will change along the simulation in order to find the expected Pitchfork bifurcation.

> **Steps:** 1) Switch-on $P_{\cos}$ > 2) Increase $P_{\rm mag}$ until enough draped deformation > 3) Switch-off $P_{\cos}$ > 4) Decrease $P_{\rm mag}$ until reaching axisymmetric sol again

##### 1. Coarse mesh:
Element_area = 0.5, n_segment = 4 [view](eta141e5_pinc1_ea05_ns4_mesh.png)
$\eta = 1.41 \cdot 10^5$
Attempts:
1) $\ p_{\rm inc} = 1, \ P_{\cos} = 10$ 
	 Simulation stops after step 1

2) $\ p_{\rm inc} = 0.1, \ P_{\cos} = 10$ 
	Buckles to U-shape around $P_{\rm mag}=0.6$
```
paraview paraview_sesions/pitchfork_pcos10_pinc01_eta141e5_ea05_ns4.pvsm
```

##### 2. Finer mesh:
Element_area = 0.05, n_segment = 4 [view](eta141e5_pinc1_ea005_ns4_mesh.png)
$\eta = 1.41 \cdot 10^5$
Attempts:
1) $\ p_{\rm inc} = 0.1, \ P_{\cos} = 10$ 
	Again, buckles to U-shape around $P_{\rm mag}=0.6$
```
paraview paraview_sesions/pitchfork_pcos10_pinc01_eta141e5_ea005_ns4.pvsm
```
- Check: rotation??

2) $\ p_{\rm inc} = 1, \ P_{\cos} = 0.1$ 
	Newton method breaks after $P_{\rm mag}=7$
```
paraview paraview_sesions/pitchfork_pcos01_pinc1_eta141e5_ea005_ns4.pvsm
```
- This makes more sense: we start forcing a small (linear) N=6 perturbation and see how it develops

3) $\ p_{\rm inc} = 0.1, \ P_{\cos} = 0.1$ 

##### 3. Even finer mesh:
Element_area = 0.005, n_segment = 4 [view](eta141e5_pinc1_ea0005_ns4_mesh.png)
$\eta = 1.41 \cdot 10^5$
Attempts:
1) $\ p_{\rm inc} = 0.1, \ P_{\cos} = 10$  
	Same, it buckles to U-shape around $P_{\rm mag}=0.6$
```
paraview paraview_sesions/pitchfork_pcos10_pinc01_eta141e5_ea0005_ns4.pvsm
```


















#### Simulation 2.1: finer mesh (old mesh - N=5??) 
- Parameters:
	$\eta = 1.41 \cdot 10^5, \ p_{\rm inc} = 1$
- Mesh:
	Element_area = 0.05, n_segment = $\pi/\sqrt{\rm Element\_area}$ 

```
paraview paraview_sesions/eta141e5_pinc01_ea005_old_N5.pvsm
```

## New results - Polyline

Basically previous results where non reliable as we were using curviline for the internal boundaries (needed to determine central node and also max_x node where we suppress rotation)
> Note - Rotation: I'm still confused with this point. Presumably is necessary to suppress rotation to avoid degeneracy on solutions that seems to be problematic (seen in previous studies). Anyway, I'm still running simulations where the system happens to rotate. **Answer:** That's fine, it only means that another equivalent (rotated) solution was chosen for a different pressure, as we fixed plane displacements in max_x, we can only have one solution - But still, why this change?

1. Finest mesh: ea = 0.001
	- Base state with inner curviline or inner polyline is almost the same at low pressure (p=2)
	- Although, leads to different final state when increasing p_mag    
	- curviline-->  N=10 mode appears around p = 9    
	- polyline --> axisymmetric sol even at p=40	
	- Things to try: Pitchfork N=6 (basic solution quite similar to axi_sol)
    
2. Another mesh: ea = 0.05
	- curviline - N=11 mode appears at p = 12
	- polyline - Newton's method breaks just before reaching p=12 // but look at pert_sol - N=11 mode
	- compare curviline and polyline perturbation (also for ea=0.005) 
	- Pitchfork study (using polyline): N=6. Different results depending on p_inc:
	- p_cos = 0.1 // p_inc = 1-0.1 --> check: rotation?? (at step 14: p=6.8). Newton's method eventually breaks when decreasing p_mag (with p_cos = 0)
	- p_cos = 0.1 // p_inc = 0.1 --> look at pert_sol: N=6 --> N=5  (p=1.4 - 1.5)



### Write some draft with my results using...

https://squidfunk.github.io/mkdocs-material/

or better:

https://quartz.jzhao.xyz/

Look at some examples here:

https://turntrout.com/research

To translate to LaTeX use: https://pandoc.org/

