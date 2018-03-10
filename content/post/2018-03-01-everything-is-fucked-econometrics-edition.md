---
title: 'Everything is fucked: Econometrics Edition'
author: "Stijn"
date: '2018-03-01'
slug: everything-is-fucked-econometrics-edition
tags: []
categories:
- econometrics
- methodology
---

Following Sanjay Srivastava's (fake) [syllabus on pychological
research](https://hardsci.wordpress.com/2016/08/11/everything-is-fucked-the-syllabus/), I thought I summarise a couple of recent econometrics related papers with
a similar message.

### Clustered standard errors

The first paper by [Abadie, Athey, Imbens, and Wooldridge](http://www.nber.org/papers/w24003)
explains why we should think more carefully about the level at which clustering
of standard errors is applied (and if it is necessary at all). A good summary 
is found at the [Metrics Monday blog](http://marcfbellemare.com/wordpress/12712).

The take-a-way message is that clustering is not an empirical issue but a 
research design decisions. 

> Moreover, we show that the question whether, and at what level, to adjust
standard errors for clustering is a substantive question that cannot be informed
solely by the data (Abadie et al.)

What that means is that it is not enough to run the analysis with and without
clustered standard errors and check whether there is any difference.

There are two things two consider:

1. *Sampling:* If you randomly sample a subset of the clusters in the population
    and leave some out. A research design like that is not uncommon with hand
    collected data where the hand collected data is only collected for a subset
    of firms in the ASX200 but for multiple time periods. In this case, you
    should cluster at the firm level if you want to say something about the 
    ASX200 firms that are not in your dataset. This is probably the less
    important issue for most accounting and finance studies.
   
2. *Causal effect:* If you have a causal effect (e.g. a change in regulation),
    and that is administered to a cluster and not to individual observations, 
    you should cluster at that level. For instance, if you do a study with US
    data, and you look at a regulatory change in some states but not in other 
    states, you should cluster *at the state level*. Similar for cross-country
    studies.

PS: Adding fixed effects only absolves you of clustering standard errors if you
think that your causal effect is the same for each observation. That is if you
think that some firms will react differently to a change in regulation, fixed
effects don't solve the need for clustering.

### Instrumental variables.

The second one by
[Young](http://personal.lse.ac.uk/YoungA/ConsistencyWithoutInference.pdf)
focuses on (weak) instrumental variables and their standard errors. It does
not look very good for the traditional 2SLS estimators. 

The paper uses the bootstrap to test whether the standard errors of 2SLS are
appropriate. They are not. 2SLS underestimates the standard errors and leads
to more false positives. You should use the bootstrap to estimate standard 
errors of 2SLS. The intuition is that least squared standard errors are not very
robust to deviations from normally distributed residuals. The two equations 
in 2SLS multiply the bias in standard errors compared to the one equation in 
OLS. 

The paper actually show that in a lot of cases, you are better of to use regular
OLS than *2SLS with bootstrap*. Long story short, if you want to use 2SLS you
have to have a setting that resembles a natural experiment. 

### Residuals as dependent variables

The last one by [Chen, Hribar, and Melessa](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=2597429)
is especially relevant for the accountants.  The link is to the working paper.
The paper has been accepted in JAR. The paper deals with research designs
where in a first step, a researcher runs a regression to measure the unexpected 
component of a variable (e.g. abnormal returns, unexpected audit fees, 
unexpected earnings) and then in a second step the researcher runs a regression
on the unexpected component.

The basic problem is that if the independent variables from step 1 are not
included in step 2, you get biased estimates. The results suggests that there
are some false positives in the literature. The solution is relatively simple

1. Do not run two different regressions but run one regression with all 
    independent variables from step 1 and step 2.
2. If that is not possible, you can run 2 regressions but you have to use all
    independent variables from step 1 in step 2 regression. 




