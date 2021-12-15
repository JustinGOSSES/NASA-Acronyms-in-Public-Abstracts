# NASA-Acronyms-in-Public-Abstracts
NASA Acronyms in Public Abstracts from data.nasa.gov

A place to put this pulic dataset https://data.nasa.gov/Raw-Data/NASA-Acronyms-in-Public-Abstracts/byqb-7uyn and play around with it

## Dataset Description 

This dataset was created as a data source for machine-learning models used to disambiguate acronyms with multiple definitions. This dataset includes files that cover 406,005 abstracts. 484 acronyms with multiple definitions and multiple examples of use in different abstracts were extracted.

This was found to be a suitable dataset for training disambiguation models that use the context of the surrounding sentences to predict the correct meaning of the acronym. The prototype machine-learning models created from this dataset have not been released.


The NASA Science Technology and Information Program (https://www.sti.nasa.gov/) provided the NASA Office of the Chief Information Officer Transformation and Data Division Data Analytics team with a large JSONL of public abstracts from NASA authored papers and reports. These can be found in the results_merged.jsonl. These documents were exported in late 2018 and processed in 2019. They should not be thought to be extensive or complete of all public NASA abstracts. Please contact https://www.sti.nasa.gov/ if you want a full and up-to-date data dump. This dataset is processed for a specific purpose at a specific point in time.

JSONL is used as the format instead of JSON as it is faster and easier to access specific lines without having to check the dictionary for each metadata instance.

This dataset could be used for various purposes including lists of acronyms, lists of acronym definitions, and natural language processing models to disambiguate the meanings of acronyms with more than one definition. Anthony Buonomo, Jack Steilberg, and Justin Gosses contributed preparing this dataset as part of an intern project.


### Individual File Descriptions 
--------------------------------------------------
README.md:


- This is this file and contains a description of the individual files.

--------------------------------------------------
results_merged.jsonl:

- Holds the abstracts and associated abstract metadata in a JSONL format where each metadata object is a separate line. There are 406005 number of lines or abstracts in the JSONL file.

- The keys for each object include:
- 'contributor.originator',
- 'creator',
- 'date.available',
- 'date.issued',
- 'description',
- 'format',
- 'identifier',
- 'identifier.casi_id',
- 'language',
- 'relation.requires',
- 'rights',
- 'rights.accessRights',
- 'subject',
- 'subject.NASATerms',
- 'title',
- 'type'

--------------------------------------------------
test_records.jsonl:


- This is a file similar to results_merged.jsonl but it only includes 102 lines of metadata instances, which makes it much easier to work with when testing.
- processed_acronyms.jsonl:
- Each line in this file is an acronym found to have more than one defintion. There are 484 acronyms found with multiple definitions suitable for model building. Each line contains information on acronym, definitions, and where found in the corpus. The corpus is the file results_merged.jsonl
- The keys include:
- "acronym"
- "definition"
- "corpus_positions"
- "freq"
- "ac_freq":
- "mult_defs"
- "group_ids"

--------------------------------------------------
formatted_acronyms.jsonl:

- This file contains approximately 92,000 words extracted that might be acronyms, their defintions if found, and their position within the corpus. Many do not have extracted definitions. It should be noted that not all of them area acronyms. A relatively broad definition was used to generate this file.
- Each acronym instance is on a separate line and has the following keys:
- "acronym"
- "definition"
- "corpus_positions"
- "freq"
- "ac_freq"
--------------------------------------------------
acronyms.jsonl:

- Each line in this JSONL file maps back to each line that contains metadata for an abstrat in results_merged.jsonl.
- Each object on each line is key:value pairs of acronym & detected definition. If a definition is not detected, it is left as empty string "".

### EXAMPLE CODE TO LOAD JSONL FILES IN PYTHON

Because JSONL is a little different than JSON, here's some example code for loading a file:
```
import json
with open('results_merged.jsonl', 'r') as json_file:
json_list = list(json_file)
for json_str in json_list:
result = json.loads(json_str)
print(f"result: {result}")
print(isinstance(result, dict))



## Observable Notebook Explores Dataset

<a href="https://observablehq.com/@justingosses/exploration-of-nasa-acronyms-with-multiple-meanings">https://observablehq.com/@justingosses/exploration-of-nasa-acronyms-with-multiple-meanings</a>

![Chart showing how many acronyms occur in how many abstracts](acronyms_chart.png "Chart showing how many acronyms occur in how many abstracts")

![Observable notebook](observablenotebook.png "Observable notebook")
