---
title: 'Improving Bioschemas creation and community adoption through process improvements and tool development, and advancing compliance to FAIR standards'
tags:
  - Bioschemas 
  - Schema.org 
  - FAIR 
authors:
  - name: First Last
    orcid: 0000-0000-0000-0000
    affiliation: 1
  - name: Alban Gaignard
    orcid: 0000-0002-3597-8557
    affiliation: 2

affiliations:
 - name: Institution 1, address, city, country
   index: 1
 - name: Nantes Université, CNRS, INSERM, l’institut du thorax, Nantes F-44000, France
   index: 2
date: 27 November 2023
bibliography: paper.bib
authors_short: Last et al. (2023) BioHackrXiv  template
group: BioHackrXiv
event: BioHackathon Europe 2023
---

# Introduction
## Background

Nowadays scientists massively produce diverse datasets in many communities. They need to combine them to answer scientific or novel questions. To do so, these diverse computational resources need first to be found by search engines. 

Bioschemas [@Gray2017BioschemasFP] is a simple and lightweight mechanism to annotate online resources in a standardized way and expose key metadata. 

## Objectives

In our project, we have a number of threads. Firstly we aim to ease adoption for new users by providing appropriate tooling. Therefore, we will be working on technically connecting the [Data Discovery Engine](https://discovery.biothings.io) to the [Bioschemas](https://bioschemas.org) website. Ultimately this will enable us to more easily generate machine readable types and profiles for existing and NEW communities. This will, for example, enable us to more easily develop new profiles working with plant, biodiversity and machine learning communities on their minimal sets of metadata. 

Secondly we have a  “mining” strand of work, where we will examine and collate existing web resources with bioschemas mark up, both to ascertain overall usage and compliance, and identify common issues or misuse.

Furthermore, we will also try and make our work more palatable for other research communities,  by sharing domain-agnostic standards through the schemas.science site. 

We are very happy to welcome web designers, developers, and experts in knowledge engineering, as well as domain experts interested in making progress on FAIRification. 


## Subsection level 2

Please keep sections to a maximum of three levels, even better if only two levels.

### Subsection level 3

Please keep sections to a maximum of three levels.

## Tables, figures and so on

Please remember to introduce tables (see Table 1) before they appear on the document. We recommend to center tables, formulas and figure but not the corresponding captions. Feel free to modify the table style as it better suits to your data.

Table 1
| Header 1 | Header 2 |
| -------- | -------- |
| item 1 | item 2 |
| item 3 | item 4 |

Remember to introduce figures (see Figure 1) before they appear on the document. 


# Results 
## Bioschemas usage analysis through Live Deploys 

The first part of this work consisted in assembling an RDF dataset based on the Bioschemas 140 live deploys URLS[^ld]

We developed a command line application supported by the FAIR-Checker[@Gaignard2023FAIRCheckerSD] API that harvests Bioschemas markup for a given web page and store the markup in an RDF file. This results in an RDF graph with 74 245 Schema.org triples[^rdf_crawl]. 

We automated the metadata harvesting through a weekly run GitHub action[^gh]. 

[^ld]: https://bioschemas.org/developer/liveDeploys
[^rdf_crawl]: https://github.com/BioSchemas/bioschemas-validation/tree/main/data 
[^gh]: https://github.com/BioSchemas/bioschemas-validation/blob/main/.github/workflows/gen_live_deploy_reports.yml

Table 1 and Table 2 report the top-20 most used classes and properties. In these table we can also identify some misspelling of Schema.org classes, and properties (e.g. @Type, DataSet)

Table 1. Top-20 most used Schema.org classes in Bioschemas live deploys. 
| Class | Count |
| -------- | -------- |
| http://schema.org/CreativeWork	| 14916 |
| http://schema.org/BioChemEntity	| 1085 |
| http://schema.org/DataDownload	| 910 |
| http://schema.org/creativeWork	| 714 |
| https://bioschemas.org/Taxon	| 714 |
| http://schema.org/Dataset	| 524 |
| http://schema.org/Organization	| 307 |
| http://schema.org/Person	| 256 |
| http://schema.org/DefinedTerm	| 159 |
| http://schema.org/MolecularEntity	| 113 |
| http://schema.org/DataSet	| 78 |
| http://schema.org/TaxonName	| 70 |
| http://schema.org/ChemicalSubstance	| 68 |
| http://schema.org/SequenceAnnotation	| 62 |
| http://schema.org/ScholarlyArticle	| 50 |
| http://schema.org/PropertyValue	| 47 |
| http://schema.org/SequenceRange	| 40 |
| http://schema.org/DataCatalog	| 32 |
| http://schema.org/PostalAddress	| 30 |
| http://schema.org/WebPage	| 28  |

Table 2. Top-20 most used Schema.org properties in Bioschemas live deploys. 
| Property | Count |
| -------- | -------- |
| http://www.w3.org/1999/02/22-rdf-syntax-ns#type | 20595 |
| http://schema.org/name | 20537 |
| http://schema.org/url | 12281 |
| http://schema.org/about | 5716 |
| http://schema.org/identifier | 1616 |
| http://schema.org/taxonRank | 1158 |
| http://schema.org/taxonomicRange | 1083 |
| http://schema.org/parentTaxon | 1078 |
| http://schema.org/@Type | 1074 |
| http://schema.org/studySubject | 1074 |
| http://schema.org/distribution | 916 |
| http://schema.org/description | 607 |
| http://schema.org/keywords | 578 |
| http://purl.org/dc/terms/conformsTo | 562 |
| http://schema.org/version | 444 |
| http://schema.org/author | 311 |
| http://schema.org/license | 200 |
| http://schema.org/contentURL | 178 |
| http://schema.org/creator | 164 | 
| http://schema.org/sameAs | 161 | 


Then, for each of the live deploy URLs, we computed the number of `dct:conformsTo` properties. Figure 1 highlights that a majority of live deploys do not expose `dct:conformsTo` properties. Since this proerti allows to link a Bioschemas profile to a set of Bioschemas annotations, this becomes problematic at the time of computationally validating the profiles. 

![dct:conformsTo properties](figures/conformsTo.png)
Figure 1. More than 60 live deploys expose dct:conformsTo properties whereas this property is absent for more than 70 live deploys. 

All these figures can be reproduced by re-executing the publicly available Jupyter notebooks[^nb_dumps][^nb_harvest]. 

[^nb_dumps]: https://github.com/BioSchemas/bioschemas-validation/blob/main/scripts/LiveDeploys-dump.ipynb
[^nb_harvest]: https://github.com/BioSchemas/bioschemas-validation/blob/main/scripts/Plots-Harvesting.ipynb

### Profile-based analysis
![most used profiles](figures/mostUsedProfiles.png)
Figure 2. Most used Bioschemas profiles in live deploys. 

For each of the live deploys we reused teh FAIR-Checker API to validate the profiles specified with `dct:conformsTo` properties. Figure 3 reports the number of *errors*, meaning that required properties are missing, and Figure 4 reports the number of *warnings*, meaning that recommended properties are missing. The numbers of *errors*/*warnings* have been normalized by the number of profile instances. 

![profiles with errors](figures/profErrors.png)
Figure 3. Bioschemas profiles showing the highest number of missing required properties.  

![profiles with warnings](figures/profWarnings.png)
Figure 4. Bioschemas profiles showing the highest number of missing recommended properties.  

All these figures can be reproduced by re-executing the publicly available Jupyter notebook[^nb_prof]. 

[^nb_prof]: https://github.com/BioSchemas/bioschemas-validation/blob/main/scripts/Plots-Validation.ipynb

### Property-based analysis


# Discussion and/or Conclusion

We recommend to include some discussion or conclusion about your work. Feel free to modify the section title as it fits better to your manuscript.

# Future work

And maybe you want to add a sentence or two on how you plan to continue. Please keep reading to learn about citations and references.

For citations of references, we prefer the use of parenthesis, last name and year. If you use a citation manager, Elsevier – Harvard or American Psychological Association (APA) will work. If you are referencing web pages, software or so, please do so in the same way. Whenever possible, add authors and year. We have included a couple of citations along this document for you to get the idea. Please remember to always add DOI whenever available, if not possible, please provide alternative URLs. You will end up with an alphabetical order list by authors’ last name.

# Jupyter notebooks, GitHub repositories and data repositories

* Bioschemas validation repo: https://github.com/BioSchemas/bioschemas-validation
* 

# Acknowledgements
Please always remember to acknowledge the BioHackathon, CodeFest, VoCamp, Sprint or similar where this work was (partially) developed.

# References

Leave thise section blank, create a paper.bib with all your references.
