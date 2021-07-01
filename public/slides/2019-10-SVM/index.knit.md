---
title: "Breast Cancer Classification"
subtitle: "⚔<br/>  by using SVM "
author: "<br><br>Yuan Du&nbsp;&nbsp;&nbsp;<!--html_preserve--><span>&lt;i class="fab  fa-linkedin faa-float animated "&gt;&lt;/i&gt;&amp;nbsp;https://www.linkedin.com/in/yuaneldaif/</span><!--/html_preserve-->"
date: "<br>10-15-2019<br><br><!--html_preserve--><span>&lt;i class="fas  fa-link faa-vertical animated " style=" color:white;"&gt;&lt;/i&gt;&amp;nbsp;https://yuandueldaif.netlify.com</span><!--/html_preserve-->"
output:
  xaringan::moon_reader:
    lib_dir: libs
    css: ["kunoichi", "ninjutsu", "assets/ninjutsu.css"]
    seal: true 
    self_contained: false
    nature:
      ratio: "16:9"
      highlightStyle: github
      highlightLines: true
      countIncrementalSlides: false
editor_options: 
  
  chunk_output_type: console
background-image: url("BreastCancer.jpg")
background-size: contain
---
class: bg-main1

background-image: url("BreastCancer.jpg")
background-size: contain
---
class: bg-main1
##⚠️Breast cancer is the second leading cause of cancer death in women after lung cancer. 

--
##⚠️There is a 1 in 8 chance she will develop breast cancer in the United States.

--
##⚠️The average 5-year survival rate for women with invasive breast cancer is 90%.

--
###🔴If the cancer is located only in the breast, the 5-year survival rate of women with breast cancer is 99%. 62% of people with breast cancer are diagnosed with this stage.

--
###🔴If the cancer has spread to the regional lymph nodes, the 5-year survival rate is 85%.

--
###🔴If the cancer has spread to a distant part of the body, the 5-year survival rate is 27%.

---
class: split-two white

.column.bg-main1[.content[
## Breast Cancer Wisconsin (Diagnostic) Data Set 
###University of Wisconsin, Clinical Sciences Center
<br>
###⚪Attribute Information:
###Number of instances: 569
###Number of attribute: 32
<br>
###1) ID number 
###2) Diagnosis (M = malignant, B = benign) 
<br>
###3-32)Ten real-valued features are computed for each cell nucleus:
a) radius (mean of distances from center to points on the perimeter) 
b) texture (standard deviation of gray-scale values) 
c) perimeter 
d) area 
e) smoothness (local variation in radius lengths) 
f) compactness (perimeter^2 / area - 1.0) 
g) concavity (severity of concave portions of the contour) 
h) concave points (number of concave portions of the contour) 
i) symmetry 
j) fractal dimension ("coastline approximation" - 1)


]]
.column.bg-main2[.content[
###The mean, standard error and "worst" or largest (mean of the three largest values) of these features were computed for each image, resulting in 30 features. For instance, field 3 is Mean Radius, field 13 is Radius SE, field 23 is Worst Radius.
<br>
###All feature values are recoded with four significant digits.
<br>
###⚪Missing attribute values: none
<br>
###⚪Class distribution: 357 benign, 212 malignant

]]


---
class: bg-main1
#Data Problems:
##.yellow[High dimensions]
###Attribute Information: Number of instances: 569, Number of attribute: 32
<img src="index_files/figure-html/unnamed-chunk-1-1.png" style="display: block; margin: auto;" />

---
class: bg-main1
##.yellow[Multicolinearity]: Same feature for each image was computed in three ways - mean, standard error and "worst" or largest (mean of the three largest values), results in 30 variables.
### Correlaion analysis by spearman since most variables are non normal distributed
<img src="index_files/figure-html/unnamed-chunk-2-1.png" style="display: block; margin: auto;" />

---
class: bg-main1

#Model: SVM
##.green[Article :] "Asymptotic normality of support vector machine variants and other regularized kernel methods" --Robert Hable

--
##.yellow[SVM Estimator] $$S_n: (\mathcal{X} \, X \, \mathcal{Y})^n \to H, \quad D_n \mapsto f_{L,D_n,\lambda_{D_n}}$$

##where $f_{L,D_n,\lambda_{D_n}}$ is that function $f \in H$ which minimizes $$\frac{1}{n} \sum L(x_i,y_i,f(x_i)) + \lambda_{D_n}||f||_H^2$$.

---
class: bg-main1

##Investiagte the Asymptotic properties on estimators:

--
###.yellow[Assumptions] to prove that Empirical SVM $f_{L,D_n,\lambda_{D_n}}$ is converged to theoretical SVM $f_{L,P,\lambda_0}$. This is $$\sqrt{n}(f_{L,D_n,\lambda_{D_n}} - f_{L,P,\lambda_0})$$ converges weakly to a (zero-mean) Gaussian process in the function space H.:

--
###.yellow[1)] $\mathcal{X}$ bounded and closed, $\mathcal{Y} \in \{-1,1\}$ in Function space H, $f:\mathcal{X} \to \mathbb{R}$, $(X_1,Y_1),\dots,(X_n,Y_n)$ are independent and identically distributed according to some unknown probability measure P on $(\mathcal{X} X \mathcal{Y},\mathcal{B}(\mathcal{X} X \mathcal{Y}))$.

--
###.yellow[2)] Assume Loss function is two times continuously differentiable in the third argument. This assumption is not based on any unknown entity as such model distribution P.

--
###.yellow[3)] Assume L is a P-integrable Nemitski loss function. 


--
###.yellow[4)] $\lambda$ is random sequence, so it's possible to use any data-driven method for choosing the regulization parameter, such as cross-validation. It's desirable to have a bound $$0 \leq \mathcal{R}_{L,P}(f_{L,P,\lambda_0}) - \mathcal{R}_{L,P}^* \leq C(\lambda_0) \to 0 \text{for} \lambda \to 0$$ to find $\lambda$

---
class: bg-main1
##The Proof is done by below steps:



<img src="Diagram.png" width="100%" height="100%" style="display: block; margin: auto;" />


---
class: bg-main1
#.yellow[Theorem 3.1:]
<img src="Theorem31.png" width="100%" height="100%" />

---
class: bg-main1
###.yellow[Step]1️⃣ Show that $\sqrt{n}(\mathbb{P}_{D_n} - P)$ converges weakly to a Gaussian process

--
###.yellow[Step]2️⃣The map $S: P \mapsto f_{L,P,\lambda}$ is suitably Hadamard-differentiable.

--
###🅰️ first order differentiable
###🅱️ second order differentiable

--
###.yellow[Step]3️⃣: Applying a functional delta-method, show asymptotic normality of $\lambda$,  $$\sqrt{n}(\lambda_{D_n} - \lambda_0) \xrightarrow{P} 0,$$ then the risk:    $$\sqrt{n}(\mathbb{R}_{L,P}(f_{L,D_n,\lambda_{D_n}}) - \mathbb{R}_{L,P}(f_{L,P,\lambda_0}))$$

---
class: bg-main1
##Related theorems in our class:

--
###🍫**Lebesgue Dominated Convergence Theorem**：If the random variables $X_n \to X$, then we have $|X_n| \leq Y$, almost surely for all n. Then $X_n \in L^1$, $X \in L^1$, and $\lim_{0\to\infty}E(X_n) = E(X)$.
<br>

--
###🍫**Central Limit Theorem** for some nonprametric estimators still are asymptotically normal for the same rate $\sqrt{n}$ as many parametric estiamators. This article showed that also SVM based on smooth loss fuctions enjoy an asymptotic normality property for the rate of $\sqrt{n}$.
<br>

--
###🍫**Taylor's series ( $O_p$ - delta function)** which was proved by law of large number (LLN). The average converges in probability to its expectation. 
<br>

---
class: bg-main1

#.yellow[Step]1️⃣️: CLT
<img src="Mainresult_1.png" width="100%" height="100%" />

---
class: bg-main1

#.yellow[Step]2️⃣: Define $B_s$ for Hadamard-differentiability
<img src="Mainresult_2.png" width="100%" height="100%" />

---
class: bg-main1

#.yellow[Step]3️⃣: Prove $\lambda$ is asymptotically normal so delta method can be applied
<img src="Mainresult_3.png" width="100%" height="100%" /><img src="Mainresult_4.png" width="100%" height="100%" />


---
class: bg-main1
#.yellow[Prove Theorem 3.1:] 
<img src="Theorem31_1.png" width="100%" height="100%" /><img src="Theorem31_2.png" width="100%" height="100%" />

---
class: bg-main1

#.yellow[Final : Prove Theorem 3.2 based on Theorem 3.1]
<img src="Theorem32.png" width="100%" height="100%" /><img src="Theorem32_1.png" width="100%" height="100%" />

---
class: bg-main1
#.yellow[Conclusion]:
##Asymptotic properties of support vector machines are investigated. 
<br>

--
###It is shown that the difference between the empirical and the theoretical SVM is asymptotically normal with rate $\sqrt{n}$; that is, $\sqrt{n}(f_{L,D_n,\lambda_{D_n}} - f_{L,P,\lambda_0})$ converges to a Gaussian process in the function space H.✔️
<br>

--
###These results are not only of theoretical interest but also be a starting point for statistical inferences such as confidence intervals and hypothesis testing.✔️
<br>

--
###Without any of such assumptions,similar results are not possible as follows from the no-free-lunch theorem.✔️

---
class: middle center bg-main1

<br/>

#😇Thank you!

<br/>

####Slides created via the R package [**xaringan**](https://github.com/yihui/xaringan) with [ninja themes](https://github.com/emitanaka/ninja-theme).


