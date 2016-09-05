---
layout: page
title: "Instructors' Guide"
permalink: /guide/
---

## Selective Display mirroring on OS X (useful for live coding)
<http://create.pro/blog/how-to-mirror-specific-displays-in-os-x-mirror-some-but-not-all-of-your-monitors-on-an-apple-system/>

## Solutions
### 04-Analyzing-metabolic-models

#### Exercise 1
    percentage = (0.7 / model.solve().f) * 100
    result_80perc_max_obj = flux_variability_analysis(model, fraction_of_optimum=percentage/100, remove_cycles=True)
    result_80perc_max_obj.plot(index=result_80perc_max_obj.data_frame.index, height=1200)
#### Exercise 2

flux_sums = []
optimum_percentages = range(50, 105, 5)
for i in optimum_percentages:
    df = flux_variability_analysis(model, fraction_of_optimum=i/100, remove_cycles=True).data_frame
    flux_sum = sum(abs(df.lower_bound - df.upper_bound))
    print("{}%: ".format(i), flux_sum)
    flux_sums.append(flux_sum)
