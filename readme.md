# OpenGlam/OACH Declaration - Bibliography audit

## Setup

To create an environment with the required Python packages, use Anaconda's `conda` package manager:

`conda env create -f environment.yml`

Then, before opening the Jupyter notebook, activate the environment created:

`conda activate ./envs`

Finally, open Jupyter Lab to see the `notebook.ipynb` notebook:

`jupyter lab`.

## File descriptions

**zotero.csv**:
Zotero's OACH Declaration library export, in csv format.

**zotero.rdf**:
Zotero's OACH Declaration library export, in rdf format.

**wgnd_ctry.csv**:
List of name-country pairs and their gender. See notebook section "Gender" for more information.

**gender.csv**:
Gender information per publication (identified by the Zotero ID) and author.

**authors.csv**:
zotero.csv file expanded to one row per author, and merged with gender.csv. Includes information about collections ("\*WORK IN", "\*\*CITED IN", etc) as well.

**crossref/crossref_types.csv**:
Equivalence between CrossRef content types and Zotero item types.

**crossref/config.json**:
Configuration parameters for the CrossRef API.

**crossref/query_cache**:
Index of previous cached responses from CrossRef API.

**crossref/json/<ZOTERO-ID>.json**
Saved responses from CrossRef API.

**locations.csv**
Affiliation and publisher location information from CrossRef.

