---
layout: post
title: >
    SIL Calcs 101: Beta Factor Application
image:
  path:    /assets/img/blog/beta8.png
  srcset:
    656w: /assets/img/blog/beta8.png


description: >
  Beta Factor Application Examples.
sitemap: true
excerpt_separator: <!--more-->
permalink: /2021/01/31/sil-calcs-101-beta-factor-application/

---

Enough talk, lets model something.
<!--more-->

[Last time](/2021/01/15/sil-calcs-101-beta-factor-intro/) we went through an introduction to beta factors. The relevant equation to extract from that is:

$$
\begin{equation}
\lambda_{DU} = \lambda_{I} + \lambda_{CC} = (1-\beta) \lambda_{DU}+\beta\lambda_{DU}
\end{equation}
$$

So we have split lambda up into two pieces: a common cause piece and a piece representing independent (i.e things fail together by random chance alone) events. Each piece will evolve separately in time according to our [basic equation](https://silcalcblog.com/2021/01/15/sil-calcs-101-beta-factor-intro/):

$$
\begin{equation}
PFD = 1-e^{-\lambda t}
\end{equation}
$$

This means we will be modeling two separate PFDs, the independent portion and the common cause portion.

$$
\begin{equation}
PFD_I = 1-e^{-\lambda_It}=1-e^{-(1-\beta)\lambda t}
\end{equation}
$$

$$
\begin{equation}
PFD_{CC} = 1-e^{-\lambda_{CC} t}=1-e^{-\beta \lambda t}
\end{equation}
$$

## Getting Set Up

Open up your [spreadsheet](https://docs.google.com/spreadsheets/d/1SqJResUO1NYUuvIac3PPjXDFfqtAoaUGrHxUln1ETXE/edit?usp=sharing) and setup a couple of cells to automatically split lambda based on beta, as shown below. We will assume we want to apply a 10% beta factor to the level switches.


<img srcset="/assets/img/blog/beta9.webp 1024w"
  sizes="(min-width: 800px) 50vw, 100vw"
  src="/assets/img/blog/beta9.webp"
  alt="beta factor sil calcs"
  loading="lazy" vspace="40" >

All I did here was set:

$$
\begin{equation}
\lambda_{I}= (1-\beta) \lambda_{DU}
\end{equation}
$$

and

$$
\begin{equation}
\lambda_{CC}= \beta \lambda_{DU}
\end{equation}
$$

Remember that these two pieces should sum to the original value of lambda!

## Modeling The Pieces

First, lets model the independent portion of lambda. We use our familiar (hopefully) [basic equation](https://www.silcalcblog.com/2020/11/22/sil-calcs-101-single-element-system/), like so:

<img srcset="/assets/img/blog/beta10.webp 1024w"
  sizes="(min-width: 800px) 50vw, 100vw"
  src="/assets/img/blog/beta10.webp"
  alt="modeling the independent portion of lambda"
  loading="lazy" vspace="40" >

Next, model the common cause portion of lambda, like so:

<img srcset="/assets/img/blog/beta11.webp 1024w"
  sizes="(min-width: 800px) 50vw, 100vw"
  src="/assets/img/blog/beta11.webp"
  alt="modeling the common cause portion of lambda"
  loading="lazy" vspace="40" >

## The Main Idea

In general, we are going to consider the PFD due to common causes as its own entity, and we are going to take it’s union with the PFD we get from modeling our voting structure. You will see what we mean as we go through.

## 1oo2 Voting w/ Beta

Let’s start by recalling how we model 1oo2 voting for independent events. From our [handy table](https://silcalcblog.com/2020/12/04/sil-calcs-101-venn-diagrams-introduction/):

$$
\begin{equation}
PFD_{1oo2}=P_A P_B
\end{equation}
$$

Now we union this with the PFD that results from modeling our λ<sub>CC</sub> :


$$
\begin{equation}
PFD_{1oo2}=P_A P_B + P_{CC}
\end{equation}
$$

Set this up like so:

<img srcset="/assets/img/blog/beta12.webp 1024w"
  sizes="(min-width: 800px) 50vw, 100vw"
  src="/assets/img/blog/beta12.webp"
  alt="1oo2 voting with beta factor"
  loading="lazy" vspace="40" >

That’s it! We’ve modeled a system that includes beta. Nothing to it. Notice that the PFD average for the 1oo2 system (shown below) with beta is larger than the PFD average for a 1oo2 system without beta. This is completely as expected, check out the [previous post](https://silcalcblog.com/2021/01/15/sil-calcs-101-beta-factor-intro/) if you need the details.

<img srcset="/assets/img/blog/beta13.webp 463w"
  sizes="(min-width: 800px) 50vw, 100vw"
  src="/assets/img/blog/beta13.webp"
  alt="1oo2 voting with beta factor"
  loading="lazy" vspace="40" >

## 2oo2 Voting w/ Beta

As mentioned [previously](https://silcalcblog.com/2021/01/15/sil-calcs-101-beta-factor-intro/), we don’t typically model beta in MooM systems in practice—because doing so would cause PFD average to decrease, which is a non-conservative result. That being said, I think it’s worth walking through the calculation once so that you can see the mechanics of how PFD average gets decreased, and also get in some extra practice doing calculations with beta.

First, recall our equation for modeling 2oo2 voting with independent events:

$$
\begin{equation}
PFD_{2oo2}=P_{A}+P_{B}-P_{AB}
\end{equation}
$$

Now union this with the common cause PFD:

$$
\begin{equation}
PFD_{2oo2}=P_{A}+P_{B}-P_{AB} + P_{CC}
\end{equation}
$$

Set up your spreadsheet like so:


<img srcset="/assets/img/blog/beta14.webp 1024w"
  sizes="(min-width: 800px) 50vw, 100vw"
  src="/assets/img/blog/beta14.webp"
  alt="2oo2 voting with beta factor"
  loading="lazy" vspace="40" >

Notice that, as expected, the PFD average of the 2oo2 system with beta is less than the PFD average of the system without beta.

<img srcset="/assets/img/blog/beta15.webp 573w"
  sizes="(min-width: 800px) 50vw, 100vw"
  src="/assets/img/blog/beta15.webp"
  alt="2oo2 voting with beta factor"
  loading="lazy" vspace="40" >

## 1oo3 Voting w/Beta

Alright lets do another! Recall the 1oo3 voting formula:

$$
\begin{equation}
PFD_{1oo3}=P_{A} P_{B} P_{C}
\end{equation}
$$

Now union with the common cause PFD:

$$
\begin{equation}
PFD_{1oo3}=P_{A} P_{B} P_{C} + P_{CC}
\end{equation}
$$

Set up like so:

<img srcset="/assets/img/blog/beta16.webp 723w"
  sizes="(min-width: 800px) 50vw, 100vw"
  src="/assets/img/blog/beta16.webp"
  alt="1oo3 voting with beta factor"
  loading="lazy" vspace="40" >

Results:


<img srcset="/assets/img/blog/beta17.webp 681w"
  sizes="(min-width: 800px) 50vw, 100vw"
  src="/assets/img/blog/beta17.webp"
  alt="1oo3 voting with beta factor"
  loading="lazy" vspace="40" >

## 3oo3 Voting w/ Beta

Recall the equation for independent case (note that I assumed all three level switches had identical lambdas here, and so condensed the equation due to space constraints):

$$
\begin{equation}
PFD_{3oo3}=3P_{A}-3P_A^2+P_A^3
\end{equation}
$$

Union with the common cause:

$$
\begin{equation}
PFD_{3oo3}=3P_{A}-3P_A^2+P_A^3+P_{CC}
\end{equation}
$$

Set up spreadsheet like so:

<img srcset="/assets/img/blog/beta18.webp 1024w"
  sizes="(min-width: 800px) 50vw, 100vw"
  src="/assets/img/blog/beta18.webp"
  alt="3oo3 voting with beta factor"
  loading="lazy" vspace="40" >

Results:


<img srcset="/assets/img/blog/beta19.webp 1024w"
  sizes="(min-width: 800px) 50vw, 100vw"
  src="/assets/img/blog/beta19.webp"
  alt="3oo3 voting with beta factor"
  loading="lazy" vspace="40" >

## What’s Next

That’s it for the introductory series, hopefully you have a basic handle on how to do some of this stuff now.

Next up, I am thinking a post on calculating [proof test](https://www.silcalcblog.com/2021/03/03/proof-test-coverage-calculations/) coverage would be useful.
