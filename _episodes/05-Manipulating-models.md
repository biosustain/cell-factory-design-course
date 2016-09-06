---
title: "5. Manipulating models"
teaching: 30
exercises: 30
questions:
- How can I add missing reactions to a model?
- How can I delete a gene from a model?
objectives:
- Understanding the basic mechanisms of adding and removing content from a model.
keypoints:
- "`cameo.util.TimeMachine` provides a convenient way to undo changes to models in order to avoid copies."
- "`reaction.change_bounds` allows one to change the lower and upper bound of reaction simultaneously."
- "`Reaction` and `Metabolite` can be used to define reactions."
- "`model.add_reaction(reaction)` adds reaction to model."
---

{% include nbviewer_iframe.html %}
