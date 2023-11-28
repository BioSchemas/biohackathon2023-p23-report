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

![BioHackrXiv logo](figures/biohackrxiv.png)
Figure 1. A figure corresponding to the logo of our BioHackrXiv preprint.

# Results 
## Bioschemas usage analysis through Live Deploys 

The first part of this work consisted in assembling an RDF dataset based on the Bioschemas 140 live deploys URLS[^ld]

We developed a command line application supported by the FAIR-Checker[@Gaignard2023FAIRCheckerSD] API that harvests Bioschemas markup for a given web page and store the markup in an RDF file. This results in an RDF graph with 74 245 Schema.org triples[^rdf_crawl]. 

We automated the metadata harvesting through a weekly run GitHub action[^gh]. 

[^ld]: https://bioschemas.org/developer/liveDeploys
[^rdf_crawl]: https://github.com/BioSchemas/bioschemas-validation/tree/main/data 
[^gh]: https://github.com/BioSchemas/bioschemas-validation/blob/main/.github/workflows/gen_live_deploy_reports.yml


### Profile-based analysis


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
