---
title: "Getting started"
teaching: 15 min
exercises: 10 min
questions:
- How can I get started with metabolic models?
objectives:
- Load a model and simulate it.
- Obtain a model from a database for a host organism you're interested in and simulate it.
keypoints:
- `load_model` can be used to load a model.
- `model.solve()` simulates the model.
- `reaction.flux` contains the computed flux of the reaction.
- `model.solve()` also returns a solution object that contains the simulation results.
---

{% include nbviewer_iframe.html %}
