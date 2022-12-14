# Data Reusability Pipeline

Analysis pipeline for the paper *A comprehensive analysis of the reusability of public omics data across 2.8 million research publications,* produced by the Mangul Lab at USC.

This analysis includes publications that interact with one or both of two online resources hosted by the National Center for Biotechnology Information (NCBI): the Sequence Read Archive (SRA) and the Gene Expression Omnibus (GEO).

Authors: Nicholas Darci-Maher, Kerui Peng, Dat Duong, Richard J. Abdill, Eleazar Eskin, Serghei Mangul

## Download data

Download the most recent open access subset of PubMed Central (PMC) publications. Rename journals with commas in their names to avoid issues downstream.Download metadata reference tables for every public SRA and GEO dataset.

Note: this data is large. Create a directory outside this repository to store the data, and point each script to that directory where appropriate.

```bash
cd scripts
./download_publications.sh
./rename_CommaJournals.sh
./download_refs.py
cd ../
```

## Select papers mentioning SRA or GEO

Parse the text of every publication for regular expressions matching SRA and GEO accession IDs.

```bash
cd scripts
./preFilterPMCscrape.sh
cd ../
```

## Extract the publication date from every selected paper

Create a key file containing the paths to each desired paper. Then, parse the XML files to find the earliest listed publish date.

```bash
cd scripts
./gen_pmc_paths.sh
./extractDate.sh
cd ../
```

## Create a master table containing all the data

### Launch jupyter notebook

Requires installation: https://jupyter.org/install

```bash
cd jupyter_notebooks
jupyter notebook
```

Merge data scraped from the PMC publications onto reference data from SRA and GEO.

* Run jupyter_notebooks/create_metadata_table.ipynb
* Run jupyter_notebooks/create_impactFactor_table.ipynb
* Run jupyter_notebooks/analyze_metadata_table.ipynb

## Create figures

Use everything generated so far to visualize findings.

* Run jupyter_notebooks/vizualize_data.ipynb
