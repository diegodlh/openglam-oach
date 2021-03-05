# OpenGlam/OACH Declaration - Bibliography audit

See the report published [here](https://medium.com/open-glam/bibliography-audit-and-data-extraction-671c76a99626) to find out more.

## Setup

To create an environment with the required Python packages, use Anaconda's `conda` package manager:

`conda env create -f environment.yml`

Then, before opening the Jupyter notebook, activate the environment created:

`conda activate ./envs`

Finally, open Jupyter Lab to see the `notebook.ipynb` notebook:

`jupyter lab`.

## File descriptions

### zotero.csv
Zotero's OACH Declaration library export, in csv format.

### zotero.rdf
Zotero's OACH Declaration library export, in rdf format.

### wgnd_ctry.csv
List of name-country pairs and their gender. See notebook section "Gender" for more information.

### gender.csv
Gender information per publication (identified by the Zotero ID) and author.

- gender: consensus gender (F: female, M: male, ?: ambiguous). If two or more genders are equally likely, they are all shown (e.g., "FM", "?F", etc).
	- "No name": no author was available for the source.
	- "Name(s) not found": name was not found in the gender database
	- "Unexpected name format": name does not follow the "string <comma> string" format (this is often the case with non-human creators, such as institutions).
- agreement: this is the index of agreement among databases for the consensus gender. 1 is maximum agreement.
- split: False if full name was found in the gender database (e.g., "Jean Claude"). True if the full name was not found and it had to be split into its separate parts.
- male/female/ambiguous: for each gender, a list of country codes is shown for each name found. For example, "{'ED': ['CA', 'GB', 'NL', 'US']}" in the male column indicates that "Ed" was found to be "male" according to information provided by "Canada", "Great Britain", "New Zealand" and "United States".

### authors.csv
zotero.csv file expanded to one row per author, and merged with gender.csv. Includes information about collections ("\*WORK IN", "\*\*CITED IN", etc) as well.

### crossref/crossref_types.csv
Equivalence between CrossRef content types and Zotero item types.

### crossref/config.json
Configuration parameters for the CrossRef API.

### crossref/query_cache
Index of previous cached responses from CrossRef API.

- **key**: Zotero ID.
- **query**: how the API was called.
- **doi**:
 	- doi of the publication returned by the API, or
 	- *Error "Type not supported"*: the Zotero item is of a type not found in CrossRef (e.g., webpage).
 	- *Error "Not found"*: the API search returned no results.
 	- *Error "HTTP Error: NNN"*: unexpected HTTP error from API.
- **score**: matching score of the top result returned. "exact" if doi was used for retrieval.
- **ts**: timestamp.

### crossref/json/<ZOTERO-ID>.json
Saved responses from CrossRef API.

### crossref.csv
Affiliation and publisher location information from CrossRef.

- **key**: Zotero ID.
- **xref_doi**: DOI of CrossRef top result, as in *crossref/query_cache* above.
- **xref_title**: title of CrossRef top result, to compare with title of Zotero item. "Error: No title" if no title provided.
- **xref_score**: as in *crossref/query_cache*.
- **xref_author_count**: number of authors in the publication returned. Also to compare with original Zotero item.
- **xref_affiliations**: list of affiliation lists, on per author. "Error: No affiliations provided" if no affiliations returned by the API.
- **xref_affil_first_first**: first affiliation of the first author.
- **xref_affil_main**: most frequent affiliation across all authors. More than one may be returned in case of tie.
- **xref_publisher_location**: publisher location.

### locations.csv
zotero.csv and crossref.csv merged, with collection information as well.

### emails.csv
zotero.csv + collection information + email information (parsed from Zotero attachments)
