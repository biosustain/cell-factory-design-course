---
title: "Calculating yields"
teaching: 30 min
exercises: 30 min
questions:
- How can I calculate the maximum possible yield for a desired product?
- How does product yield vary with growth?
objectives:
- Learn how to calculate molar, mass, and c-mol yields.
- "Use `phenotypic_phase_plane` to observe the product vs. growth tradeoff."
keypoints:
- "Set the exchange reaction of the product as the model objective using `model.objective`."
- "Optimize the model and divide the product flux by the carbon source uptake flux to determine the molar yield." 
---

{% include nbviewer_iframe.html %}
