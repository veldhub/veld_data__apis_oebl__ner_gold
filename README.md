# APIS ÖBL NER data

Randomized sentences from historical German biographies, containing named entities.

## Source of data

The original data was extracted from the [Austrian Biographical Lexicon
(ÖBL)](https://www.oeaw.ac.at/acdh/oebl) in the context of the [Austrian Prosopographical
Information System (APIS) project](https://www.oeaw.ac.at/acdh/projects/completed-projects/apis).

From there, samples were randomly pulled and annotated for Named Entity Recognition tasks, which
form this dataset.

The texts concern numerous smaller biographies in the time period between 19th and early 20th
century within historical Austria-Hungary, and were produced by the [Austrian Acadamey of
Sciences](https://www.oeaw.ac.at/en) between 1957 and 2023.

The language style is rather condensed and contains a lot of domain-specific abbreviations.

The contained NER tags are `PER` (Person), `ORG` (Organisation), `LOC` (Location).

Extracted and transformed from: https://gitlab.oeaw.ac.at/acdh-ch/apis/spacy-ner in the context of a
VELD chain: https://github.com/steffres/veld_chain_6__apis_ner_transform_to_conll2003

In the original spacy-ner repo, several data sets are split into corpus / training / eval sets,
scattered across folders with their respective nlp models, and also spread across different formats
(txt, json, pickle). In order to reuse this data, it was extracted, harmonized, cleaned,
deduplicated and transformed it into one consistent data source as json files, where only texts and
the indices and tags of their contained named entities are persisted.

## data description

### files

[./data/apis_oebl__ner__1_uncleaned.json](./data/apis_oebl__ner__1_uncleaned.json)

The original, but united, data coming from APIS / ÖBL.

[./data/apis_oebl__ner__2_cleaned.json](./data/apis_oebl__ner__2_cleaned.json)

Overlapping entities are removed, index offsets corrected, and duplicates removed. Also texts
without any entities are removed too, since it's not known if they don't contain any entities (which
often is not true; quite a few of them contain entities) or if the annotators simply didn't go
through them (which is more likely, hence they were removed).

In the original uncleaned data, some entity types are suffixed with numbers (e.g. `PER-1337`). These
were used for identifying entities in a project context, but are probably of less use for NER NLP
training. This dataset keeps the identifiers.

[./data/apis_oebl__ner__3_cleaned_simplified.json](./data/apis_oebl__ner__3_cleaned_simplified.json)

Same as apis_oebl__ner__2_cleaned.json, but with simplified entities (e.g. `PER` instead of
`PER-1337`). **Probably it's best to use this data set for NER training.**

