---
presentation:
  # presentation 主题
  # === 可选的主题 ===
  # "beige.css"
  # "black.css"
  # "blood.css"
  # "league.css"
  # "moon.css"
  # "night.css"
  # "serif.css"
  # "simple.css"
  # "sky.css"
  # "solarized.css"
  # "white.css"
  # "none.css"
  theme: serif.css

  # The "normal" size of the presentation, aspect ratio will be preserved
  # when the presentation is scaled to fit different resolutions. Can be
  # specified using percentage units.
  width: 960
  height: 700

  # Factor of the display size that should remain empty around the content
  margin: 0.1

  # Bounds for smallest/largest possible scale to apply to content
  minScale: 0.2
  maxScale: 1.5

  # Display controls in the bottom right corner
  controls: true

  # Display a presentation progress bar
  progress: true

  # Display the page number of the current slide
  slideNumber: true

  # Push each slide change to the browser history
  history: false

  # Enable keyboard shortcuts for navigation
  keyboard: true

  # Enable the slide overview mode
  overview: true

  # Vertical centering of slides
  center: true

  # Enables touch navigation on devices with touch input
  touch: true

  # Loop the presentation
  loop: false

  # Change the presentation direction to be RTL
  rtl: false

  # Randomizes the order of slides each time the presentation loads
  shuffle: false

  # Turns fragments on and off globally
  fragments: true

  # Flags if the presentation is running in an embedded mode,
  # i.e. contained within a limited portion of the screen
  embedded: false

  mouseWheel: true

---


<!-- slide -->
## Review: How to go beyond the black-box simulation barrier 
Zihan Hu, Kai Su, Shiyu Zhao 
<!-- slide -->
### Recap
* Zero-knowledge
  <font size=5>There exists a probabilistic polynomial-time simulator S such that for every polynomial-sized circuit family $\{V_N^*\}_{n\in \mathbb{N}}$ and every sequence $\{(x_n,y_n)\}_{n\in \mathbb{N}}$, where $x_n\in \{0,1\}^n \cap L$ and $(x_n,y_n)\in R$, we have
  $$\left\{\operatorname{view}_{V_{n}^{*}}\left\langle P\left(x_{n}, y_{n}\right), V_{n}^{*}\left(x_{n}\right)\right\rangle\right\}_{n \in \mathbb{N}}\approx_C \left\{S(V_n^*,x_n)\right\}$$
  </font> 

<!-- slide -->
## General Idea

<!-- slide -->
### Key point of simulator
* Challenge
  * <font size=5>convince verifier without witness </font>
* Advantages
  * <font size=5>have access to random tape of verifier,    
  predict next question to ask</font>
  * <font size=5>retry when it fails (called *rewinding* technique)</font>

<!-- slide -->
### Why non-black-box
blackbox = verifier as an oracle
non-black-box = code of verifier
* Control randomness?
  <font size=5>verifier can hide randomness into algorithm (PRF, hash function)</font>
  * <font size=5>random, uncontrollable if it's black-box</font>
  * <font size=5>Reverse-engineering is hard and code can be well-obfuscated 
  still random, still uncontrollable even when it's non-black-box</font>
* Rewinding(all zero-knowledge protocols)
    <font size=5>1. NO constant-round  zero-knowledge  proof  in  con-current composition</font>
    <font size=5>2. NO constant-round  zero-knowledge  proof  in strict polynomial time</font>

<!-- slide -->
### Why non-black-box
* Rewinding
<font size=5>''easy question'': The questions simulator can output answer successfully
Rewinding is just to **find** the ''easy question''
</font>
* **Key idea!**
<font size=5>What about modifying the definition of ''easy question''?</font><font size=7>
''easy question'' = ''what the verifier asks'' </font>
<font size=5>So it can be trivially answered</font>

* How?
**<center>FLS technique!<center>**

<!-- slide -->
## FLS  Zero-Knowledge  Argument


<!-- slide -->
### FLS technique
* Idea
  <font size=5>a framework that allows using **trapdoor information** to cheat the verifier while verifier **does not know it is cheated** </font>
  <font size=5>
  * let **trapdoor information** to be the question verifier asks
  $\Rightarrow$ Knowing what the verifier asks is enough to convince/cheat the verifier
  $\Leftrightarrow$''easy question'' is just ''what the verifier asks'' as desired</font>
  <font size=5>
  * Role of description: to define the ''easy question'' to be what the verifier asks</font>

<!-- slide -->
### FLS technique
* Idea
* Witness-indistinguishable
  <font size=5>Let L = L(R) be some language and let (P, V) be an interactive argument for L. We say that (P, V) is witness-indistinguishable if for every polynomial-sized circuit family $\{V^*_n\}_{n\in \mathbb{N}}$ and every sequence ${(x_n, y_n, y'_n)}_{n\in \mathbb{N}}$, where $x_n \in \{0, 1\}_n$ and $(x_n, y_n), (x_n, y'_n) \in R$ , we have 
  $$\left\{\operatorname{view}_{V_{n}^{*}}\left\langle P\left(x_{n}, y_{n}\right), V_{n}^{*}\left(x_{n}\right)\right\rangle\right\}_{n \in \mathbb{N}}\approx_C \left\{\operatorname{view}_{V_{n}^{*}}\left\langle P\left(x_{n}, y'_{n}\right), V_{n}^{*}\left(x_{n}\right)\right\rangle\right\}_{n \in \mathbb{N}}$$</font>
  * <font size=5> Let the view of proving with witness for x and witness for trapdoor be indistinguishable $\Rightarrow$ verifier does not know it's cheated</font>


<!-- slide -->
### FLS-type zero-knowledge protocol
![](./FLSprot.png)
 <font size=5>Notice: In WI proof, $\langle x, \tau\rangle\in L'$ if either $x\in L$ or $\tau \in \Lambda$</font>


<!--
### FLS technique
 <img src="./FLSprot.png" width = "640" height = "300" alt="图片名称" align=center />

* Reduction
  * <font size=5>Aim: find an iteractive zero-knowledge proof for language $L\in NP$</font>
  * <font size=5>Design a language $L'$ from $L$ ($\langle x, \tau\rangle\in L'$ if either $x\in L$ or $\tau \in \Lambda$)</font>
  * <font size=5>Find a WI proof for $L'$ (universal arguments)</font>
  * <font size=5>Use FLS technique to derive a zero-knowledge proof for $L$ from a WI proof for $L'$</font>

### Generation protocol's properties

* Soundness
  * <font size=6>$Pr[\tau \in \Lambda]< \epsilon(n)$</font>
  <font size=6>So that $\forall P^*$, if $x\notin L$, $Pr[\langle P^*,V\rangle(x)=1]<\epsilon(n)$</font>
* Properly generated
  * <font size=6>$\exists S_{GenProt}$ that outputs $(v, \sigma)$ satisfying</font>
    * <font size=5>$\left\{\operatorname{view}_{V_{n}^{*}}\left\langle P\left(x_{n}, y_{n}\right), V_{n}^{*}\left(x_{n}\right)\right\rangle\right\}_{n \in \mathbb{N}}\approx_{C} v$</font>
    * <font size=5>$\tau \in \Lambda$ and $\sigma$ is the witness</font>

### Proof: FLS-type protocol is zero-knowledge argument
* Completeness
  * <font size=6>If $x\in L$, then $\langle x, \tau\rangle \in L$</font>
* Soundness
  * <font size=6>If $x\notin L$, since $Pr[\tau\in \Lambda]<\epsilon(n), Pr[x\in L \text{ or } \tau\in \Lambda]<\epsilon(n)$</font>
* Zero-knowledge

### Proof: FLS-type protocol is zero-knowledge argument
* Zero-knowledge
![](/FLS_sim.png)
-->


<!-- slide -->

![](./2-showcase/幻灯片1.PNG)

<!-- slide -->

![](./2-showcase/幻灯片2.PNG)

<!-- slide -->

![](./2-showcase/幻灯片3.PNG)

<!-- slide -->

![](./2-showcase/幻灯片4.PNG)

<!-- slide -->

Game #1: Bob wins if he outputs some “random” string.

$$
\begin{aligned}
\text{Prover}\xleftarrow{r}&\text{Verifier}\\
\end{aligned}\\
M:\text{a TM that outputs }r\\
\Lambda = \left\{r:\exists M,\left|M\right|<\frac{\left|r\right|}2,M()=r\text{ in }|r|^{\log\log|r|}\right\}
$$

<!-- slide -->

![](./2-showcase/幻灯片6.PNG)

<!-- slide -->

Game #2: Bob wins if:
he has a different output from the program sent by Alice.

<font size=5>

$$
\begin{aligned}
\text{Prover}\xrightarrow{z}&\text{Verifier}\\
\text{Prover}\xleftarrow{r}&\text{Verifier}\\
\end{aligned}\\
\Lambda = \left\{(z, r):\exists(s,\Pi),\text{Com}(\Pi;s) = z, \Pi(z) = r \text{ in } |r|^{\log\log|r|}\right\}
$$

</font>

<!-- slide -->

### Non-Uniform Verifier

<!-- slide -->

![](./2-showcase/幻灯片9.PNG)

<!-- slide -->

![](./2-showcase/幻灯片10.PNG)

<!-- slide -->

Game #3: Bob wins if:
he has a different output from the program
<span style="color:red;">whose hash is sent by Alice.</span>

<font size=5>

$$
\begin{aligned}
\text{Prover}\xleftarrow{h}&\text{Verifier}\\
\text{Prover}\xrightarrow{z}&\text{Verifier}\\
\text{Prover}\xleftarrow{r}&\text{Verifier}\\
\end{aligned}\\
\Lambda = \left\{(h, z, r):\exists (s, \Pi),\text{Com}(h(\Pi);s) = z, \Pi(z) = r \text{ in } |r|^{\log\log|r|}\right\}
$$

</font>

<!-- slide -->

  Sometimes prover proves related statements simultaneously...

<!-- slide -->

![](./pic_for_concurrent_1.jpg)


<!--### Definition
* $t$-times concurrent execution
​<font size=5>Run $t$ **independent** copies of $P$ with **one** verifier $V$ on $t$ instances. $V$ chooses which prover to ask at each time and is given the response from the corresponding prover.
</font> -->

<!-- slide -->

![](./def_execution.jpg)

<!-- slide -->

![](./def_concurrent_ZK.jpg)

<!-- slide -->

![](./pic_for_naive_sim.jpg)

<!-- slide -->


<font size=5>

$$\begin{aligned}
&\text{Prover}\xleftarrow{h}&\text{Verifier}\\
&\text{Prover}\xrightarrow{z}&\text{Verifier}\\
&\text{Prover}\xleftarrow{r}&\text{Verifier}\\
\end{aligned}\\$$

</font>

##### Non-uniform case

<font size=5>$\Lambda = \{(h, z, r):\exists(s, \Pi),\text{Com}(h(\Pi);s) = z, \Pi(z) = r \text{ in } |r|^{\log\log|r|}\}$
</font>

​                                                                         $\downarrow$
##### Bounded concurrent zero-knowledge case

<font size=5>$\Lambda = \{(h, z, r):\exists (s, \Pi,y),\text{Com}(h(\Pi);s) = z, \Pi(z,y) = r \text{ in } |r|^{\log\log|r|}\}$
</font>

<!-- slide -->

#### Proof Sketch

<font size=5>$\Lambda = \{(h, z, r)|\exists (s, \Pi,y),\text{Com}(h(\Pi);s) = z, \Pi(z,y) = r \text{ in } |r|^{\log\log|r|}\}$
</font>

<div style="text-align:left;">

* <font size=5> Simulator: two parts 
  * $S_{GenProt}$ generates the view of generation protocol (the first stage) and the trapdoor information $(s, \Pi, y)$ along with $(h, z, r)$

  * $S_{WI}$ generates the view of witness indistinguishable universal argument (the second stage)

</font>

* <font size=5> Completeness (trivial)
</font>

* <font size=5> Soundness
</font>

</div>

<!-- slide -->

#### Proof Sketch (Cont'd)

<font size=5>$\Lambda = \{(h, z, r)|\exists (s, \Pi,y),\text{Com}(h(\Pi);s) = z, \Pi(z,y) = r \text{ in } |r|^{\log\log|r|}\}$
</font>

<div style="text-align:left;">

* <font size=5> Simulator
</font>

* <font size=5> Completeness (trivial)
</font>

* <font size=5> Soundness
If verifier will be convinced with non-negligible probability for random $r$, 
consider random $r \ne r'$, 
$\text{Com}(h(\Pi);s) = z, \Pi(z,y) = r$, $\text{Com}(h(\Pi');s') = z, \Pi'(z,y') = r'$
$\Rightarrow h(\Pi) = h(\Pi')$, if $|y| < \frac{|r|}{2}$, $\Pi \ne \Pi'$
</font>

</div>

<!-- slide -->

##### Non-uniform case

<font size=5>$\Lambda = \{(h, z, r)|\exists(s, \Pi),\text{Com}(h(\Pi);s) = z, \Pi(z) = r \text{ in } |r|^{\log\log|r|}\}$
</font>

​                                                                         $\downarrow$
##### Bounded concurrent zero-knowledge case

<font size=5>$\Lambda = \{(h, z, r)|\exists (s, \Pi,y), |y| < \frac{|r|}{2}, \text{Com}(h(\Pi);s) = z, \Pi(z,y) = r \text{ in } |r|^{\log\log|r|}\}$
</font>


<!-- slide -->

### Summary

<font size=5>Assuming the existence of CRH (against some adversaries), there is a zero-knowledge argument system for NP satisfying the following properties:
</font>

* <font size=5>negligible soundness error </font>
* <font size=5>for non-uniform $V^*$ </font>
* <font size=5>constant rounds and public coin
</font>
* <font size=5>bounded concurrent zero-knowledge
</font>
* <font size=5>strict polynomial time simulator
</font>

<!-- slide -->

### Subsequent work

 <font size = 5>why we need CRH against a super polynomial adversary?
 </font>

<!-- slide -->

### Subsequent work

 <font size = 5>why we need CRH against a super polynomial adversary?

 based on more standard assumption?

 [BG01] Suppose CRH against ***polynomial***-sized adversary exists, universal argument and witness-indistinguishable universal argument exist. Furthermore, these proof systems are of ***public coin*** type and use a ***constant*** number of rounds.
 </font>

<!-- slide -->

#### Proof Sketch

* <font size=5>universal argument: via PCP
</font>

* <font size=5>+ witness indistinguishable: via concurrent execution of "encrypt" version of universal argument + constant error soundness zero-knowledge proof
</font>

* <font size=5>how to use in this work: 
  * hope that a random bit is different (via error correcting code)
  * hope that we can decommit to a single bit (via tree commitment)

</font>


<!-- slide -->

### Future directions

* <font size=5> Non-black-box proofs of security
</font>

* <font size=5> Black box reduction and non-black box reduction
</font>

* <font size=5> Arguments vs. proof
</font>

* <font size=5> Fiat-Shamir heuristic
</font>

<!-- slide -->

## Thank you!
