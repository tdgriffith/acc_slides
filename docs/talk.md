<!-- .slide: data-background="#500000" class="dark" -->

# Adaptive Estimation of Unknown Inputs with Weakly Nonlinear Dynamics

## T. Griffith, V. Gehlot, M. Balas
#### ACC 2022

#### June 8, 2022

---

<!-- .slide: data-background="#ffffff" class="light" -->
# ***Outline***

### 1. Introduction & Motivation
### 2. A Dynamic Systems View of Brain Waves
### 3. System Identification of Brain Wave Modes Using EEG
### 4. Modal Analysis of Brain Wave Dynamics
### 5. Adaptive Unknown Input Estimators
### 6. Reconstructing the Brain's Unknown Input
### 7. Conclusions 


---

<!-- .slide: data-background="#ffffff" class="light" -->
# 1. Introduction & Motivation
<div class="col">
<img src="img/defense/black_box.png" alt="Trial 5, Averaged" width="80%">
<figcaption> Fig 1. A Wholistic View of Brain Waves </figcaption>
</div>


---

<!-- .slide: data-background="#ffffff" class="light" -->

<div class="col">
<img src="img/defense/guardrails.jpg" alt="Trial 5, Averaged" width="80%">
</div>

<div style="text-align: right"> <sub><sub><sup><a href="https://unsplash.com/@hogarthd">Hogarth de la Plante</a>, Unsplash</sup></sup></sub></div>

---

<!-- .slide: data-background="#ffffff" class="light" -->

# Clinical and HMI Applications

<img src="img/factory.jpg" alt="Trial 5, Averaged" width="32%">
<img src="img/hospital2.jpg" alt="Trial 5, Averaged" width="32%">
<img src="img/farm.jpg" alt="Trial 5, Averaged" width="32%">

<div style="text-align: right"> <sub><sub><sup><a href="https://www.wired.co.uk/article/robots-in-the-workplace">Spencer Lowell</a>, Wired, 2021</sup></sup></sub></div>

---


# Shared flow of information is implied
<style>
.container{
    display: flex;
}
.col{
    flex: 1;
}
</style>

<div class="container">

<div class="col">
<img src="img/defense/paradigm1.png" alt="Trulli" height="500">
<figcaption> The computer as part of the system </figcaption>
</div>

<div class="col">
<img src="img/defense/paradigm2.png" alt="Trulli" height="500">
  <figcaption> The computer as a teaming member </figcaption>
</div>

</div>




---

<!-- .slide: data-background="#ffffff" class="light" -->

# State of the art: surveys and orthogonal bases


> Recent modeling work, however, using large-scale dynamical models on the human connectome, suggests that cortical flow patterns are multistable and exhibit phase-transitions. To study such phenomena, a dynamic analysis in which no assumptions about stationarity are made, is required.




<div style="text-align: right"> <small>Hindriks, Rikkert, et al. "Latency analysis of resting-state BOLD-fMRI reveals traveling waves in visual cortex linking task-positive and task-negative networks." Neuroimage 200 (2019): 259-274.</small></div>

---

<!-- .slide: data-background="#ffffff" class="light" -->

# Novel potential

>  There has been a recent proliferation of more rugged and durable sensor devices (e.g., fNIRS sensors) that can be used while people take part in ecologically valid activities to assess changes in neurophysiology, physiology, and behavior that correlate with cognitive state. In addition, recent advances in machine learning and modeling techniques can be used to interpret information about human states (e.g., SA) from noisy data acquired in such environments that previously was unusable.



<div style="text-align: right"> <small>Bracken, B., Tobyne, S., Winder, A., Shamsi, N., & Endsley, M. R. (2021, July). Can Situation Awareness Be Measured Physiologically?. In International Conference on Applied Human Factors and Ergonomics (pp. 31-38). Springer, Cham.</small></div>

---

<!-- .slide: data-background="#ffffff" class="light" -->

## There is a demonstrated need for improved models of neural biomarkers that consider ***nonstationary spatio-temporal dynamics*** jointly.


- Rigorous
- Transparent
- Non-invasive
- Physiological



---

<!-- .slide: data-background="#ffffff" class="light" -->

# Modeling considerations
- Local vs. ***Whole***
- Linear vs. ***Nonlinear***
- ***Individual*** vs. Population
- Static vs. ***Dynamic***
- Offline vs. ***Online***
- Parametric vs. ***Nonparametric***


---


<!-- .slide: data-background="#003C71" class="dark" -->

# 2. A Dynamic Systems View of Brain Waves


---

<!-- .slide: data-background="#ffffff" class="light" -->

# Characteristics of EEG
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
  <li>EEG is only loosely tied to outcomes</li>
  <li>Linear, nonlinear, and noise</li>
  <li>Channel cross talk</li>
  <li>Variety of referencing techniques</li>
</ul> 
<img src="img/defense/EEG1020_ref_crop.png" alt="Trulli" height="500">
  <figcaption> Longitudinal referencing </figcaption>
</div>

<div class="col">
<figure>
  <img src="img/defense/channels_independent.png" alt="Trulli" height="500">
    <figcaption>EEG channel pair plots</figcaption>
</figure>
</div>

</div>


---


<!-- .slide: data-background="#ffffff" class="light" -->

# A cannonical approach: 

<img src="img/defense/eeg_ex.png" alt="Trulli" height="400">

:arrow_double_down:

True brain wave plant: 
  $\begin{aligned}
    \begin{cases}
    \dot{x}=Ax+Bu +v_x \\\
    y=Cx
    \end{cases}
  \end{aligned}$

where $A, \ B, \ C, \ v_x, \ x, \text{and} \ u $ are ***all unknown***.

----

## This level of uncertainty is an unsovled problem 

Identify the plant: 
  $\begin{aligned}
    \begin{cases}
\dot{x}_m=A_m x +v_x \\\
y_m=C x_m
\end{cases}
  \end{aligned}$,

accepting the uncertainty in $A_m$.

----

## Treating nonlinear effects
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
  <img src="img/defense/nonlin1.PNG" alt="Trulli" height="150">
</figure>
<figure>
  <img src="img/defense/nonlin2.PNG" alt="Trulli" height="150">
</figure>
<figure>
  <img src="img/defense/nonlin3.PNG" alt="Trulli" height="150">
</figure>
</div>

<div class="col">
<h3> Adaptive Unknown Input Brain Wave Estimator: </h3>

  $\begin{aligned}
    \begin{cases} 
      \dot{\hat{x}}=\big(A_m+BL(t)C\big) \hat{x} + B\hat{u} + K_x e_y; \\\
      \hat{y}= C \hat{x}.
    \end{cases} 
  \end{aligned}$
</div>

</div>

----

## Modes elegantly capture the spatio-temporal dynamics

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
<h4> True brain wave plant </h4>
  $\begin{aligned}
    \begin{cases}
    \dot{x}=Ax+Bu +v_x \\\
    y=C x
    \end{cases}
  \end{aligned}$
<br>
:arrow_double_down:
<h4> Modal brain wave plant </h4>
  $\begin{aligned}
    \begin{cases}
    \dot{\eta}=\Lambda \eta +V^{-1}B u + V^{-1} v_x \\\
    y=CV \eta
    \end{cases}
  \end{aligned}$
</div>



<div class="col">
<h3> Some important analytical properties: </h3>

 <ul>
  <li>Frequency</li>
  <li>Damping</li>
  <li>Mode shape</li>
  <li>Complexity</li>
</ul> 
</div>

</div>


---

<!-- .slide: data-background="#003C71" class="dark" -->

# 3. System Identification of Brain Wave Modes Using EEG

---

<!-- .slide: data-background="#ffffff" class="light" -->
<section>

<h1> System Identification of Brain Wave Modes Using EEG </h1>
<h2> Identifying linear patterns </h2>
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
Identify the plant: 
  $\begin{aligned}
    \begin{cases}
\dot{x}_m=A_m x +v_x\\\
y_m=C x_m 
\end{cases}
  \end{aligned}$
  <br><br>
  <h3> Considered algorithms </h3>
 <ul>
  <li>OMA</li>
  <li>NeXT-ERA</li>
  <li>n4sid</li>
  <li><strong><em>DMD</em></strong></li>
</ul> 
</div>

<div class="col">
<figure>
  <img src="img/defense/modal_out.png" alt="Trulli" height="800">
</figure>
</div>

</div>

</section>

<section>

<h1> System Identification of Brain Wave Modes Using EEG </h1>
<h2> Identifying linear patterns </h2>
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
Identify the plant: 
  $\begin{aligned}
    \begin{cases}
\dot{x}_m=A_m x +v_x\\\
y_m=C x_m 
\end{cases}
  \end{aligned}$
<br><br>
$\begin{aligned}
    O&=\begin{bmatrix}
    C \\\ CA_m \\\ CA_m^2 \\\ \vdots \\\ CA_m^{s-1}
    \end{bmatrix} X_0 \\\
    &= \Gamma X_0
\end{aligned}$
<br><br>
$\begin{aligned}
    \hat{\Gamma}=US^{1/2}\\
    \hat{X}_0=S^{1/2}V^*
\end{aligned}$
</div>



<div class="col">
<figure>
  <img src="img/defense/max_order.jpg" alt="Trulli" height="600">
</figure>
</div>

</div>

</section>

<section>

<h1> System Identification of Brain Wave Modes Using EEG </h1>
<h2> Identifying linear patterns </h2>
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
Identify the plant: 
  $\begin{aligned}
    \begin{cases}
\dot{x}_m=A_m x +v_x\\\
y_m=C x_m 
\end{cases}
  \end{aligned}$
<br><br>
$\begin{aligned}
    O&=\begin{bmatrix}
    C \\\ CA_m \\\ CA_m^2 \\\ \vdots \\\ CA_m^{s-1}
    \end{bmatrix} X_0 \\\
    &= \Gamma X_0
\end{aligned}$
<br><br>
$\begin{aligned}
    \hat{\Gamma}=US^{1/2}\\
    \hat{X}_0=S^{1/2}V^*
\end{aligned}$
</div>



<div class="col">
<figure>
  <img src="img/defense/truncate_ex.png" alt="Trulli" height="500">
</figure>
</div>

</div>

</section>


<section>

<h1> System Identification of Brain Wave Modes Using EEG </h1>
<h2> Identifying linear patterns </h2>
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
Identify the plant: 
  $\begin{aligned}
    \begin{cases}
\dot{x}_m=A_m x +v_x \\\
y_m=C x_m
\end{cases}
  \end{aligned}$
<br><br>
$\begin{aligned}
    O&=\begin{bmatrix}
    C \\\ CA \\\ CA^2 \\\ \vdots \\\ CA^{s-1}
    \end{bmatrix} X_0 \\\
    &= \Gamma X_0
\end{aligned}$
<br><br>
$\begin{aligned}
    \hat{\Gamma}=US^{1/2}\\
    \hat{X}_0=S^{1/2}V^*
\end{aligned}$
</div>



<div class="col">

<figure>
  <img src="img/defense/superposemodes.gif" alt="Trulli" height="600">
</figure>



</div>

</div>

</section>


<section>

<h1> System Identification of Brain Wave Modes Using EEG </h1>
<h2> Identifying linear patterns </h2>
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
Identify the plant: 
  $\begin{aligned}
    \begin{cases}
\dot{x}_m=A_m x +v_x\\\
y_m=C x_m
\end{cases}
  \end{aligned}$
<br><br>
$\begin{aligned}
    O&=\begin{bmatrix}
    C \\\ CA \\\ CA^2 \\\ \vdots \\\ CA^{s-1}
    \end{bmatrix} X_0 \\\
    &= \Gamma X_0
\end{aligned}$
<br><br>
$\begin{aligned}
    \hat{\Gamma}=U S^{1/2}\\
    \hat{X}_0=S^{1/2}V^*
\end{aligned}$
</div>



<div class="col">

<figure>
  <img src="img/defense/braingif/comb_tot.gif" alt="Trulli"  style="border:0px;margin:0px;float:left;width:800px;">
  <img src="img/defense/braingif/modes2.png" alt="Trulli" style="border:0px;margin:0px;float:left;width:800px;">
</figure>



</div>

</div>

</section>

<section>

<h1> System Identification of Brain Wave Modes Using EEG </h1>
<h2> Identifying linear patterns </h2>
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
Identify the plant: 
  $\begin{aligned}
    \begin{cases}
\dot{x}_m=A_m x +v_x\\\
y_m=C x_m
\end{cases}
  \end{aligned}$
<br><br>
$\begin{aligned}
    O&=\begin{bmatrix}
    C \\\ CA \\\ CA^2 \\\ \vdots \\\ CA^{s-1}
    \end{bmatrix} X_0 \\\
    &= \Gamma X_0
\end{aligned}$
<br><br>
$\begin{aligned}
    \hat{\Gamma}=U S^{1/2}\\
    \hat{X}_0=S^{1/2}V^*
\end{aligned}$
</div>



<div class="col">

<figure>
  <img src="img\defense\obsv.png" height="750">
</figure>



</div>

</div>

</section>

---


<!-- .slide: data-background="#003C71" class="dark" -->

# 4. Modal Analysis of Brain Wave Dynamics

---

<section>
<h1> Modal Analysis of Brain Wave Dynamics </h1>
<h2> Brain wave modes are traveling and standing </h2>
<img class="plain" src="img/animode.gif" alt="Trial 5, Averaged" style="height:600px;">
<img class="plain" src="img/animode2.gif" alt="Trial 5, Averaged" style="height:600px;">
</section>

<section>
<h1> Modal Analysis of Brain Wave Dynamics </h1>
<h2> Brain wave modes are traveling and standing </h2>
<img class="plain" src="img\defense\braingif\standing.gif" alt="Trial 5, Averaged" style="height:600px;">
<img class="plain" src="img\defense\braingif\traveling.gif" alt="Trial 5, Averaged" style="height:600px;">
</section>


<section>
<h1> Modal Analysis of Brain Wave Dynamics </h1>
<h2> Some brain wave modes are task independent </h2>
<img class="plain" src="img/common1.gif" alt="Trial 5, Averaged" style="height:500px;">
<img class="plain" src="img/common2.gif" alt="Trial 5, Averaged" style="height:500px;">

<table style="width:100%">
  <tr>
    <th> </th>
    <th>Frequency</th>
    <th>Damping [%]</th>
    <th>Complexity [%] </th>
    <th>Shape Correl.</th>
  </tr>
  <tr>
    <td>Alpha Mode 1 </td>
    <td> $4.34\pm 0.03$ </td>
    <td> $8.20\pm 1.20$ </td>
    <td> $11.47\pm 17.59$ </td>
    <td> $0.97 \pm 0.016$ </td>
  </tr>
  <tr>
    <td>Beta Mode 2 </td>
    <td> $21.83 \pm 0.22$ </td>
    <td> $1.98 \pm 2.63$ </td>
    <td> $32.29 \pm 35.67$ </td>
    <td> $0.96 \pm 0.018$ </td>
  </tr>
  <tr>
    <td>Gamma Mode 3 </td>
    <td> $40.39\pm 0.26$ </td>
    <td> $11.87 \pm 7.49$ </td>
    <td> $12.42 \pm 16.88$ </td>
    <td> $0.99 \pm 0.010$ </td>
  </tr>
  <tr>
    <td>Gamma Mode 4 </td>
    <td> $44.19 \pm 0.24$ </td>
    <td> $2.52\pm 1.39$ </td>
    <td> $2.93\pm 5.69$ </td>
    <td> $0.99 \pm 0.012$ </td>
  </tr>
</table>

</section>

<section>
<h1> Modal Analysis of Brain Wave Dynamics </h1>
<h2> Brain wave modes are interindividual </h2>
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
<img class="plain" src="img\confmat.jpg" alt="Trial 5, Averaged" style="height:800px;">
</div>



<div class="col">

<table style="width:100%">
  <tr>
    <th>Reference</th>
    <th>No. of Electrodes</th>
    <th>Accuracy [%]</th>
  </tr>
  <tr>
    <td>This work</td>
    <td>32</td>
    <td>99.85</td>
  </tr>
  <tr>
    <td>This work</td>
    <td>8</td>
    <td>96.45</td>
  </tr>
  <tr>
    <td><a href="https://ieeexplore.ieee.org/document/8745473">Wilaiprasitporn et al.</a> </td>
    <td>32</td>
    <td>99.90</td>
  </tr>
  <tr>
    <td><a href="https://ieeexplore.ieee.org/document/8745473">Wilaiprasitporn et al.</a> </td>
    <td>5</td>
    <td>99.1</td>
  </tr>
  <tr>
  <tr>
    <td><a href="https://www.worldscientific.com/doi/abs/10.1142/S0129065717500356">DelPozo-Banos et al.</a> </td>
    <td>32</td>
    <td>97.97</td>
  </tr>
  <tr>
</table>

</div>
</section>

<section>
<h1> Modal Analysis of Brain Wave Dynamics </h1>
<h2> Brain wave modes poorly match nonlinear dynamics </h2>
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
  <img src="img/defense/superposemodes.gif" alt="Trulli" height="600">
</figure>
</div>



<div class="col">

<figure>
  <img src="img/defense/bad_modes.gif" alt="Trulli" height="600">
</figure>



</div>


</section>

---

<!-- .slide: data-background="#003C71" class="dark" -->

# 5. Adaptive Unknown Input Estimators

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

<dl>
<dt>Three significant uncertainties</dt>
  <dd>- Input $u$ is unknown, external</dd>
  <dd>- State matrix $A$ may have uncertainty</dd>
  <dd>- General process uncertainty $v_x$</dd>
<dt>Can we synthesize $u$ and correct $A$?</dt>
</dl> 
</div>



<div class="col">

\begin{aligned}
    \dot{x}&=Ax+Bu+v_x\\\
    y&=Cx
\end{aligned}



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

<dl>
<dt>Approximate input space $\mathbb{U}$</dt>
  <dd>- $\hat{u}=\sum_{i=1}^{N} c_i f_i(t)$</dd>
<dt>Persisten Inputs</dt>
  <dd>- $\dot{z}_u=F_u z_u$</dd>
  <dd>- $\hat{u}=\Theta_u z_u$</dd>
  <dd>- $F_u = \begin{bmatrix} 0 & 1 & 0 \\\ -\omega^2 & 0 & 0 \\\ 0 & 0 & 0 \end{bmatrix}$</dd>
</dl> 
</div>



<div class="col">

<figure>
  <img src="img/defense/uhat.gif" alt="Trulli" height="600">
</figure>


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
  <img src="img/defense/est_arch.png" alt="Trulli" height="600">
</figure>
</div>



<div class="col">

Recover $A$ with adaptive scheme
`$$ A \equiv A_m +B L_{*} C $$`
`$$ \dot{L} = -e_y y^* \gamma_e - \alpha L; \ \alpha>0, \ \gamma_e > 0 $$`
<br>
Error dynamics

`$$ \dot{e}=(\bar{A}+\bar{K} \bar{C})e+\bar{B}w + v $$`
`$$ \begin{bmatrix} \dot{e}_x \\\ \dot{e}_z \end{bmatrix} = \Big(\begin{bmatrix} A_m & B \Theta_u \\\ 0 & F_u \end{bmatrix} + \begin{bmatrix} K_x \\\ K_u \end{bmatrix} \begin{bmatrix} C & 0 \end{bmatrix} \Big) \begin{bmatrix} e_x \\\ e_z \end{bmatrix} +\begin{bmatrix} B \\\ 0 \end{bmatrix} w +\begin{bmatrix} v_x \\\ v_u \end{bmatrix}$$`
`$$ \begin{bmatrix} \dot{e}_x \\\ \dot{e}_z \end{bmatrix} = \underbrace{\begin{bmatrix} A_m+K_x C & B \Theta_u \\\ K_u C & F_u \end{bmatrix}}_\text{$\bar{A}_c$} \begin{bmatrix} e_x \\\ e_z \end{bmatrix} +\begin{bmatrix} B \\\ 0 \end{bmatrix} w +\begin{bmatrix} v_x \\\ v_u \end{bmatrix}$$`


</div>



</section>

<section>
<h1> Adaptive Unknown Input Estimators </h1>
<h2> Architecture and estimator error </h2>

<dl>
<dt>ASD plant dynamics</dt>
<dt>Bounded `$L_{*}$`, $v$, and $\gamma_e$</dt>
<dt>Error in state and input converges to an n-ball centered at zero</dt>
  <dd>- `$V(e,\Delta L) = \frac{1}{2} e^* \bar{P} e + \frac{1}{2} \text{tr}(\Delta L \gamma_e^{-1} \Delta L^*)$`</dd>
  <dd>- `$\lim_{t \rightarrow \infty} \sup ||e(t)|| \leq \frac{1+\sqrt{\lambda_{\text{max}}\bar{P}}}{\alpha \sqrt{\lambda_{\text{min}}\bar{P}}} M_v \equiv R^*$`</dd>
</dl> 







<figure>
  <img src="img/defense/x_ex2.gif" alt="Trulli" height="400">
  <img src="img/defense/u_ex3.gif" alt="Trulli" height="400">
</figure>

</section>

---

<!-- .slide: data-background="#003C71" class="dark" -->

# 6. Reconstructing the Brain's Unknown Input
Recall: Solving the nonstationary problem

---

<section>

<h1> Reconstructing the Brain's Unknown Input </h1>
<h2> aUIO outperforms static modes </h2>
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

<h3> aUIO on unseen data </h3>
<figure>
  <img src="img/defense/square_L.gif" alt="Trulli" height="750">
</figure>
</div>



<div class="col">

<h3> Weighted modes on seen data </h3>
<figure>
  <img src="img/defense/square_noL.gif" alt="Trulli" height="750">
</figure>



</div>

</div>

</section>

<section>

<h1> Reconstructing the Brain's Unknown Input </h1>
<h2> aUIO critically updates model as needed </h2>
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

<h3> aUIO on unseen data </h3>
<figure>
  <img src="img/defense/square_L.gif" alt="Trulli" height="750">
</figure>
</div>



<div class="col">

<h3> Adaptive gain matrix 2-norm </h3>
<figure>
  <img src="img/defense/Ly.gif" alt="Trulli" height="750">
</figure>



</div>

</div>

</section>

</section>

<section>

<h1> Reconstructing the Brain's Unknown Input </h1>
<h2> Modeling details </h2>

 <ul>
  <li>Unknown input acts evenly over spatial domain</li>
  <li>$F_u$ generates sine-cosine basis</li>
  <li>Static gains per LQR </li>
</ul> 

</section>

<section>

<h1> Reconstructing the Brain's Unknown Input </h1>
<h2> aUIO is tolerant to parametric uncertainty in modes </h2>
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

<h3> aUIO on unseen data </h3>
<figure>
  <img src="img/defense/no_eye.gif" alt="Trulli" height="600">
</figure>
</div>



<div class="col">

<h3> aUIO with wrong $A_m$ </h3>
<figure>
  <img src="img/defense/eye.gif" alt="Trulli" height="600">
</figure>



</div>

</div>

</section>

<section>

<h1> Reconstructing the Brain's Unknown Input </h1>
<h2> Classification via estimation </h2>
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
  <img src="img/defense/val_arou.jpg" alt="Trulli" height="400">
</figure>

</div>



<div class="col">

<figure>
  <img src="img/defense/classification_alg.png" alt="Trulli" height="300">
</figure>



</div>

</div>

</section>

<section>

<h1> Reconstructing the Brain's Unknown Input </h1>
<h2> Classification via estimation </h2>
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
<h3> Valence Classification </h3>
<figure>
  <img src="img/defense/val_acc.png" alt="Trulli" height="600">
</figure>

</div>

<div class="col">
<h3> Arousal Classification </h3>
<figure>
  <img src="img/defense/arou_acc.png" alt="Trulli" height="600">
</figure>


</div>

</div>
<div style="text-align: right"> <sub><sub><sup><a href="https://dl.acm.org/doi/10.5555/3297863.3297883">CNN1</a>, <a href="https://www.sciencedirect.com/science/article/abs/pii/S0010482521005515">CNN2</a>, <a href="https://www.frontiersin.org/articles/10.3389/fnbot.2020.617531/full">MFDF</a></sup></sup></sub></div>


</section>

<section>

<h1> Reconstructing the Brain's Unknown Input </h1>
<h2> Classification validation </h2>
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
<table style="width:80%">
  <tr>
    <th>Task</th>
    <th>aUIO Acc. [%]</th>
    <th>PSD CNN Acc. [%]</th>
  </tr>
  <tr>
    <td>DEAP Valence</td>
    <td>77.8</td>
    <td>68.1</td>
  </tr>
  <tr>
    <td>DEAP Arousal</td>
    <td>75.2</td>
    <td>63.8</td>
  </tr>
  <tr>
    <td>Like/Dislike</td>
    <td>79.4</td>
    <td>67.3</td>
  </tr>
  <tr>
</table>


</div>

<div class="col">
<h3> Static gain grid search </h3>
<figure>
  <img src="img/defense/DEAP_accs.png" alt="Trulli" height="600">
</figure>


</div>

</div>

</section>

---

<!-- .slide: data-background="#003C71" class="dark" -->

# 7. Conclusions


---












<!-- .slide: data-background="#5B6236" class="dark" -->

## Backup: Best Fit B Matricies

----

<!-- .slide: data-background="#ffffff" class="light" -->

# *A* Convex Function for B matrix optimization
- $\min ||y-\hat{y}-C \Delta B \hat{u}||_2$
- ***not*** the only possible minimization

----

<!-- .slide: data-background="#ffffff" class="light" -->

# B Matrix Optimization Example
- 3x3 example
 - $\dot{\hat{x}} = A_m x + B \hat{u}$
 - $A_m \neq A$ 
- ***$\min ||y-\hat{y}-C \Delta B \hat{u}||_2$***
- $B=\begin{bmatrix} 1.2 \\\ 1 \\\ 1.6 \end{bmatrix}$, 
- $B_m=\begin{bmatrix} 1 \\\ 1 \\\ 1 \end{bmatrix}$




----

<!-- .slide: data-background="#ffffff" class="light" -->

# B Matrix Optimization Example
- $\min ||y-\hat{y}-C \Delta B \hat{u}||_2$
- $\Delta B=\begin{bmatrix} 0.18 \\\ 0 \\\ 0.37 \end{bmatrix}$, 
- $B_f=\begin{bmatrix} 1.18 \\\ 1 \\\ 1.37 \end{bmatrix}$

<img class="plain" src="img/bmat/toy_Bopt2.png" alt="Trial 5, Averaged" width="55%">


----

<!-- .slide: data-background="#ffffff" class="light" -->

# B Matrix on EEG Data
<img class="plain" src="img/bmat/Bopt.png" alt="Trial 5, Averaged" width="90%">


----

<!-- .slide: data-background="#ffffff" class="light" -->

# B Matrix on EEG Data
<img class="plain" src="img/bmat/B_ic.jpg" alt="Trial 5, Averaged" width="70%">


----


<!-- .slide: data-background="#ffffff" class="light" -->

# Current models
<img class="plain" src="img/bmat/UIO_opt.png" alt="Trial 5, Averaged" width="45%">
<img class="plain" src="img/bmat/Bmap2.png" alt="Trial 5, Averaged" width="45%">


----

<!-- .slide: data-background="#ffffff" class="light" -->

## 5. Application to Emotion Data

----



<!-- .slide: data-background="#ffffff" class="light" -->


## B Matrix on EEG Data: ***Satisfaction (T1)*** 
<img class="plain" src="img/bmat/sat_map.png" alt="Trial 5, Averaged" width="60%">



----

<!-- .slide: data-background="#ffffff" class="light" -->

## B Matrix on EEG Data: ***Surprise (T2)*** 

<img class="plain" src="img/bmat/surp_map.png" alt="Trial 5, Averaged" width="60%">


----

<!-- .slide: data-background="#ffffff" class="light" -->

## B Matrix on EEG Data: ***Fear (T8)*** 

<img class="plain" src="img/bmat/fear_map.png" alt="Trial 5, Averaged" width="60%">



----

<!-- .slide: data-background="#ffffff" class="light" -->
## Comparing the same "emotion"

<img class="plain" src="img/bmat/val.jpg" alt="Trial 5, Averaged" width="45%">

<div style="text-align: right"> <small>Mneimne, M., Powers, A. S., Walton, K. E., Kosson, D. S., Fonda, S., & Simonetti, J. (2010). Emotional valence and arousal effects on memory and hemispheric asymmetries. Brain and Cognition, 74(1), 10-17.</small></div>


----

<!-- .slide: data-background="#ffffff" class="light" -->

## B Matrix on EEG Data: ***HVHA*** 

<img class="plain" src="img/bmat/HVHA_map.png" alt="Trial 5, Averaged" width="60%">


----

<!-- .slide: data-background="#ffffff" class="light" -->

## B Matrix on EEG Data: ***HVLA*** 

<img class="plain" src="img/bmat/HVLA_map.png" alt="Trial 5, Averaged" width="60%">


----

<!-- .slide: data-background="#ffffff" class="light" -->

## B Matrix on EEG Data: ***LVHA*** 

<img class="plain" src="img/bmat/LVHA_map.png" alt="Trial 5, Averaged" width="60%">



----

<!-- .slide: data-background="#ffffff" class="light" -->

## B Matrix on EEG Data: ***LVLA***  

<img class="plain" src="img/bmat/LVLA_map.png" alt="Trial 5, Averaged" width="60%">

----

<!-- .slide: data-background="#ffffff" class="light" -->

## B Matrix on EEG Data: ***Avg. Quadrants***  

<img class="plain" src="img/bmat/all_emot_map.png" alt="Trial 5, Averaged" width="60%">

----

<!-- .slide: data-background="#ffffff" class="light" -->

## 6. Application to Movement Data

----

<!-- .slide: data-background="#ffffff" class="light" -->

## B Matrix on EEG Data: ***Left Hand***  

<img class="plain" src="img/bmat/lh_map.png" alt="Trial 5, Averaged" width="60%">

----

<!-- .slide: data-background="#ffffff" class="light" -->

## B Matrix on EEG Data: ***Right Hand***  

<img class="plain" src="img/bmat/rh_map.png" alt="Trial 5, Averaged" width="60%">

----

<!-- .slide: data-background="#ffffff" class="light" -->

## B Matrix on EEG Data: ***Resting***  

<img class="plain" src="img/bmat/rest_map.png" alt="Trial 5, Averaged" width="60%">

----

<!-- .slide: data-background="#ffffff" class="light" -->

## B Matrix on EEG Data: ***All Averages***  

<img class="plain" src="img/bmat/all_hand_map.png" alt="Trial 5, Averaged" width="60%">

----

<!-- .slide: data-background="#ffffff" class="light" -->

## A unique solution?
- B matrix is different for everyone
 - A math construct or physical significance?
- A unique input?

