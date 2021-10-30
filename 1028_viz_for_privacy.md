# Visualisation for Privacy Preservation

* Introduce uncertainty to plots to balance preservations of privacy of individuals vs utility of the visualisation
    * Visual uncertainty: Encoding uncertainty + decoding uncertainty
* Measures of Privacy: Entropy, Mutual Info
* Measures of utility: clustering, preservation of patterns
* Considerations for interactivity of visualisations in leaking sensitive attributes (e.g. slicing)
* Prediction of attach scenarios

## Common methods to preserve privacy

### Hiding the data
* assess: spacial, temporal, tabular data?
* anonymise data first, e.g. k-anonymity, l-diversity, t-closeness, differential privacy
* spacial (e.g. Strava): hide coordinates of locations, e.g. merge original clusters to have at least n points/min max span distance, suppress location of landmarks
* spacial example - where do people tweet from? Aggregation into categories e.g. shopping, home, entertainment
* k-anonymity: Obfuscation applied so that k represents how many other records is a given record similar to. E.g. k=3 each record is equal to 3 other records. Attained by merging parallel lines to decrease granularity of line chart

### Masking the data
* cluster individual points to reduce granularity - range, overlaps
* pixel binning: pixel colour = attribute value

### Aggregating the data
* ranges, hierachical roll up
* consideration given to order of aggregation e.g. age then occupation or vice-versa?


