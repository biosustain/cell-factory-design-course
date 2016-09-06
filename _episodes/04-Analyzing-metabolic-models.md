---
title: "4. Analyzing metabolic models"
teaching: 30
exercises: 30
questions:
- How uniquely determined is the flux distribution returned by flux balance analysis?
- What is the optimal oxygen uptake rate at maximum growth?
objectives:
- Learn how to determine flux capacities using flux variability analysis.
- Learn how to generate phenotypic phase planes for different fluxes.
keypoints:
- "`flux_variability_analysis` calculates all the minimum and maximum fluxes that all reactions in a model can attain."
- "`flux_variability_analysis` has a keyword argument `fraction_of_optimum` that allows one to specify a fraction of the model's objective that needs to be achieved."
---

{% include nbviewer_iframe.html %}
