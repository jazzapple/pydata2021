# Start Asking your Data "Why?" - A Gentle Intro to Causal Inference

* Slides: https://bit.ly/start-ask-why
* Judea Pearl - godfather of causal inference - "Pearls' Causality Ladder"
* Simpsons Calculator: bit.ly/simpson-calculator

## Limitations of correlations
* results from correlation can be inconclusive or at worst misleading
* e.g. decrease drowning: ice cream sales are strongly correlated, but not a cause. Weather , supply all impact.
* e.g. fire alarms detect smoke, not fire
* can be used to mask true causation e.g. smoking and lung cancer

## Simpsons Paradox / Lords Paradox (continuous vars)
* classic case of data misinterpretation
* contradication between results of full population vs subpopulations: trends can exist in subgroups that are contradictory to the population
* confounding variables can cause this, e.g. gender, **so need to be controlled for**
    * ACE: Average Causal Effect - weighting applied to adjust for confounding variable to adjust in the popualtion at large
    * RD: Risk difference refers to cohort

## Graph Models - visualise story behind the data
* Help make educated decisions about which variables we should be controlling for, by identifying dependencies between parameters (including experiment group)
* nodes/vertices: variables
* edges; communication "who is related to who) - correlations, joint proabilities. Directional in the case of causation
* DAG: no cyclical edges back to same node

## Pearl's causality ladder
1. Just as seeing my be decieving, correlation/association may be misinterpreted (Simpsons, spurious correlations)
2. Sentinents learn causation by doing. By controlling for confounders (e.g via ACE), we may infer causality for sub populations. Topic: do algebra
3. Imagining "What If" hypothetical conditioning, may provide causal insights for individuals. Topic: counterfactuals

