---
title: Meta-analysis for within-study and across-study biases
layout: archive
author_profile: false
output:
  md_document:
    variant: gfm
    preserve_yaml: true
---

## How to use this website

This website provides interactive apps to conduct bias corrections and
sensitivity analyses for meta-analyses with respect to within-study and
across-study biases.

### Publication bias

This app conducts sensitivity analyses for publication bias in
meta-analyses.

These analyses consider publication bias that favors affirmative studies
(i.e., those with positive estimates and significant p-values) over
nonaffirmative studies (i.e., those with negative or nonsignificant
estimates). These analyses enable statements such as: “For publication
bias to shift the observed point estimate to the null, significant
results would need to be at least 30-fold more likely to be published
than negative or nonsignificant results.” Alternatively, you can
consider shifting to a chosen non-null value or shifting the confidence
interval to include the null or another value.

This app also provides a worst-case meta-analytic point estimate under
maximal publication bias obtained simply by conducting a standard
meta-analysis of only the negative and nonsignificant studies.

Please use the following citation:

<a href="https://rss.onlinelibrary.wiley.com/doi/10.1111/rssc.12440" rel="nofollow noopener noreferrer" target="_blank">
Mathur MB & VanderWeele TJ (2020). Sensitivity analysis for publication
bias in meta-analyses. *Journal of the Royal Statistical Society: Series
C*, 69(5), 1091-1119. </a>

### *p*-hacking

This app fits right-truncated meta-analysis (RTMA), a bias correction
for the joint effects of *p*-hacking (i.e., manipulation of results
within studies to obtain significant, positive estimates) and
traditional publication bias (i.e., the selective publication of studies
with significant, positive results) in meta-analyses.

Unlike publication bias alone, *p*-hacking that favors significant,
positive results (termed “affirmative”) can distort the distribution of
affirmative results. To bias-correct results from affirmative studies
would require strong assumptions on the exact nature of *p*-hacking. In
contrast, joint *p*-hacking and publication bias do not distort the
distribution of published nonaffirmative results when there is stringent
*p*-hacking (e.g., investigators who hack always eventually obtain an
affirmative result) or when there is stringent publication bias (e.g.,
nonaffirmative results from hacked studies are never published). This
means that any published nonaffirmative results are from unhacked
studies. Under these assumptions, RTMA involves analyzing only the
published nonaffirmative results to essentially impute the full
underlying distribution of all results prior to selection due to
*p*-hacking and/or publication bias.

Please use the following citation:

<a href="https://doi.org/10.31219/osf.io/ezjsx" rel="nofollow noopener noreferrer" target="_blank">
Mathur MB (2022). Sensitivity analysis for *p*-hacking in meta-analyses.
</a>

## Bug reports

Submit bug reports by opening an issue on GitHub:

<div class="page__footer-follow">

<ul class="social-icons">
<li>
<a href="https://github.com/mikabr/pubbias-app" rel="nofollow noopener noreferrer" target="_blank"><i class="fab fa-fw fa-github" aria-hidden="true"></i>
mikabr/pubbias-app</a>
</li>
<li>
<a href="https://github.com/mikabr/phacking-app" rel="nofollow noopener noreferrer" target="_blank"><i class="fab fa-fw fa-github" aria-hidden="true"></i>
mikabr/phacking-app</a>
</li>
</ul>

</div>
