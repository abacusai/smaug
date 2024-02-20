# Datasheet for Pairwise Preference ARC, HellaSwag, and MetaMath

We include a [Datasheet](https://arxiv.org/abs/1803.09010). 
Thanks for the Markdown template from [Christian Garbin's repository](https://github.com/fau-masters-collected-works-cgarbin/datasheet-for-dataset-template).

Jump to section:

- [Motivation](#motivation)
- [Dataset Composition](#dataset-composition)
- [Collection Process](#collection-process)
- [Data Preprocessing](#data-preprocessing)
- [Data Distribution](#data-distribution)
- [Dataset Maintenance](#dataset-maintenance)
- [Legal and Ethical Considerations](#legal-and-ethical-considerations)

## Motivation

### Why was the datasheet created? (e.g., was there a specific task in mind? was there a specific gap that needed to be filled?)

The goal of releasing the three preference-based datasets (ARC, HellaSwag, and MetaMath) is to improve the reasoning abilities of LLMs by fine-tuning on these datasets (such as by performing DPOP, as described in our paper). We found that fine-tuning using these datasets improves reasoning abilities of open-source LLMs better than existing datasets.

### Has the dataset been used already? If so, where are the results so others can compare (e.g., links to published papers)?

So far, we are the only ones to use the datasets, and we have used them to create the Smaug series of models as described in our paper.

### What (other) tasks could the dataset be used for?

All of these datasets are preference-based datasets for reasoning tasks. To the best of our knowledge, the pairwise preference-based format is well-suited only for fine-tuning and aligning LLMs, so they can only be used for improving LLMs' reasoning and mathematical abilities.

### Who funded the creation of the dataset? 

These datasets were created by researchers at Abacus.AI. Funding for the dataset creation is from Abacus.AI.

### Any other comments?

None.

## Dataset Composition

### What are the instances?(that is, examples; e.g., documents, images, people, countries) Are there multiple types of instances? (e.g., movies, users, ratings; people, interactions between them; nodes, edges)

Each instance is a question, together with a preferred completion and a dispreferred completion.
Here is an example from the preference-based MetaMath dataset.

Question: ```What is the total cost of purchasing equipment for all sixteen players on the football team, considering that each player requires a \$25 jersey, a \$15.20 pair of shorts, and a pair of socks priced at \$6.80?```

Preferred completion:
```Each player requires a \$25 jersey, a \$15.20 pair of shorts, and a pair of socks priced at \$6.80. So the total cost for each player is \$25 + \$15.20 + \$6.80 = \$\textbf{47}. Since there are sixteen players on the football team, the total cost for all of them is 16 * \$47 = \$752. \#\#\#\# 752 The answer is: 752.```

Dispreferred completion: 
```Each player requires a \$25 jersey, a \$15.20 pair of shorts, and a pair of socks priced at \$6.80. So the total cost for each player is \$25 + \$15.20 + \$6.80 = \$\textbf{52}. Since there are sixteen players on the football team, the total cost for all of them is 16 * \$47 = \$752. \#\#\#\# 752 The answer is: 752.```

### How many instances are there in total (of each type, if appropriate)?

The preference-based MetaMath dataset contains 393,999 training examples and 1,000 evaluation examples.
The preference-based ARC dataset contains 3357 training examples and 895 evaluation examples.
The preference-based HellaSwag dataset contains 119,715 training examples and 30,126 evaluation examples.

### What data does each instance consist of ? “Raw” data (e.g., unprocessed text or images)? Features/attributes? Is there a label/target associated with instances? If the instances related to people, are subpopulations identified (e.g., by age, gender, etc.) and what is their distribution?

Each instance consists of a question, together with a preferred completion and a dispreferred completion. It is entirely English text. The preferred completion is the 'positive label', and the dispreferred completion is the 'negative label'.

### Is any information missing from individual instances? If so, please provide a description, explaining why this information is missing (e.g., because it was unavailable). This does not include intentionally removed information, but might include, e.g., redacted text.

There is no missing information.

### Are relationships between individual instances made explicit (e.g., users’ movie ratings, social network links)? If so, please describe how these relationships are made explicit.

There are no relationships between individual instances.

### Does the dataset contain all possible instances or is it a sample (not necessarily random) of instances from a larger set? If the dataset is a sample, then what is the larger set? Is the sample representative of the larger set (e.g., geographic coverage)? If so, please describe how this representativeness was validated/verified. If it is not representative of the larger set, please describe why not (e.g., to cover a more diverse range of instances, because instances were withheld or unavailable).

The preference-based MetaMath dataset has one instance for each instance of the original MetaMath dataset.
For ARC and HellaSwag, the original datasets consist of four choices of responses to each question, one of which is correct. To create a paired preference-ranked dataset, for each correct response in the training split, we create three pairs using each incorrect response.

### Are there recommended data splits (e.g., training, development/validation, testing)? If so, please provide a description of these splits, explaining the rationale behind them.

The preference-based MetaMath dataset contains 393,999 training examples and 1,000 evaluation examples.
The preference-based ARC dataset contains 3357 training examples and 895 evaluation examples.
The preference-based HellaSwag dataset contains 119,715 training examples and 30,126 evaluation examples.

### Are there any errors, sources of noise, or redundancies in the dataset? If so, please provide a description.

There are no known errors, sources of noise, or redundancies.

### Is the dataset self-contained, or does it link to or otherwise rely on external resources (e.g., websites, tweets, other datasets)? If it links to or relies on external resources, a) are there guarantees that they will exist, and remain constant, over time; b) are there official archival versions of the complete dataset (i.e., including the external resources as they existed at the time the dataset was created); c) are there any restrictions (e.g., licenses, fees) associated with any of the external resources that might apply to a future user? Please provide descriptions of all external resources and any restrictions associated with them, as well as links or other access points, as appropriate.

The dataset is self-contained.

### Any other comments?

None.


## Collection Process


### What mechanisms or procedures were used to collect the data (e.g., hardware apparatus or sensor, manual human curation, software program, software API)? How were these mechanisms or procedures validated?
 
The preference-based MetaMath dataset has one instance for each instance of the original MetaMath dataset.
For ARC and HellaSwag, the original datasets consist of four choices of responses to each question, one of which is correct. To create a paired preference-ranked dataset, for each correct response in the training split, we create three pairs using each incorrect response.

### How was the data associated with each instance acquired? Was the data directly observable (e.g., raw text, movie ratings), reported by subjects (e.g., survey responses), or indirectly inferred/derived from other data (e.g., part-of-speech tags, model-based guesses for age or language)? If data was reported by subjects or indirectly inferred/derived from other data, was the data validated/verified? If so, please describe how.
 
The instances were taken from the corresponding MetaMath, ARC, and HellaSwag datasets, as described above.

### If the dataset is a sample from a larger set, what was the sampling strategy (e.g., deterministic, probabilistic with specific sampling probabilities)?
 
We did not use a probabilistic sampling strategy. As described earlier, the preference-based MetaMath dataset has one instance for each instance of the original MetaMath dataset, and for ARC and HellaSwag, for each correct response in the training split, we create three pairs using each corresponding incorrect response.

### Who was involved in the data collection process (e.g., students, crowdworkers, contractors) and how were they compensated (e.g., how much were crowdworkers paid)?
 
The creation of the datasets were done by the authors of this work.

### Over what timeframe was the data collected? Does this timeframe match the creation timeframe of the data associated with the instances (e.g., recent crawl of old news articles)? If not, please describe the timeframe in which the data associated with the instances was created.
 
The timeframe for constructing the dataset was from January 15, 2024 to February 1, 2024.

## Data Preprocessing

### Was any preprocessing/cleaning/labeling of the data done (e.g., discretization or bucketing, tokenization, part-of-speech tagging, SIFT feature extraction, removal of instances, processing of missing values)? If so, please provide a description. If not, you may skip the remainder of the questions in this section.
 
We did not perform any preprocessing ourselves on top of the preprocessing already done in creating MetaMath, ARC, and HellaSwag.

### Does this dataset collection/processing procedure achieve the motivation for creating the dataset stated in the first section of this datasheet? If not, what are the limitations?
 
Yes, the dataset does achieve our motivation as stated above (to improve the reasoning abilities of LLMs by fine-tuning using methods such as DPOP): as we show in our paper, fine-tuning on these and existing datasets results in state-of-the-art open-source LLM ability.

### Any other comments
 
None.

## Dataset Distribution

### How will the dataset be distributed? (e.g., tarball on website, API, GitHub; does the data have a DOI and is it archived redundantly?)
 
The datasets are available on an anonymous google drive in our README.

### When will the dataset be released/first distributed? What license (if any) is it distributed under?
 
The datasets are public (anonymously) as of February 15, 2024, distributed under the Apache License 2.0.

### Are there any copyrights on the data?
 
There are no copyrights on the data.

### Are there any fees or access/export restrictions?
 
There are no fees or restrictions.

### Any other comments?
 
None.

## Dataset Maintenance

### Who is supporting/hosting/maintaining the dataset?
 
The authors of this work are supporting/hosting/maintaining the dataset.

### Will the dataset be updated? If so, how often and by whom?
 
We have no updates currently planned. We welcome updates from the open-source community. After the reviewing period, we will host the datasets on a public github. If any community member has an improvement, they may open a pull request to include their method.

### How will updates be communicated? (e.g., mailing list, GitHub)
 
Updates will be communicated on the GitHub README.

### If the dataset becomes obsolete how will this be communicated?
 
If the dataset becomes obsolete, it will be communicated on the GitHub README.

### If others want to extend/augment/build on this dataset, is there a mechanism for them to do so? If so, is there a process for tracking/assessing the quality of those contributions. What is the process for communicating/distributing these contributions to users?
 
Others can create a pull request on GitHub with possible extensions to our datasets, which will be approved case-by-case. 


## Legal and Ethical Considerations

### Were any ethical review processes conducted (e.g., by an institutional review board)? If so, please provide a description of these review processes, including the outcomes, as well as a link or other access point to any supporting documentation.
 
There was no ethical review process.

### Does the dataset contain data that might be considered confidential (e.g., data that is protected by legal privilege or by doctorpatient confidentiality, data that includes the content of individuals non-public communications)? If so, please provide a description.
 
The datasets do not contain any confidential data.

### Does the dataset contain data that, if viewed directly, might be offensive, insulting, threatening, or might otherwise cause anxiety? If so, please describe why.
 
None of the data might be offensive, insulting, threatening, or otherwise cause anxiety.

### Does the dataset relate to people? If not, you may skip the remaining questions in this section.
 
The datasets do not relate to people.

### Any other comments?
 
None.
