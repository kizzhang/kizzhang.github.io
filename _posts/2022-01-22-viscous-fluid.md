---
layout: post
title:  "Notes on Viscous Term in Navier-Stokes' Equation"
date:   2022-01-22 12:40:00
blurb: Study notes on viscous fluid. A close analysis of the viscous tensor and strain tensor.
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
Let's consider the famous Navier Stokes' Equation:

\begin{equation}
\frac{D (\rho \vec{u})}{D t} = -\vec{\nabla} \cdot \vec{P}+\vec{\nabla}\cdot \pmb{\tau}+\rho \vec{f},
\end{equation}

where $$\frac{D}{Dt}$$ is the total time derivative, $$ \rho$$ is the density of fluid, $$\vec{P}$$ is the pressure, and $$\vec{f}$$ is some other forces on the fluid. Here, for Cartesian coordinate $$(x,y,z) \in \reals^3$$, 

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

The tensor property is due to the fact each face of a fluid parcel suffers forces from left/right (along x-axis), front/back (along y-axis), and up/down (along z-axis). <ins>**THIS IS AN IMPORTANT FACT.**</ins>

The *first letter* denotes the **normal direction** of the face, while the *later* one denotes the **direction the force is pointing**. This is demonstrated in the following diagram.

<img src="{{ "/assets/img/content/viscous-fluid/tau_tensor.jpg" | absolute_url }}" alt="bay" class="content-pic"/>
<div class="fig-caption">
  <p>Figure 1. Free body diagram of an infinitestimal fluid parcel. Image from <i>Viscous FLuid</i> by Frank White.</p>
</div>
<br />
### Viscous Tensor as Forces per Unit Area

To see that $$\vec{\nabla}\cdot \pmb{\tau}$$ gives us the correct discription of viscous forces per unit volum $$\overrightarrow{\mathrm{\bf{f}}}_{\mathrm{viscous}}$$ on the fluid parcel, we consider, without loss of generality, component of this force in the x direciton. 

It is not hard to see from Fig. 1 that the force in the x direction on the rightmost face is just the sum of each $$\tau_{ix}$$ that points to the right multiplied by the area of that face

\begin{equation}
\mathrm{F_x^{right}} = \tau_{xx}(x+dx) dy dz + \tau_{yx}(y+dy) dx dz + \tau_{zx}(z+dz) dy dx
\end{equation}

Hence, we can get the net force by subtrating forces on the leftmost faces and the rightmost as

$$
\begin{align}
\mathrm{F_x^{net}} &= \mathrm{F_x^{right}} - \mathrm{F_x^{left}} \\ &= \frac{d \tau_{xx}(x)}{dx} dx dy dz + \frac{\tau_{yx}(y)}{dy} dy dx dz + \frac{d \tau_{zx}(z)} {dz} dz dy dx
\end{align}
$$

Hence we have the x-component force per unit volume $$\mathrm{V_{par}}$$ on the fluid parcel as

$$
\begin{align}
f_x &= \frac{\mathrm{F_x^{net}}}{\mathrm{V_{par}}} \\ &= \frac{d \tau_{xx}}{dx} + \frac{d\tau_{yx}}{dy} + \frac{d \tau_{zx}}{dz} 
\end{align}
$$

Similarly, we have force per unit density $$\bf{\vec{f}}$$ as

$$
\begin{aligned}
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
&= \begin{bmatrix}
        \frac{d}{dx} &
        \frac{d}{dy}  &
        \frac{d}{dz}  
   \end{bmatrix} 

\begin{bmatrix}
        \tau_{xx} & \tau_{xy} & \tau_{xz}\\
        \tau_{yx} & \tau_{yy} & \tau_{yz} \\
        \tau_{zx} & \tau_{zy} & \tau_{zz}
   \end{bmatrix} \\
&= \vec{\nabla} \cdot \pmb{\tau}

\end{aligned} 
$$

Great! I think at this point it is clear that why we use a tensor to express the viscous force.
<br/>

### Viscous Tensor is Symmetric

The reasoning behind is that we dont want the fluid parcel to rotate. This is a physical assumption, right? If you think about water we drink is a giant cloud of rotating cubes, that would be really weird. 

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

### Viscous Tensor and Strain Tensor

We know that strain tensor $$\pmb{\epsilon}=\epsilon_{ij} $$ expresses the deformation of the fluid parcel.



<br/>

##### FOOTNOTES

[^1]: This is a note!
