---
layout: post
title: >
    Proof Test Coverage Calculations
image:
  path:    /assets/img/blog/ptc0.png
  srcset:
    611w: /assets/img/blog/ptc0.png


description: >
  Proof test coverage calculations
sitemap: true
excerpt_separator: <!--more-->
permalink: /2021/03/03/proof-test-coverage-calculations/
tags:       [proof testing]
---

Finally, it is time to talk about proof test coverage calcs! Recall that when we covered how to [model proof testing](https://www.silcalcblog.com/2020/12/20/sil-calcs-101-proof-testing/), we took the proof test coverage as an assumption, but no longer (kind of).
<!--more-->

Unfortunately it is still pretty difficult to get rid of assumptions, and there is a heavy reliance on vendor data, as we will see.

## Single Components

### Vendor & Generic Data

Figuring out the proof test coverage for a single component (an actuator, a valve, a level switch, etc.) is actually pretty easy, you just look it up. Let’s start with a valve, perhaps a [Jamesbury 9000 series ball valve](https://www.neles.com/products/valves/ball-valves/jamesbury-ball-valves/jamesbury-full-port-flanged-ball-valve-series-9000/). Typically, to evaluate the proof test coverage of a device, you’d like to have the safety manual and the safety certification for that product. Most likely you will need to ask the vendor for the latest copy of these materials, however, older copies are usually available online, so I am using that for this example.

The safety certification we are using for the Jamesbury 9000 gives us the following info:

<img srcset="/assets/img/blog/ptc1.webp 677w"
  sizes="(min-width: 800px) 50vw, 100vw"
  src="/assets/img/blog/ptc1.webp"
  alt="jamesbury 9000 safety cert"
  loading="lazy" vspace="40" >

From this we can read off our lambda (24 FITs), and our proof test coverage (85%). If 24 FITs seems a bit low to you (for comparison, the generic data low end for a ball valve is around 300 FITs, for valves that close on trip—see [SILSafeData](http://silsafedata.com/)), then you might want to consider substituting generic data in. Note that SILSafeData won’t give you the proof test coverage for generic equipment, I think you need to buy their books for that. It would be nice if anything in the SIS world was free (except this blog of course, no charge there).

The [safety manual](https://valveproducts.neles.com/documents/jamesbury/SafetyManuals/en/10SM_5_9000_en.pdf) for the valve tells us what we actually have to do as part of our proof test (to achieve the 85% coverage).

<img srcset="/assets/img/blog/ptc2.webp 670w"
  sizes="(min-width: 800px) 50vw, 100vw"
  src="/assets/img/blog/ptc2.webp"
  alt="jamesbury 9000 safety manual"
  loading="lazy" vspace="40" >

Basically we have to stroke test the valve, and give it a visual inspection.

### Data Sources

As is likely obvious from above, reliable data is the hardest part of determining the proof test coverage (and failure rate!) for a single component. You can trust the vendor certifications, you can pay for the generic data sets, or, if you are lucky, your organization may keep it’s own, internal data.

## Multiple Components

Let’s stick with the vendor data in this example. The next step is to figure out how proof test coverage for multiple devices combine. After all, when we go out and stroke our valve, we aren’t just testing the valve, but also it’s actuator, positioner, solenoids, etc. We need a way to understand how a proof test (stroking a valve) effects an entire system of components.

I find that a concrete example is often useful, so assume our safety function shuts off fuel gas to a furnace. This is a fairly standard safety function out in industry. Our system consists of a Jamesbury 9000 series ball valve, Neles B1J actuator, and Emerson DVC 6200. Note that I am ignoring the sensors and logic solver, because they are not components that are involved in the proof test of the valve.

### Actuator

We already covered the ball valve above; the actuator [safety manual](https://valveproducts.neles.com/documents/neles/SafetyManuals/en/10SM_B1_en.pdf) and certificate combine to furnish the following information (again, always obtain current documentation from your vendor, and then question it):

<img srcset="/assets/img/blog/ptc3.webp 670w"
  sizes="(min-width: 800px) 50vw, 100vw"
  src="/assets/img/blog/ptc3.webp"
  alt="actuator proof test"
  loading="lazy" vspace="40" >

  <img srcset="/assets/img/blog/ptc4.webp 696w"
  sizes="(min-width: 800px) 50vw, 100vw"
  src="/assets/img/blog/ptc4.webp"
  alt="actuator safety manual"
  loading="lazy" vspace="40" >


Again, it’s worth noting that [generic data](http://silsafedata.com/) puts the low bound on a pneumatic piston actuator failure rate at 120 FITs.

### Digital Valve Positioner

The final element we will need is our DVC, which serves as the interface between the electrical and pneumatic signals. [Safety manual](https://www.emerson.com/documents/automation/im-supplement-safety-manual-for-fieldvue-dvc6200-sis-digital-valve-controller-position-monitor-lcp200-local-control-panel-en-125602.pdf) and certification yield the following:

  <img srcset="/assets/img/blog/ptc5.webp 571w"
  sizes="(min-width: 800px) 50vw, 100vw"
  src="/assets/img/blog/ptc5.webp"
  alt="DVC safety manual"
  loading="lazy" vspace="40" >

 <img srcset="/assets/img/blog/ptc6.webp 615w"
  sizes="(min-width: 800px) 50vw, 100vw"
  src="/assets/img/blog/ptc6.webp"
  alt="DVC safety manual"
  loading="lazy" vspace="40" >

Where DETT stands for de-energize to trip, which is a pretty common setup.

### Calculating Coverage

Time for a new [spreadsheet](Time for a new spreadsheet! Let’s start by getting all of our information put in; set up a sheet like so:)! Let’s start by getting all of our information put in; set up a sheet like so:

 <img srcset="/assets/img/blog/ptc7.webp 607w"
  sizes="(min-width: 800px) 50vw, 100vw"
  src="/assets/img/blog/ptc7.webp"
  alt="proof test coverage spreadsheet"
  loading="lazy" vspace="40" >

Now enter the FITs and proof test coverages from above:

 <img srcset="/assets/img/blog/ptc8.webp 588w"
  sizes="(min-width: 800px) 50vw, 100vw"
  src="/assets/img/blog/ptc8.webp"
  alt="proof test coverage spreadsheet"
  loading="lazy" vspace="40" >

Compute the failures detected by multiplying the failure rate (FITs) by the proof test coverage:

 <img srcset="/assets/img/blog/ptc9.webp 569w"
  sizes="(min-width: 800px) 50vw, 100vw"
  src="/assets/img/blog/ptc9.webp"
  alt="proof test coverage spreadsheet"
  loading="lazy" vspace="40" >

Filling that down we get:

 <img srcset="/assets/img/blog/ptc10.webp 557w"
  sizes="(min-width: 800px) 50vw, 100vw"
  src="/assets/img/blog/ptc10.webp"
  alt="proof test coverage spreadsheet"
  loading="lazy" vspace="40" >

Calculation of proof test coverage is done by dividing the failures detected (technically failure rate since we are in FITs = failures per billion hours) by the total failure rate:

 <img srcset="/assets/img/blog/ptc11.webp 611w"
  sizes="(min-width: 800px) 50vw, 100vw"
  src="/assets/img/blog/ptc11.webp"
  alt="proof test coverage spreadsheet"
  loading="lazy" vspace="40" >

 <img srcset="/assets/img/blog/ptc12.webp 556w"
  sizes="(min-width: 800px) 50vw, 100vw"
  src="/assets/img/blog/ptc12.webp"
  alt="proof test coverage spreadsheet"
  loading="lazy" vspace="40" >


Notice that this isn’t a straight average of the proof test coverages of the individual components, it’s weighed by the number of failures. Components with high failure rates contribute more to the calculated proof test coverage than those with lower failure rates.

So, for the sake of argument, if I were to adjust the coverage on our ball valve to 99%, it doesn’t make that much difference to our overall PTC:

 <img srcset="/assets/img/blog/ptc13.webp 556w"
  sizes="(min-width: 800px) 50vw, 100vw"
  src="/assets/img/blog/ptc13.webp"
  alt="proof test coverage spreadsheet"
  loading="lazy" vspace="40" >

But, if I change the DVC to 99%, that makes a big difference:

 <img srcset="/assets/img/blog/ptc14.webp 556w"
  sizes="(min-width: 800px) 50vw, 100vw"
  src="/assets/img/blog/ptc14.webp"
  alt="proof test coverage spreadsheet"
  loading="lazy" vspace="40" >

The takeaway here isn’t that DVCs are more important to PTC than valves, its that whatever has the highest failure rate, makes the biggest difference.

## Improving Coverages

What if your proof test goes above and beyond what the vendor says is required (to achieve their stated proof test coverage). Well, we are getting into the arena of engineering judgement here, so what follows is a mostly qualitative description, but hopefully it is still helpful.

### Case 1: You Buy New

On one extreme, you could just throw the whole installation out and install all new components at every proof test interval. Costly, but you are pretty much guaranteeing you can claim 100% proof test coverage; everything is new, so logically you would start tracking failure rate from zero again.

## Case 2: You Overhaul Everything

You pull the valve (or the sensor, or whatever) and all it’s accessories and send them to the shop for a complete overhaul. All gaskets, O-rings, and other soft goods get replaced, surfaces get machined and smoothed, the valve is stroke tested in the shop, timed, leak tested, linkages are cleaned up and repaired if required, etc.

Now what proof test coverage do we claim?

This is a judgement call, but typically something high, like 95-100%. You should review the performance of your device after it’s overhauled, dig into the components of the device that are repaired and those that are not, and make a decision.

### Case 3: Mixed Overhaul, Replacement & Inline Tests

Fairly straightforward here, if you replace it then you treat it as 100% proof test coverage, overhauled components treated as per case 2, inline tests treated as in our main example above. Plug the respective coverages into the sheet and compute the total coverage for the assembly.

### Case 4: Something In-between

You’re not pulling and shopping the valve (or device, valves are just an easy example), but you’re still doing more than the vendor requires. Maybe you run a valve signature, leak test the valve inline, or perform some other type of inline repair or diagnostic.

Now what’s the coverage? This one is completely up to you, there are too many variables. How has the device performed in the past after similar inline repairs? Can you argue that the additional testing you are doing makes a measurable difference in the valve’s failure rate? Are you relying on the improved proof test coverage to pass your SIL calcs, or is it just gravy? (If it is, then maybe do the extra testing, but don’t take the credit for it)

That’s all I’ve got for now, [next time](https://www.silcalcblog.com/2021/03/13/partial-stroke-testing/) we will talk partial stroke testing coverage.






