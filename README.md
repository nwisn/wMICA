# About

wMICA is a weighted implementation of [Maximal Information Component Analysis](http://www.ncbi.nlm.nih.gov/pubmed/23487572). wMICA is used for the analysis of large interconnected networks and the identification of modules of similarly-acting nodes within the larger network.  It was designed specifically to work with gene expression datasets (RNA microarrays, RNAseq, etc), but is expandable to any relational network.  wMICA avoids two common pitfalls by using the Maximal Information instead of Pearson correlation to calulate node relatedness, which preserves non-linear relationships in the data, as well as a interaction component modeling process to allow each node to proportionally have membership in all modules.

More details are illustrated here:
* [poster pdf](https://drive.google.com/open?id=1CmBBdfQGh_QtdDi_gekoOF4GUSNgV1qw)
* [slides ppt](https://drive.google.com/open?id=1bW1rpSHmPUlcQPSWb5dE0AVkkXUJXkz6)

# Usage
Usage:  Download the .tar.gz package and add it to R as you would any other compressed package. For now, only works on UNIX-based systems (Mac/Linux)

There is a single master function `wMICA.Run()`, which optionally implements the following features:

* Edge weighting:  It is possible (and, in fact, highly recommended due to improved Gene Ontology Enrichments and module comprehensibility) to now add the calculated relationship score between two nodes to the module identification step.  This has been previously shown in other algorithms to dramatically improve the quality of the results and does the same here.

* Module Seeding:  If desired, the non-supervised nature of the algorithm may be compromised by allowing the user to 'seed' modules with certain genes to, for instance, pull down a module relating to a gene of interest or tease apart a pathway's interacting partners.

* Weighted GO Enrichment: which will harness the continuous nature of the module memberships to calculate GO enrichment without the need for a hard threshold. Now implemented as a separate package:  https://github.com/ChristophRau/GSAA

**KNOWN BUG**: if the last (or last several) genes in your dataset do not have strong enough MI scores to pass the threshold for inclusion in the algorithm, then an error will occur.  Deleting these columns will fix the problem.
