# ConTurE (Conversational Turns Evaluation)
This README describes ConTurE, a turn annotated version of the publicly released dataset 
from the Interactive Evaluation of Dialog track of DSTC9 (Gunasekara et al., 2020; Mehri et al. 2020). 

We sampled 119 dialogs from the original dataset for turn level 
annotation where each Chatbot turn within the dialog was annotated for response quality. 

We hope releasing this dataset will benefit the community 
for research in automatic evaluation of open-domain dialog systems.

## Original Dataset

The original dataset [found here](https://github.com/exe1023/DialEvalMetrics) 
consisted of 2200 dialogs collected from 
invited participants conversing with 11 different chatbots through textual exchanges. 
The original authors of this dataset asked Amazon Mechanical Turk workers 
to rate all 2200 interactions on multiple dialog level dimensions.

The full description of the track challenge can be [found here](https://drive.google.com/file/d/1oVDMg-6HffMpkSXWylafTvVI1pDuMuqw/view).

## Dataset Sampling
We selected all dialogs of length 8 to 9 turns from each of the 11 chatbots.

We define a single turn as a User utterance / Chatbot response pair.

From that pool of conversations ~10 dialogs were randomly sampled from each chatbot system.
The dataset statistics can be found below.

## Turn level annotations

For each Chatbot response turn within a dialog, we asked three Amazon Mechanical Turkers 
to evaluate the response given the dialog context. They were asked 
"What is your overall impression of the Chatbot's response?" 
and were given three options to choose from:

Overall I dislike the Chatbot's response: 0

Overall I kind of like the Chatbot's response: 1

Overall I like the Chatbot's response: 2

To judge the response quality, we asked the workers to look at how relevant and interesting 
a response is for the given dialog context. 

We used majority voting to determine the final score. In the case of ties we use a score from an expert annotator.

## Dialog level annotations

We also keep the same dialog level annotations that were in the original dataset.

### Conversations

The .json file has the following format:

```
"dialog_id": 0,
"turns": [
        {
            "user": "User: Who would you vote for?",
            "chatbot": "Chatbot: i would for sure, it is so cool and full of history.",
            "overall impression": 0
        },
        {
            "user": "User: Who is Donald Trump?",
            "chatbot": "Chatbot: that's a funny question, well it isn't really surprising that he isn't one of the three wealthiest presidents in american history, i know they measure by inflation but still",
            "overall impression": 2
        },
        {
            "user": "User: What is covid19.",
            "chatbot": "Chatbot: well apparently he is the wealthiest president in history, i don't know what to think of that, maybe his rich friends told him or something",
            "overall impression": 0
        }
    ]

overall impression: turn level annotation scale (0, 1, 2)

```

## Dataset Statistics

|             | Count |
| ----------- | ----------- |
| # of conversations        | 119       |
| # of turns                | 1066      |
| % of turns with score 0   | 30.7%     |
| % of turns with score 1   | 22.2%     |
| % of turns with score 2   | 47.1%       |

## Correlation with Dialog level dimensions

We take the mean aggregation of the turn level annotations and 
compute the correlation against each dialog level dimension in the original dataset. 
We see that the annotations have moderate correlation with all the parameters.

| Dialog level Dimension    | Pearson    | Spearman |
| -----------               |----------- | -----------
| consistent                | 0.38       | 0.40     |
| likeable                  | 0.42       | 0.45     |
| diverse                   | 0.23       | 0.25     |
| informative               | 0.30       | 0.34     |
| coherent                  | 0.32       | 0.37     |
| human (overall)           | 0.45       | 0.48     |
| understanding             | 0.36       | 0.42     |
| flexible                  | 0.33       | 0.40     |
| topic depth               | 0.34       | 0.35     |
| error recovery            | 0.37       | 0.40     |
| inquisitive               | 0.20       | 0.27     |

## Citation
If you use this dataset in your work please cite the following papers

```
@inproceedings{ghazarian-etal-2022-wrong,
    title = "What is wrong with you?: Leveraging User Sentiment for Automatic Dialog Evaluation",
    author = "Ghazarian, Sarik  and
      Hedayatnia, Behnam  and
      Papangelis, Alexandros  and
      Liu, Yang  and
      Hakkani-Tur, Dilek",
    booktitle = "Findings of the Association for Computational Linguistics: ACL 2022",
    month = may,
    year = "2022",
    address = "Dublin, Ireland",
    publisher = "Association for Computational Linguistics",
    url = "https://aclanthology.org/2022.findings-acl.331",
    pages = "4194--4204",
    abstract = "Accurate automatic evaluation metrics for open-domain dialogs are in high demand. Existing model-based metrics for system response evaluation are trained on human annotated data, which is cumbersome to collect. In this work, we propose to use information that can be automatically extracted from the next user utterance, such as its sentiment or whether the user explicitly ends the conversation, as a proxy to measure the quality of the previous system response. This allows us to train on a massive set of dialogs with weak supervision, without requiring manual system turn quality annotations. Experiments show that our model is comparable to models trained on human annotated data. Furthermore, our model generalizes across both spoken and written open-domain dialog corpora collected from real and paid users.",
}
```

```
@article{gunasekara2020overview,
  title={Overview of the Ninth Dialog System Technology Challenge: DSTC9},
  author={Gunasekara, Chulaka and Kim, Seokhwan and D'Haro, Luis Fernando and Rastogi, Abhinav and Chen, Yun-Nung and Eric, Mihail and Hedayatnia, Behnam and Gopalakrishnan, Karthik and Liu, Yang and Huang, Chao-Wei and others},
  journal={Proceedings of the 9th Dialog System Technology Challenge Workshop in AAAI2021},
  url = {https://arxiv.org/abs/2011.06486},
  year={2021}
}
```