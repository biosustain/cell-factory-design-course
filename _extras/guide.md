---
layout: page
title: "Instructors' Guide"
permalink: /guide/
---

## Selective Display mirroring on OS X (useful for live coding)
<http://create.pro/blog/how-to-mirror-specific-displays-in-os-x-mirror-some-but-not-all-of-your-monitors-on-an-apple-system/>

## Solutions

### 04-Analyzing-metabolic-models

#### Exercise 1.1

    percentage = (0.7 / model.solve().f) * 100
    result_80perc_max_obj = flux_variability_analysis(model, fraction_of_optimum=percentage/100, remove_cycles=True)
    result_80perc_max_obj.plot(index=result_80perc_max_obj.data_frame.index, height=1200)

#### Exercise 1.2

    flux_sums = []
    optimum_percentages = range(50, 105, 5)
    for i in optimum_percentages:
        df = flux_variability_analysis(model, fraction_of_optimum=i/100, remove_cycles=True).data_frame
        flux_sum = sum(abs(df.lower_bound - df.upper_bound))
        print("{}%: ".format(i), flux_sum)
        flux_sums.append(flux_sum)

    import matplotlib.pyplot as plt
    plt.plot(optimum_percentages, flux_sums)
    plt.xlabel('Optimum (%)')
    plt.ylabel('Flux sum [mmol gDW^-1 h^-1]')
    plt.show()

#### Exercise 2

    result = flux_variability_analysis(model, remove_cycles=True)
    result.data_frame[(result.data_frame.lower_bound == 0) & (result.data_frame.upper_bound == 0)]


#### Exercise 3

    result = phenotypic_phase_plane(model,
                                    variables=[model.reactions.EX_o2_e],
                                    objective=model.reactions.BIOMASS_Ecoli_core_w_GAM)
    result.plot()


### 06-Gene-essentiality

#### Exercise 1

    wt_growth_rate = model.solve().objective_value
    essential = 0
    reduced_growth = 0
    same_growth = 0
    for gene, growth in essentiality.items():
        if growth < 0.05:
            essential = essential + 1
        elif growth > wt_growth_rate * .95:
            same_growth = same_growth + 1
        else:
            reduced_growth = reduced_growth + 1
    print(essential)
    print(reduced_growth)
    print(same_growth)

#### Exercise 2

    result = {}
    with TimeMachine() as tm:
    model.reactions.EX_glc__D_e.change_bounds(0, 0, time_machine=tm)
    for source in carbon_exchanges:
        with TimeMachine() as tm3:
            print('Determining essentiality for: ' + source)
            result[source] = {}
            model.reactions.get_by_id(source).change_bounds(-20, 0, time_machine=tm3)
            for gene in model.genes:
                with TimeMachine() as tm2:
                    gene.knock_out(time_machine=tm2)
                    try:
                        solution = model.solve()
                    except exceptions.Infeasible:
                        result[source][gene] = 0.
                    else:
                        result[source][gene] = solution.objective_value


    from pandas import DataFrame

    df = DataFrame.from_dict(result)

    import matplotlib.pyplot as plt

    binary_df = df.applymap(lambda x: 0 if x < 0.05 else 1)

    ax = plt.matshow(binary_df, cmap='gray').axes
    ax.set_aspect(.05)
    ax.grid(color='gray')
    ax.set_xlabel('Carbon sources')
    ax.set_ylabel('Genes')
    ax.figure.set_figwidth(8)

### 07-Theoretical-maximum-yields

#### Exercise 1

C-mol yield

    (model.reactions.EX_ac_e.flux * model.metabolites.ac_c.elements['C']) / (-1. * model.reactions.EX_glc__D_e.flux * model.metabolites.glc__D_e.elements['C'])

Mass yield

    (model.reactions.EX_ac_e.flux * model.metabolites.ac_c.formula_weight) / (-1. * model.reactions.EX_glc__D_e.flux * model.metabolites.glc__D_e.formula_weight)


#### Exercise 2

Biomass mass yield

    gDW_biomass_per_g_glucose = gDW_biomass_per_mmol_glucose * (1000 / model.metabolites.glc__D_e.formula_weight)
    gDW_biomass_per_g_glucose

#### Excercise 3

    product_fluxes = []
    model.objective = model.reactions.EX_ac_e
    for growth in growth_rates:
        model.reactions.BIOMASS_Ec_iJO1366_core_53p95M.change_bounds(growth, growth)
        product_fluxes.append(model.solve().objective_value)
    product_fluxes = array(product_fluxes)

### Episode 09

#### Solution 1

    mutant1.reactions.EX_o2_e.lower_bound = -20
    ppp = phenotypic_phase_plane(mutant1,
                                 variables=[mutant1.reactions.BIOMASS_Ecoli_core_w_GAM],
                                 objective=mutant1.reactions.EX_succ_e)

    ppp.plot()

    mutant2.reactions.EX_o2_e.lower_bound = -20
    ppp = phenotypic_phase_plane(mutant2,
                                 variables=[mutant2.reactions.BIOMASS_Ecoli_core_w_GAM],
                                 objective=mutant2.reactions.EX_succ_e)

    ppp.plot()

    mutant3.reactions.EX_o2_e.lower_bound = -20
    ppp = phenotypic_phase_plane(mutant3,
                                 variables=[mutant3.reactions.BIOMASS_Ecoli_core_w_GAM],
                                 objective=mutant3.reactions.EX_succ_e)

    ppp.plot()


#### Solution 2

    mutant3.reactions.ACALD.gene_name_reaction_rule

    mutant3.reactions.LDH_D.gene_name_reaction_rule

    for gene in mutant3.reactions.ACALD.genes:
        print(gene.name, gene.reactions)

    for gene in mutant3.reactions.LDH_D.genes:
        print(gene.name, gene.reactions)

    mutant4 = model.copy()
    mutant4.reactions.ACALD.knock_out()
    mutant4.reactions.LDH_D.knock_out()
    mutant4.reactions.ALCD2x.knock_out()

    ppp = phenotypic_phase_plane(mutant4,
                                 variables=[mutant4.reactions.BIOMASS_Ecoli_core_w_GAM],
                                 objective=mutant4.reactions.EX_succ_e)

    ppp.plot()
