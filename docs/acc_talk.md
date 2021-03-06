<!-- .slide: data-background="#500000" class="dark" -->

# Adaptive Estimation of Unknown Inputs with Weakly Nonlinear Dynamics

## T. Griffith, V. Gehlot, M. Balas
#### ACC 2022

#### June 10, 2022

---

<section>
<h1> Adaptive Unknown Input Estimators </h1>
<h2> Estimator overview </h2>
<style>
.vertical-center {
  min-height: 100%;  /* Fallback for browsers do NOT support vh unit */
  min-height: 100vh; /* These two lines are counted as one :-)       */

  display: flex;
  align-items: center;
}

.container{
    display: flex;
}
.col{
    flex: 1;
}
</style>

<div class="container vertical-center">

<div class="col">

<ul style="font-size:1.5vw">
<li style="padding-bottom:0.9em">Three significant uncertainties</li>
<ul>
  <li style="padding-bottom:0.9em"> Input $u$ is unknown, external, deterministic</li>
  <li style="padding-bottom:0.9em"> State matrix $A$ may have uncertainty</li>
  <li style="padding-bottom:0.9em"> Known, Lipschitz nonlinear internal dynamics $g(x)$</li>
  </ul>
<li ><strong><em>Can we synthesize $u$ and correct $A$?</em></strong></li>
</ul> 
</div>



<div class="col">

\begin{aligned}
    \dot{x}&=Ax+g(x)+Bu\\\
    y&=Cx
\end{aligned}



</div>
</div>
</section>


<section>
<h1> Adaptive Unknown Input Estimators </h1>
<h2> Modeling unknown inputs </h2>
<style>
.vertical-center {
  min-height: 100%;  /* Fallback for browsers do NOT support vh unit */
  min-height: 100vh; /* These two lines are counted as one :-)       */

  display: flex;
  align-items: center;
}

.container{
    display: flex;
}
.col{
    flex: 1;
}
</style>

<div class="container vertical-center">

<div class="col">

<ul>
<li style="padding-bottom:0.9em">Approximate input space $\mathbb{U}$</li>
  <ul>
  <li style="padding-bottom:0.9em">$\hat{u}=\sum_{i=1}^{N} c_i f_i(t)$</li></ul>
<li style="padding-bottom:0.9em" style="padding-bottom:0.9em">Persistent Inputs</dt>
<ul>
  <li style="padding-bottom:0.9em">$\dot{z}_u=F_u z_u$</li>
  <li style="padding-bottom:0.9em">$\hat{u}=\Theta_u z_u$</li>
  <li style="padding-bottom:0.9em">$F_u = \begin{bmatrix} 0 & 1 & 0 \\\ -\omega^2 & 0 & 0 \\\ 0 & 0 & 0 \end{bmatrix}$</li>
  </ul>
</ul> 
</div>



<div class="col">

<figure>
  <img src="img/acc/uhat.gif" alt="Trulli" height="600">
</figure>


</div>
</div>

</section>

<section>
<h1> Adaptive Unknown Input Estimators </h1>
<h2> Architecture and estimator error </h2>
<style>
.vertical-center {
  min-height: 100%;  /* Fallback for browsers do NOT support vh unit */
  min-height: 100vh; /* These two lines are counted as one :-)       */

  display: flex;
  align-items: center;
}

.container{
    display: flex;
}
.col{
    flex: 1;
}
</style>

<div class="container vertical-center">

<div class="col">

<figure>
  <img src="img/acc/adapt_est_weak.png" alt="Trulli" height="600">
</figure>
</div>



<div class="col">

Recover $A$ with adaptive scheme
`$$ A \equiv A_m +B L_{*} C $$`
`$$ \dot{L} = -e_y y^* \gamma_e; \ \gamma_e > 0 $$`
<br>
Error dynamics

`$$ \dot{e}=(\bar{A}+\bar{K} \bar{C})e+\bar{B} \Delta L y +\varepsilon \Delta g $$`

`$$ \begin{bmatrix} \dot{e}_x \\\ \dot{e}_z \end{bmatrix} = \underbrace{\begin{bmatrix} A_m+K_x C & B \Theta_u \\\ K_u C & F \end{bmatrix}}_\text{$\bar{A}_c$} \begin{bmatrix} e_x \\\ e_z \end{bmatrix} +\begin{bmatrix} B \\\ 0 \end{bmatrix} w +\varepsilon\begin{bmatrix} g(\hat{x})-g(x) \\\ 0 \end{bmatrix}$$`



</div>



</section>

<section>
<h1> Adaptive Unknown Input Estimators </h1>
<h2> Architecture and estimator error </h2>
<style>
.vertical-center {
  min-height: 100%;  /* Fallback for browsers do NOT support vh unit */
  min-height: 100vh; /* These two lines are counted as one :-)       */

  display: flex;
  align-items: center;
}

.container{
    display: flex;
}
.col{
    flex: 1;
}
</style>

<div class="container vertical-center">

<div class="col">

 <ul>
  <li style="padding-bottom:0.5em">ASD plant dynamics</li>
<ul>
<li style="padding-bottom:0.5em">`$\bar{A}_c^* \bar{P} + \bar{P} \bar{A}_c = -\bar{Q}$`</li>
<li style="padding-bottom:0.5em">`$\bar{P}\bar{B}=\bar{C}^*$`</li>
</ul>
  <li style="padding-bottom:0.5em">$A$ Hurwitz</li>
  <li style="padding-bottom:0.5em">Bounded `$L_{*}$`</li>
  </ul>
</div>

<div class="col">
<ul>
 <li style="padding-bottom:0.5em">Error in state and input converges to zero
    <ul>
      <li style="padding-bottom:0.5em">`$V(e,\Delta L) = \frac{1}{2}e^*\bar{P}e+\frac{1}{2}\text{tr}(\Delta L \gamma_e^{-1} \Delta L^*)$`</li>
      <li style="padding-bottom:0.5em">`$\dot{V}(e, \Delta L)\leq -\Big(\underbrace{\frac{1}{2}\lambda_{\text{min}}(\bar{Q})-\varepsilon \mu\lambda_{\text{max}}(\bar{P})}_{\bar{\alpha}>0}\Big)||e||^2$`</li>
    </ul>
  </li>
</ul> 
<br>
<p> `\begin{align} 0<\varepsilon <\frac{\lambda_{\text{min}}(\bar{Q})}{2 \mu \lambda_{\text{max}}(\bar{P})}\Longleftrightarrow \bar{\alpha}>0. \end{align}`</p>



</div>





</section>

---


<!-- .slide: data-background="#ffffff" class="light" -->

<section>

<h1> Illustrative example</h1>
<style>
.vertical-center {
  min-height: 100%;  /* Fallback for browsers do NOT support vh unit */
  min-height: 100vh; /* These two lines are counted as one :-)       */

  display: flex;
  align-items: center;
}

.container{
    display: flex;
}
.col{
    flex: 1;
}
</style>

<div class="container vertical-center">

<div class="col">
\begin{align}
\dot{x}&=A_m x+\varepsilon g(x)+Bu\\\
&=\begin{bmatrix}
-4 &1 &2\\\
-1 & -1 & 1\\\
-1 & 1 &-1 
\end{bmatrix}x+ \sin(x)+B u \\\
y&=Cx
\end{align}

</div>



<div class="col">
\begin{align}
\dot{x}&=A x+\varepsilon g(x)+Bu\\\
&=\begin{bmatrix}
-2.86 &1 &4.7\\\
1.8 & -1 & 6.7\\\
-9 & 1 &-1 7.2
\end{bmatrix}x+ \sin(x)+B u \\\
y&=Cx
\end{align}
<br>

</div>

</div>

<br>
`\begin{align}
L*=\begin{bmatrix}
-8 & 1\\\
2 & -7
\end{bmatrix}
\end{align}`


`\begin{align}
u_1(t)&=c_{11} \sin(2t)+ c_{12} \cos(2t) + c_{13} \sin(7t) + c_{14} \cos(7t)
\end{align}`
`\begin{align}
u_2(t)&=c_{11} +c_{22}t+c_{23}t^2+c_{24}t^3
\end{align}`

</section>



<section>

<h1> Illustrative example</h1>
<h3> Both the state error and the input error converge simultaneously </h3>
<style>
.vertical-center {
  min-height: 100%;  /* Fallback for browsers do NOT support vh unit */
  min-height: 100vh; /* These two lines are counted as one :-)       */

  display: flex;
  align-items: center;
}

.container{
    display: flex;
}
.col{
    flex: 1;
}
</style>

<div class="container vertical-center">

<div class="col">
<figure>
  <img src="img/acc/ex_converge2.gif" alt="Trulli" height="500">
</figure>
</div>



<div class="col">
<figure>
  <img src="img/acc/eu_converge.gif" alt="Trulli" height="500">
</figure>

</div>

</div>

</section>

<section>

<h1> Illustrative example</h1>
<h3> provided $\epsilon$ is not too great </h3>
<p> `$0 < \epsilon < \frac{\lambda_{\min}(\bar{Q})}{2 \mu \lambda_{\max}(\bar{P})}$` </p>
<style>
.vertical-center {
  min-height: 100%;  /* Fallback for browsers do NOT support vh unit */
  min-height: 100vh; /* These two lines are counted as one :-)       */

  display: flex;
  align-items: center;
}

.container{
    display: flex;
}
.col{
    flex: 1;
}
</style>

<div class="container vertical-center">

<div class="col">
<figure>
  <img src="img/acc/ex_sad_epsilon2.gif" alt="Trulli" height="500">
</figure>
</div>



<div class="col">
<figure>
  <img src="img/acc/eu_sad_epsilon3.gif" alt="Trulli" height="500">
</figure>

</div>

</div>

</section>

---

<section>

<h1> Application: Biomarker dynamics </h1>
<style>
.vertical-center {
  min-height: 100%;  /* Fallback for browsers do NOT support vh unit */
  min-height: 100vh; /* These two lines are counted as one :-)       */

  display: flex;
  align-items: center;
}

.container{
    display: flex;
}
.col{
    flex: 1;
}
</style>

<div class="container vertical-center">

<div class="col">


<h3> Kalman filtering </h3>
<figure>
  <img src="img/acc/square_noL.gif" alt="Trulli" height="750">
</figure>

</div>



<div class="col">

<h3> aUIO  </h3>
<figure>
  <img src="img/acc/square_L.gif" alt="Trulli" height="750">
</figure>



</div>

</div>

</section>

---

<!-- .slide: data-background="#003C71" class="dark" -->


<h3>We lived in a sloppy world,  </h3>
<h2> ***but we were precise, very precise.*** </h2>
<br>
<div style="text-align: right"> <small>- Carrying the Fire</small></div>