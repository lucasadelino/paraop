# Paraop
Paraop is a framework for annotating _paraphrase operations_: the specific changes that occur in a sentence in the production of a paraphrase. 

To illustrate, if we have the following pair of sentences:
	
> John gave Mary a book
> 
> John gave a book to Mary

Then the Paraop annotations for the sentence pair would be:

| John | gave | Mary   | a     | book   |
| :--: | :--: | :----: | :---: | :----: |
|  0   |  0   | 3      | 3     | 3      |

| John | gave | a     | book   | to    | Mary   |
| :--: | :--: | :---: | :----: | :---: | :----: |
|  0   |  0   | 3     | 3      | 1     | 3      |

The numbers below each word in the example above denote which Paraop operation applies to that word. For instance, 1 represents the addition of a function word, 3 represents a change of order, and 0 represents no change.

## What resources are available?
This repository contains:
- The Paraop corpus, available in the `dataset` directory.
- The four Paraop token classifiers, available in the notebooks in the root directory.

## Structure of the framework
Paraop operations describe string-level transformations between pairs of sentences. There are eight total operations, which can be categorized under three major groups:

| Operation Group      | Operation Name             | ID     | 
|:--------------------:|:--------------------------:|:------:| 
| Addition/Deletion    | Content word               | 1      | 
|                      | Function word              | 2      | 
|                      | Punctuation                | 8      | 
| Change of Order      |                            | 3      | 
| Substitution         | Synonym                    | 4      | 
|                      | Contextual synonym         | 5      | 
|                      | Morphological              | 6      | 
|                      | Spelling and format        | 7      | 

To account for a wide variety of tasks, we make available four Paraop classifiers. These classifiers all share the same underlying architecture (namely, they are all [BERT](https://arxiv.org/abs/1810.04805) token classifiers), but they have slightly differences in the annotation task and in how Paraop labels are represented:

- In the **Subgroup** (`sub_`) models, labels represent all of the eight Paraop labels shown in the table above.
  - In the **Major group** (`maj_`) models, labels represent only the three major operation groups: addition/deletion, change of order, and substitution
- In the **Single-label** (`_single`) models, each token gets a single label.
  - In the **Multi-label** (`_multi`) models, each token gets an *array* of labels, containing either eight (in the case of the `sub_multi` model) or three labels (in the case of the `maj_multi` model).

If you're not sure which model to use, we recommend using the `sub_single` model. 

# Additional Information
## Precursors
The Paraop corpus is based on the Extended Typology Paraphrase Corpus [(ETPC)](https://github.com/venelink/ETPC), which, in turn, is based on the Microsoft Research Paraphrase Corpus [(MRPC)](https://www.microsoft.com/en-us/download/details.aspx?id=52398).

## Why annotate paraphrase operations?
Applications of paraphrase operation detection include:

- Data augmentation
- Machine translation
- Textual entailment detection
- Text summarization and simplification
- Plagiarism detection