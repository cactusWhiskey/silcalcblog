---
layout: post
title: >
    Analytical Equations
image:
  path:    /assets/img/blog/pfd_avg.png
  srcset:
    2329w: /assets/img/blog/pfd_avg.png



description: >
  Theoretical post about PFD equations derivation
sitemap: true
excerpt_separator: <!--more-->
permalink: /2023/03/17/analytical-equations/
tags:       [theoretical]
---

# Analytical PFD and PFD Avg Equations

* this unordered seed list will be replaced by the toc
{:toc}

It's long past time we derived the analytical equations for the common voting configurations. This post won't have a ton of exposition, we are just going to get down to the work of deriving the various equations, and then finding their averages. Cataloging these will come in useful down the road, so let's hit it.
<!--more-->

## Tables of Results
If you just care about the results and none of the math:
### Same Lambda

PFD equations assuming all devices in the voting scheme have the same lambda:

| **Voting** |                                                                                     **PFD**                                                                                    |                      **PFD Avg**                     |
|:----------:|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|:----------------------------------------------------:|
|    1oo1    |                                                                          $$1 - e^{-\lambda t}$$                                                                          | $$1 + \frac{e^{-\lambda T}-1}{\lambda T}$$ |
|    1oo2    |                                                                           $$1 - 2e^{-\lambda t} + e^{-2\lambda t}$$            | $$1 + \frac{2e^{-\lambda T}-2}{\lambda T} + \frac{1-e^{-2\lambda T}}{2\lambda T}$$                  |
|    2oo2    |                                                         $$ 1 - e^{-2\lambda t} $$                                                         |   $$1 + \frac{e^{-2\lambda T}-1}{2\lambda T}$$                |
|    1oo3    | $$1 - 3 e^{- \lambda t} + 3 e^{- 2 \lambda t} - e^{- 3 \lambda t}$$ | $$1 - \frac{11}{6 \lambda T} + \frac{3 e^{- \lambda T}}{\lambda T} - \frac{3 e^{- 2 \lambda T}}{2 \lambda T} + \frac{e^{- 3 \lambda T}}{3 \lambda T}$$        |
|    2oo3    | $$1 - 3 e^{- 2 \lambda t} + 2 e^{- 3 \lambda t}$$   | $$1 - \frac{5}{6 \lambda T} + \frac{3 e^{- 2 \lambda T}}{2 \lambda T} - \frac{2 e^{- 3 \lambda T}}{3 \lambda T}$$ |
|    3oo3    | $$1 - e^{- 3 \lambda t}$$|    $$1 - \frac{1}{3 \lambda T} + \frac{e^{- 3 \lambda T}}{3 \lambda T}$$               |

### Unique Lambdas

These don't render in a table nicely because they tend to be longer, please just jump to the relevant section to see the results for unique lambdas.

## Derivations
### 1oo1 Analytical PFD

This one we already know and love. We derived it from scratch in a [previous post](/2021/05/04/pfd-equation-derivation/), if you're interested. We will just take it as a given here:

$$
\begin{equation}
PFD = 1 - e^{-\lambda t}
\end{equation}
$$



### 1oo1 Analytical PFD average

Finding the average of a function involves integrating the function, then dividing by the time interval. Check out [Wikipedia](https://en.wikipedia.org/wiki/Mean_of_a_function) for an overview. Thankfully for us, functions involving exponentials tend to be easy to integrate. It often helps to think about them backwards, i.e. what function do I need to write down, so that when I take it's derivative, I get the original exponential function. Typically this just amounts to dividing the original exponential by the derivative of whatever is in the exponent, like so:


$$
\begin{align}
PFD_{avg} &= \frac{1}{T} \int_{0}^{T} 1 - e^{-\lambda t} \,dt \\ \\
 &= \frac{1}{T} * \left[t + \frac{e^{-\lambda t}}{\lambda} \right] _0^T \\ \\
 &= \frac{1}{T} * \left[T + \frac{e^{-\lambda T}}{\lambda} - \frac{1}{\lambda} \right] \\ \\
 &= 1 + \frac{e^{-\lambda T}-1}{\lambda T}
\end{align}
$$

Where "T" is the time interval over which we want to calculate the average PFD.

### 1oo2 Analytical PFD

Referencing the table in our [multiple elements post](/2020/12/10/sil-calcs-101-multiple-elements/), we see that the logic for 1oo2 voting is:


$$
\begin{equation}
P_AP_B
\end{equation}
$$

Substituting in the basic equation for the PFD of a 1oo1 system for each probability:

$$
\begin{equation}
P_AP_B = (1-e^{-\lambda_A t})(1-e^{-\lambda_B t})
\end{equation}
$$

Where  	&lambda;<sub>A</sub> and &lambda;<sub>B</sub> are the failure rates of the two devices. These are often taken to be the same, but lets keep them separate for now so as to be a bit more general.

Multiplying through:

$$
\begin{align}
P_AP_B &= (1-e^{-\lambda_A t})(1-e^{-\lambda_B t}) \\ \\
&= 1 -e^{-\lambda_A t} - e^{-\lambda_B t} + e^{-(\lambda_A+\lambda_B) t}
\end{align}
$$

Combining terms if lambda is assumed to be the same for each device:

$$
\begin{equation}
PFD = 1 - 2e^{-\lambda t} + e^{-2\lambda t}
\end{equation}
$$

### 1oo2 Analytical PFD average

Finding the average, assuming different lambdas for each device:

$$
\begin{align}
PFD_{avg} &= \frac{1}{T} \int_{0}^{T} 1 -e^{-\lambda_A t} - e^{-\lambda_B t} +  e^{-(\lambda_A+\lambda_B) t} \,dt \\ \\
 &= \frac{1}{T} * \left[t + \frac{e^{-\lambda_A t}}{\lambda_A} + \frac{e^{-\lambda_B t}}{\lambda_B} - \frac{e^{-(\lambda_A+\lambda_B) t}}{\lambda_A+\lambda_B} \right] _0^T \\ \\
 &= \frac{1}{T} * \left[T + \frac{e^{-\lambda_A T}}{\lambda_A} + \frac{e^{-\lambda_B T}}{\lambda_B} - \frac{e^{-(\lambda_A+\lambda_B) T}}{\lambda_A+\lambda_B} - \frac{1}{\lambda_A} - \frac{1}{\lambda_B} + \frac{1}{\lambda_A+\lambda_B} \right] \\ \\
 &= 1 + \frac{e^{-\lambda_A T}-1}{\lambda_A T} + \frac{e^{-\lambda_B T}-1}{\lambda_B T} + \frac{1-e^{-(\lambda_A+ \lambda_B )T}}{(\lambda_A+\lambda_B) T}
\end{align}
$$

Where "T" is the time interval over which we want to calculate the average PFD.

Assuming the lambdas are the same:


$$
\begin{equation}
PFD_{Avg} = 1 + \frac{2e^{-\lambda T}-2}{\lambda T} + \frac{1-e^{-2\lambda T}}{2\lambda T}
\end{equation}
$$

### 2oo2 Analytical PFD

Referencing the table in our [multiple elements post](/2020/12/10/sil-calcs-101-multiple-elements/), we see that the logic for 2oo2 voting is:

$$
\begin{equation}
P_A+P_B-P_AP_B
\end{equation}
$$

Substituting in the basic equation for the PFD of a 1oo1 system for each probability:

$$
\begin{align}
P_A+P_B-P_AP_B = (1-e^{-\lambda_A t})+(1-e^{-\lambda_B t})-(1-e^{-\lambda_A t})(1-e^{-\lambda_B t})
\end{align}
$$



Where  	&lambda;<sub>A</sub> and &lambda;<sub>B</sub> are the failure rates of the two devices. These are often taken to be the same, but lets keep them separate for now so as to be a bit more general. Multiplying through:

$$
\begin{align}
PFD &= 2 - e^{-\lambda_A t} - e^{-\lambda_B t} - [1 -e^{-\lambda_A t} - e^{-\lambda_B t} + e^{-(\lambda_A +\lambda_B) t}] \\ \\
&= 1 - e^{-(\lambda_A +\lambda_B) t}
\end{align}
$$

Taking the lambdas to be the same we get:


$$
\begin{equation}
PFD =  1 - e^{-2\lambda t}
\end{equation}
$$

### 2oo2 Analytical PFD Average

Finding the average, assuming different lambdas for each device:

$$
\begin{align}
PFD_{avg} &= \frac{1}{T} \int_{0}^{T} 1 -e^{-(\lambda_A+\lambda_B) t} \,dt \\ \\
 &= \frac{1}{T} * \left[t + \frac{e^{-(\lambda_A+ \lambda_B) t}}{\lambda_A+\lambda_B} \right] _0^T \\ \\
 &= \frac{1}{T} * \left[T + \frac{e^{-(\lambda_A+ \lambda_B) T}}{\lambda_A+\lambda_B} - \frac{1}{\lambda_A+\lambda_B} \right] \\ \\
 &= 1 + \frac{e^{-(\lambda_A+ \lambda_B) T}-1}{(\lambda_A+\lambda_B) T}
\end{align}
$$

Taking the lambdas to be the same:

$$
\begin{equation}
PFD_{Avg} = 1 + \frac{e^{-2\lambda T}-1}{2\lambda T}
\end{equation}
$$

### SymPy

I think we are getting the idea at this point. To avoid the tedium and inevitable mistakes from doing all this algebra, we are going to use [SymPy](https://www.sympy.org/en/index.html) to finish things up. SymPy is a [computer algebra system](https://en.wikipedia.org/wiki/Computer_algebra_system) written for python. The installation is pretty easy to follow along with if you are familiar with [python](https://www.python.org/downloads/), and if you aren't, keep in mind that SymPy has a [live shell](https://www.sympy.org/en/shell.html) you can use without installing anything.

The computer can sometimes represent formulas in ways that seem odd to a person. I will try and clean it up as much as possible, but sometimes it's good to be flexible. For example, when having it compute the 1oo2 PFD Avg formula, it produces:

$$
\begin{equation}
PFD_{Avg} = 1 - \frac{3}{2 \lambda T} + \frac{2 e^{- \lambda T}}{\lambda T} - \frac{e^{- 2\lambda T}}{2 \lambda T}
\end{equation}
$$

Comparing this with our result above we see that:

$$
\begin{align}
PFD_{Avg} &= 1 + \frac{2e^{-\lambda T}-2}{\lambda T} + \frac{1-e^{-2\lambda T}}{2\lambda T} \\ \\
&= 1+\frac{2e^{-\lambda T}}{\lambda T} - \frac{2}{\lambda T}+ \frac{1}{2\lambda T}- \frac{e^{-2\lambda T}}{2\lambda T} \\ \\
&= 1+\frac{2e^{-\lambda T}}{\lambda T} - 2*\frac{1}{\lambda T}+ \frac{1}{2}*\frac{1}{\lambda T}- \frac{e^{-2\lambda T}}{2\lambda T} \\ \\
&= 1+\frac{2e^{-\lambda T}}{\lambda T} - \frac{3}{2}*\frac{1}{\lambda T}- \frac{e^{-2\lambda T}}{2\lambda T}
\end{align}
$$

And we see that the two formulas are the same.

I will provide the SymPy script at the end of this post.


### 1oo3 Analytical PFD

We are going to skip writing out the steps at this point. The general idea is the same as above, use the logic from the [multiple elements post](/2020/12/10/sil-calcs-101-multiple-elements/) to obtain the pfd equation, and then find it's average.

Results from SymPy:

$$
\begin{equation}
PFD= 1 - e^{- \lambda_{C} t} - e^{- \lambda_{B} t} + e^{- \lambda_{B} t} e^{- \lambda_{C} t} - e^{- \lambda_{A} t} + e^{- \lambda_{A} t} e^{- \lambda_{C} t} + e^{- \lambda_{A} t} e^{- \lambda_{B} t} - e^{- \lambda_{A} t} e^{- \lambda_{B} t} e^{- \lambda_{C} t}
\end{equation}
$$

Assuming lambdas are the same:

$$
\begin{equation}
PFD=1 - 3 e^{- \lambda t} + 3 e^{- 2 \lambda t} - e^{- 3 \lambda t}
\end{equation}
$$

### 1oo3 Analytical PFD Average

Results from SymPy:

$$
\begin{equation}
PFD_{Avg} = \frac{T + \frac{-1 + e^{- \lambda_{A} T} e^{- \lambda_{B} T} e^{- \lambda_{C} T}}{\lambda_{A} + \lambda_{B} + \lambda_{C}} + \frac{1 - e^{- \lambda_{A} T} e^{- \lambda_{B} T}}{\lambda_{A} + \lambda_{B}} + \frac{1 - e^{- \lambda_{A} T} e^{- \lambda_{C} T}}{\lambda_{A} + \lambda_{C}} + \frac{1 - e^{- \lambda_{B} T} e^{- \lambda_{C} T}}{\lambda_{B} + \lambda_{C}} + \frac{-1 + e^{- \lambda_{C} T}}{\lambda_{C}} + \frac{-1 + e^{- \lambda_{B} T}}{\lambda_{B}} + \frac{-1 + e^{- \lambda_{A} T}}{\lambda_{A}}}{T}
\end{equation}
$$

Assuming lambdas are the same:

$$
\begin{equation}
PFD_{Avg}= 1 - \frac{11}{6 \lambda T} + \frac{3 e^{- \lambda T}}{\lambda T} - \frac{3 e^{- 2 \lambda T}}{2 \lambda T} + \frac{e^{- 3 \lambda T}}{3 \lambda T}
\end{equation}
$$

### 3oo3 Analytical PFD

Results from SymPy:

$$
\begin{equation}
PFD=1 - e^{- \lambda_{A} t} e^{- \lambda_{B} t} e^{- \lambda_{C} t}
\end{equation}
$$

Assuming lambdas are the same:

$$
\begin{equation}
PFD=1 - e^{- 3 \lambda t}
\end{equation}
$$

### 3oo3 Analytical PFD Average

Results from SymPy:

$$
\begin{equation}
PFD_{Avg}=\frac{T + \frac{e^{- \lambda_{A} T - \lambda_{B} T - \lambda_{C} T} - 1}{\lambda_{A} + \lambda_{B} + \lambda_{C}}}{T}
\end{equation}
$$

Assuming lambdas are the same:

$$
\begin{equation}
PFD_{Avg}=1 - \frac{1}{3 \lambda T} + \frac{e^{- 3 \lambda T}}{3 \lambda T}
\end{equation}
$$

### 2oo3 Analytical PFD

Results from SymPy:

$$
\begin{equation}
PFD=1 - e^{- \lambda_{B} t} e^{- \lambda_{C} t} - e^{- \lambda_{A} t} e^{- \lambda_{C} t} - e^{- \lambda_{A} t} e^{- \lambda_{B} t} + 2 e^{- \lambda_{A} t} e^{- \lambda_{B} t} e^{- \lambda_{C} t}
\end{equation}
$$

Assuming lambdas are the same:

$$
\begin{equation}
PFD=1 - 3 e^{- 2 \lambda t} + 2 e^{- 3 \lambda t}
\end{equation}
$$

### 2oo3 Analytical PFD Average

Results from SymPy:

$$
\begin{equation}
PFD_{Avg}=\frac{T + \frac{2 - 2 e^{- T \left(\lambda_{A} + \lambda_{B} + \lambda_{C}\right)}}{\lambda_{A} + \lambda_{B} + \lambda_{C}} + \frac{e^{- \lambda_{B} T - \lambda_{C} T} - 1}{\lambda_{B} + \lambda_{C}} + \frac{e^{- \lambda_{A} T -            \lambda_{C} T} - 1}{\lambda_{A} + \lambda_{C}} + \frac{e^{- \lambda_{A} T - \lambda_{B} T} - 1}{\lambda_{A} + \lambda_{B}}}{T}
\end{equation}
$$

Assuming lambdas are the same:

$$
\begin{equation}
1 - \frac{5}{6 \lambda T} + \frac{3 e^{- 2 \lambda T}}{2 \lambda T} - \frac{2 e^{- 3 \lambda T}}{3 \lambda T}
\end{equation}
$$

### SymPy Script

Here is the script that I used to calculate these:

~~~python
from sympy import *

init_printing()

# here "L" is being used for lambda, T is test interval
t, L, L_A, L_B, L_C, T = symbols('t L L_A L_B L_C T', positive=True)


# 1oo1
pfd_1oo1 = 1 - exp(-L * t)  # by assumption
integral_1oo1 = integrate(pfd_1oo1, (t, 0, T))  # integrate over test interval
avg_1oo1 = simplify(integral_1oo1 / T)
print("PFD_1oo1: " + str(latex(pfd_1oo1)))  # generate latex for pfd
print("PFD_Avg_1oo1: " + str(latex(avg_1oo1)))  # generate latex for pfd avg


# 1oo2 unique lambdas
pfd_1oo1_A = 1 - exp(-L_A * t)  # 1oo1 device with lambda = L_A
pfd_1oo1_B = 1 - exp(-L_B * t)  # 1oo1 device with lambda = L_B
pfd_1oo2 = expand(pfd_1oo1_A * pfd_1oo1_B)  # logic for probability of 1oo2
# integrate over test interval, collect like terms
integral_1oo2 = collect(integrate(pfd_1oo2, (t, 0, T)), [1 / L_A, 1 / L_B])
args = list(integral_1oo2.args)  # get the list of terms in the integrated expression
args[2] = factor(integral_1oo2.args[2])  # need to factor this term to make it look pretty
# remake the integral with the factored term, collect like terms
integral_1oo2 = collect(integral_1oo2.func(*tuple(args)), 1 / (L_A + L_B))
avg_1oo2 = integral_1oo2 / T
print("PFD_1oo2 unique lambdas: " + str(latex(pfd_1oo2)))  # generate latex for pfd
print("PFD_Avg_1oo2 unique lambdas: " + str(latex(avg_1oo2)))  # generate latex for pfd avg


# 1oo2 same lambdas
pfd_1oo2 = expand(pfd_1oo1 * pfd_1oo1)  # logic for probability of 1oo2
integral_1oo2 = integrate(pfd_1oo2, (t, 0, T))  # integrate over test interval
avg_1oo2 = simplify(integral_1oo2 / T)
print("PFD_1oo2 same lambdas: " + str(latex(pfd_1oo2)))  # generate latex for pfd
print("PFD_Avg_1oo2 same lambdas: " + str(latex(avg_1oo2)))  # generate latex for pfd avg


# 2oo2 unique lambdas
pfd_2oo2 = expand(pfd_1oo1_A + pfd_1oo1_B - pfd_1oo1_A * pfd_1oo1_B)  # logic for probability of 2oo2
integral_2oo2 = collect(integrate(pfd_2oo2, (t, 0, T)), 1 / (L_A + L_B))  # integrate over test interval
avg_2oo2 = integral_2oo2 / T
print("PFD_2oo2 unique lambdas: " + str(latex(pfd_2oo2)))  # generate latex for pfd
print("PFD_Avg_2oo2 unique lambdas: " + str(latex(avg_2oo2)))  # generate latex for pfd avg


# 2oo2 same lambdas
pfd_2oo2 = expand(pfd_1oo1 + pfd_1oo1 - pfd_1oo1 * pfd_1oo1)  # logic for probability of 2oo2
integral_2oo2 = collect(integrate(pfd_2oo2, (t, 0, T)), 1 / (2 * L))  # integrate over test interval
avg_2oo2 = integral_2oo2 / T
print("PFD_2oo2 same lambdas: " + str(latex(pfd_2oo2)))  # generate latex for pfd
print("PFD_Avg_2oo2 same lambdas: " + str(latex(avg_2oo2)))  # generate latex for pfd avg


# 1oo3 unique lambdas
pfd_1oo1_C = 1 - exp(-L_C * t)  # 1oo1 device with lambda = L_C
pfd_1oo3 = expand(pfd_1oo1_A * pfd_1oo1_B * pfd_1oo1_C)  # logic for probability of 1oo3
# integrate over test interval
integral_1oo3 = integrate(pfd_1oo3, (t, 0, T))
args = list(integral_1oo3.args)  # get the list of terms in the integrated expression
# factor each term individually
factored_args = []
for arg in args:
    factored_args.append(factor(arg))
# remake the integral with the factored terms, collect like terms
integral_1oo3 = collect(integral_1oo3.func(*tuple(factored_args)),
                        [1 / L_A, 1 / L_B, 1 / L_C, 1 / (L_A + L_B), 1 / (L_B + L_C), 1 / (L_A + L_C),
                         1 / (L_A + L_B + L_C)])
avg_1oo3 = integral_1oo3 / T
print("PFD_1oo3 unique lambdas: " + str(latex(pfd_1oo3)))  # generate latex for pfd
print("PFD_Avg_1oo3 unique lambdas: " + str(latex(avg_1oo3)))  # generate latex for pfd avg


# 1oo3 same lambdas
pfd_1oo3 = expand(pfd_1oo1 * pfd_1oo1 * pfd_1oo1)  # logic for probability of 1oo3
# integrate over test interval
integral_1oo3 = integrate(pfd_1oo3, (t, 0, T))
avg_1oo3 = simplify(integral_1oo3 / T)
print("PFD_1oo3 same lambdas: " + str(latex(pfd_1oo3)))  # generate latex for pfd
print("PFD_Avg_1oo3 same lambdas: " + str(latex(avg_1oo3)))  # generate latex for pfd avg


# 3oo3 unique lambdas
pfd_3oo3 = expand(pfd_1oo1_A + pfd_1oo1_B + pfd_1oo1_C - pfd_1oo1_A * pfd_1oo1_B - pfd_1oo1_A * pfd_1oo1_C -
                  pfd_1oo1_B * pfd_1oo1_C + pfd_1oo1_A * pfd_1oo1_B * pfd_1oo1_C)  # logic for probability of 3oo3
# integrate over test interval
integral_3oo3 = integrate(pfd_3oo3, (t, 0, T))
args = list(integral_3oo3.args)  # get the list of terms in the integrated expression
# factor each term individually
factored_args = []
for arg in args:
    factored_args.append(factor(arg))
# remake the integral with the factored terms, collect like terms
integral_3oo3 = powsimp(collect(integral_3oo3.func(*tuple(factored_args)), 1 / (L_A + L_B + L_C)))
avg_3oo3 = (integral_3oo3 / T)
print("PFD_3oo3 unique lambdas: " + str(latex(pfd_3oo3)))  # generate latex for pfd
print("PFD_Avg_3oo3 unique lambdas: " + str(latex(avg_3oo3)))  # generate latex for pfd avg


# 3oo3 same lambdas
pfd_3oo3 = expand(pfd_1oo1 + pfd_1oo1 + pfd_1oo1 - pfd_1oo1 * pfd_1oo1 - pfd_1oo1 * pfd_1oo1 -
                  pfd_1oo1 * pfd_1oo1 + pfd_1oo1 * pfd_1oo1 * pfd_1oo1)  # logic for probability of 3oo3
# integrate over test interval
integral_3oo3 = integrate(pfd_3oo3, (t, 0, T))

avg_3oo3 = simplify(integral_3oo3 / T)
print("PFD_3oo3 same lambdas: " + str(latex(pfd_3oo3)))  # generate latex for pfd
print("PFD_Avg_3oo3 same lambdas: " + str(latex(avg_3oo3)))  # generate latex for pfd avg


# 2oo3 unique lambas
# logic for probability of 2oo3
pfd_2oo3 = expand(pfd_1oo1_A * pfd_1oo1_B + pfd_1oo1_A * pfd_1oo1_C +
                  pfd_1oo1_B * pfd_1oo1_C - 2 * pfd_1oo1_A * pfd_1oo1_B * pfd_1oo1_C)
# integrate over test interval
integral_2oo3 = integrate(pfd_2oo3, (t, 0, T))
args = list(integral_2oo3.args)  # get the list of terms in the integrated expression
# factor each term individually
factored_args = []
for arg in args:
    factored_args.append(factor(arg))
# remake the integral with the factored terms, collect like terms
integral_2oo3 = powsimp(collect(integral_2oo3.func(*tuple(factored_args)),
                                [1 / (L_A + L_B + L_C), 1 / (L_A + L_B), 1 / (L_A + L_C), 1 / (L_B + L_C)]))
avg_2oo3 = (integral_2oo3 / T)
print("PFD_2oo3 unique lambdas: " + str(latex(pfd_2oo3)))  # generate latex for pfd
print("PFD_Avg_2oo3 unique lambdas: " + str(latex(avg_2oo3)))  # generate latex for pfd avg


# 2oo3 same lambas
# logic for probability of 2oo3
pfd_2oo3 = expand(pfd_1oo1 * pfd_1oo1 + pfd_1oo1 * pfd_1oo1 +
                  pfd_1oo1 * pfd_1oo1 - 2 * pfd_1oo1 * pfd_1oo1 * pfd_1oo1)
# integrate over test interval
integral_2oo3 = integrate(pfd_2oo3, (t, 0, T))
avg_2oo3 = simplify(integral_2oo3 / T)
print("PFD_2oo3 same lambdas: " + str(latex(pfd_2oo3)))  # generate latex for pfd
print("PFD_Avg_2oo3 same lambdas: " + str(latex(avg_2oo3)))  # generate latex for pfd avg

~~~
