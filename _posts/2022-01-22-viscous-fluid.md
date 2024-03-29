---
layout: post
title:  "Notes on Viscous Term in Navier-Stokes' Equation"
subtitle: "First-Time Learner Version"
date:   2022-01-22 12:40:00
blurb: Study notes on viscous fluid. A close analysis of the viscous tensor and strain tensor. First-time, newbee version.
og_image: /assets/img/content/post-example/Banner.jpg
---


<img src="{{ "/assets/img/content/post-example/fluid.jpg" | absolute_url }}" alt="bay" class="post-pic"/>
<div class="post-caption">
  <p>Image from <a href= "https://www.nottingham.ac.uk/mathematics/research/fluid-mechanics.aspx"> Nottingham Math Department</a>.</p>
</div>

<br />
<br />

### Navier Stokes Equation and Viscous Tensor
<br />

#### TL;DR: A hand-wavy treatment of viscous term in N-S Equation. Refer to my future notes for a more rigorous one.

Let's consider the famous Navier Stokes' Equation:

$$
\begin{equation}
\frac{D (\rho \vec{\pmb{v}})}{D t} = -\vec{\nabla} \cdot \overrightarrow{\bf{\mathrm{P}}}+ (\vec{\nabla}\cdot \pmb{\tau})^\mathrm{T} +\rho \vec{\pmb{f}}_{\mathrm{other}},
\end{equation}
$$

where $$\frac{D}{Dt}$$ is the total time derivative, $$ \rho$$ is the density of fluid, $$\vec{P}$$ is the pressure, and $$\vec{f}$$ is some other forces on the fluid. $$\cdot$$ denotes inner product.

Here, for Cartesian coordinate $$(x,y,z) \in \reals^3$$, 

$$
\begin{aligned}
\pmb{\tau} =
   \begin{bmatrix}
       \tau_{xx} & \tau_{xy} & \tau_{xz}\\
      \tau_{yx} & \tau_{yy} & \tau_{yz}\\
      \tau_{zx} & \tau_{zy} & \tau_{zz}
\end{bmatrix}
\end{aligned} $$

is a viscous tensor of rank two. 

The reason we use a tensor to express forces is due to the fact each face of a fluid parcel suffers forces from left/right (along x-axis), front/back (along y-axis), and up/down (along z-axis). <ins>**THIS IS AN IMPORTANT FACT.**</ins>

The *first letter* in the subscript of $$ \pmb{\tau}$$ denotes the **normal direction** of the face, while the *later* one denotes the **direction the force is pointing**. This is demonstrated in the following diagram[^1].

<img src="{{ "/assets/img/content/viscous-fluid/tau_tensor.jpg" | absolute_url }}" alt="bay" class="content-pic"/>
<div class="fig-caption">
  <p>Figure 1. Free body diagram of an infinitestimal fluid parcel. Image from <i>Viscous FLuid</i> by Frank White.</p>
</div>
<br />
### Viscous Tensor as Forces per Unit Area

To see that $$(\vec{\nabla}\cdot \pmb{\tau})^\mathrm{T}$$ gives us the correct discription of viscous forces per unit volum $$\overrightarrow{\mathrm{\bf{f}}}_{\mathrm{viscous}}$$ on the fluid parcel, we consider, without loss of generality, component of this force in the x direciton. 

It is not hard to see from Fig. 1 that the force in the x direction on the rightmost face is just the sum of each $$\tau_{ix}$$ that points to the right multiplied by the area of that face

$$
\begin{equation*}
\mathrm{F_x^{right}} = \tau_{xx}(x+dx) dy dz + \tau_{yx}(y+dy) dx dz + \tau_{zx}(z+dz) dy dx
\end{equation*}
$$

Hence, we can get the net viscous force by subtrating forces on the leftmost faces and the rightmost as

$$
\begin{align}
\mathrm{F_x^{net}} &= \mathrm{F_x^{right}} - \mathrm{F_x^{left}} \\ &= \frac{d \tau_{xx}(x)}{dx} dx dy dz + \frac{d\tau_{yx}(y)}{dy} dy dx dz + \frac{d \tau_{zx}(z)} {dz} dz dy dx
\end{align}
$$

Hence we have the x-component viscous force per unit volume $$\mathrm{V_{par}}$$ on the fluid parcel as

$$
\begin{align}
f_x &= \frac{\mathrm{F_x^{net}}}{\mathrm{V_{par}}} \\ &= \frac{d \tau_{xx}}{dx} + \frac{d\tau_{yx}}{dy} + \frac{d \tau_{zx}}{dz} 
\end{align}
$$

Similarly, we have force per unit density $$\bf{\vec{f}}$$ as

$$
\begin{align}
\bf{\vec{f}} &= 
   \begin{bmatrix}
        f_x \\
        f_y \\
        f_z 
   \end{bmatrix} \\

   &=\begin{bmatrix}
        \frac{d \tau_{xx}}{dx} + \frac{d\tau_{yx}}{dy} + \frac{d \tau_ {zx}}{dz} \\
        \frac{d \tau_{xy}}{dx} + \frac{d\tau_{yy}}{dy} + \frac{d \tau_{zy}}{dz}\\
        \frac{d \tau_{xz}}{dx} + \frac{d\tau_{yz}}{dy} + \frac{d \tau_{zz}}{dz}
\end{bmatrix} \\
&=\Biggr( \begin{bmatrix}
        \frac{d}{dx} &
        \frac{d}{dy}  &
        \frac{d}{dz}  
   \end{bmatrix} 

\begin{bmatrix}
        \tau_{xx} & \tau_{xy} & \tau_{xz}\\
        \tau_{yx} & \tau_{yy} & \tau_{yz} \\
        \tau_{zx} & \tau_{zy} & \tau_{zz}
   \end{bmatrix}\Biggr)^\mathrm{T} \\
&= (\vec{\nabla}^\mathrm{T} \pmb{\tau})^\mathrm{T} = (\vec{\nabla} \cdot \pmb{\tau})^\mathrm{T} 

\end{align} 
$$

Great! I think at this point it is clear that why we use a tensor to express the viscous force.
<br/>

### Viscous Tensor is Symmetric

The reasoning behind is that we dont want the fluid parcel to rotate. This is a physical assumption, right 😅? If you think about water we drink is a giant cloud of rotating cubes, that would be really weird. 

Expressing this fact in physical term, we need the net angular momentum $$\vec{\mathrm{T}}_\mathrm{par}$$ of the fluid parcel to be $$0$$.  

We have by looking at Figure 1 again 

$$
\begin{aligned}
\vec{\mathrm{T}}_\mathrm{par} &= 
   \begin{bmatrix}
        \mathrm{T}_x \\
        \mathrm{T}_y \\
        \mathrm{T}_z 
   \end{bmatrix} \\ 

   &=\begin{bmatrix}
        \tau_{zy}- \tau_{yz} \\
        \tau_{xz}- \tau_{zx}\\
        \tau_{xy}- \tau_{yx}
\end{bmatrix} \\
&= 0
\end{aligned} 
$$

Hence, we proved that tensor is symmetric since $$\tau_{ij}= \tau_{ji}$$.

### The Final N-S Equation

<img src="{{ "/assets/img/content/viscous-fluid/viscous_strain.jpg" | absolute_url }}" alt="viscous_strain" class="content-pic"/>
<div class="fig-caption">
  <p>Figure 2. A plot of stress versus speed change with height change in a fluid parcel determined by experiment.</p>
</div>

Here we consider only Newtonian fluid ($$\mu$$ is scalar constant). For some other fluid, which thermal effect comes into play, you can refer to the full treatment given in the fluid mechanics notes by Dr. Joseph M. Powers at University of Notre Dame[^2].

We see from Fig. 2 that we have the following equality:

$$
\begin{equation}
\mu = \frac{\tau_{yx}}{\frac{\partial v_x}{\partial y}}
\end{equation}
$$

I will update the plot later, but here 2 means y and 1 means x. It is not hard to see that without loss of generality that

$$
\begin{align}
\mu = \frac{\tau_{ji}}{\frac{\partial v_i}{\partial x_j}}
\end{align}
$$

assuming an isotropic fluid, i.e. $$\mu$$ is the same for each face.

In a more compact notation, we write Eq. 11 as

$$
\begin{align}
\mu
\begin{bmatrix}
        \frac{\partial v_x}{\partial x} & \frac{\partial v_y}{\partial x} & \frac{\partial v_z}{\partial x}\\

       \frac{\partial v_x}{\partial y} & \frac{\partial v_y}{\partial y} & \frac{\partial v_z}{\partial y} \\

        \frac{\partial v_x}{\partial z} & \frac{\partial v_y}{\partial z} & \frac{\partial v_z}{\partial z}
   \end{bmatrix} 
   &=  \begin{bmatrix}
        \tau_{xx} & \tau_{xy} & \tau_{xz}\\
        \tau_{yx} & \tau_{yy} & \tau_{yz} \\
        \tau_{zx} & \tau_{zy} & \tau_{zz}
   \end{bmatrix} \\

   \mu  \begin{bmatrix}
        \mathrm{\partial}_x \\
        \mathrm{\partial}_y \\
        \mathrm{\partial}_z 
   \end{bmatrix} 
   \begin{bmatrix}
        v_x &
        v_y &
        v_z 
   \end{bmatrix}
   &= \pmb{\tau} \\
   \mu\vec{\nabla}(\vec{\pmb{v}}^\mathrm{T}) &= \pmb{\tau}
\end{align}
$$


Plug Eq. 15 in to the Eq. 10, we get

$$ 
\begin{align}
\vec{\nabla} \cdot \pmb{\tau} &= \mu\vec{\nabla} \cdot (\vec{\nabla}(\vec{\pmb{v}}^\mathrm{T})) \\
& = \mu
    \begin{bmatrix}
        \mathrm{\partial}_x &
        \mathrm{\partial}_y &
        \mathrm{\partial}_z 
   \end{bmatrix} 

 \begin{bmatrix}
        \frac{\partial v_x}{\partial x} & \frac{\partial v_y}{\partial x} & \frac{\partial v_z}{\partial x}\\

       \frac{\partial v_x}{\partial y} & \frac{\partial v_y}{\partial y} & \frac{\partial v_z}{\partial y} \\

        \frac{\partial v_x}{\partial z} & \frac{\partial v_y}{\partial z} & \frac{\partial v_z}{\partial z}
   \end{bmatrix}  \\
  &=  \mu \begin{bmatrix}
        \small{\frac{\partial^2 v_x}{\partial x^2}+\frac{\partial^2 v_x}{ \partial y^2}+\frac{\partial^2 v_x}{\partial z^2}} 

        & \small{\frac{\partial^2 v_y}{\partial x^2}+\frac{\partial^2 v_y}{\partial y^2}+\frac{\partial^2 v_y}{\partial z^2}} 
        
        &\small{\frac{\partial^2 v_z}{\partial x^2}+\frac{\partial^2 v_z}{\partial y^2}+\frac{\partial^2 v_z}{\partial z^2}}
   \end{bmatrix} \\
   & = \mu\nabla^2\vec{\pmb{v}}^\mathrm{T}

\end{align}
$$

We hence obtained the usual Navier Stokes Equation (from Eq. 1)

$$
\begin{equation}
\frac{D (\rho \vec{\pmb{v}})}{D t} = -\vec{\nabla} \cdot \overrightarrow{\bf{\mathrm{P}}}+ \mu\nabla^2\vec{\pmb{v}}^\mathrm{T} +\rho \vec{\pmb{f}},
\end{equation}
$$

and the transpose sign is just to get the row upright into a column, vector form.
<br/>

##### REFERENCE

[^1]: *Viscous Fluid* by Frank White
[^2]: *LECTURE NOTES ON INTERMEDIATE FLUID MECHANICS* by Joseph M. Powers.