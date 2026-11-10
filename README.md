# Automatic genre assignment for the British Library 19th-century books

**Can machine learning assign a genre to the 19th-century books that the British Library left unclassified?**
This project trains and compares six support vector machine (SVM) models to find out.

📄 **[Read the full report (PDF)](CloseVictor_IDH_Assignment.pdf)**

> [!NOTE]
> Personal project for the course *Introduction to Digital Humanities* (Margherita Fantoli), Master of Digital Humanities, KU Leuven, 2025–2026.

## The question

The *Books divided by Genre* dataset from the British Library's digitised 19th-century collection contains 49,455 books, but only 19,309 of them have a genre and a sub-genre (called *type* in the data). The others sit in an "unspecified" file. Could a model trained on the classified books predict the missing labels?

## What was done

Six SVM models were trained on 18,087 English-language titles (80 % training, 20 % testing, five-fold cross-validation):

| Model | Predicts | Input | Test accuracy |
|---|---|---|---|
| 1 | Genre | Title only | 93.2 % |
| 2 | Genre | Title, author, place and date | 94.57 % |
| 3 | Type | Title only | 86.35 % |
| 4 | Type | Title, author, place and date | 88.04 % |
| 5 | Type | Multiple features + *predicted* genre | 90.63 % |
| 6 | Type | Multiple features + *gold-standard* genre | 91.32 % |

Each model is evaluated with a classification report, a confusion matrix and a measure of uncertainty.

## Main findings

- The scores look high, but they mostly reflect the well-represented classes (prose makes up more than half of the corpus). Rare types are often missed: *parody*, with 19 examples, is never predicted correctly.
- The small gains of the multi-feature models may come from data leakage (authors already seen during training) rather than real improvement.
- Using predicted genres to assign types costs less than one point of accuracy compared with gold-standard genres.
- **Conclusion:** the models are not reliable enough to label the unspecified books automatically. A better use is partial automation: let the model label only the cases it is confident about, and leave the rest to human annotators.

## Repository structure

```
├── code/                          # Python notebooks (models and descriptive statistics)
├── data/                          # Datasets used for training and testing
├── CloseVictor_IDH_Assignment.pdf # Full report
└── README.md
```

All plots, including those not shown in the report, can be found in the notebooks.

## How to run

The code is written in Python with pandas and scikit-learn. Open the notebooks in `code/` (for example in Jupyter); the imports at the top of each notebook list the libraries required.

## Data and related work

- **Data cleaning.** The dataset was first cleaned in a group project (Victor Close, Koji Okumura and Petar Soldo) with OpenRefine and Wikidata: [petar-soldo/IDH2025-G5](https://github.com/petar-soldo/IDH2025-G5).
- **Source.** British Library, *Digitised 19th-century books*, *Books divided by Genre*.
- **Related project.** Van Strien, D., Tolfo, G., Morris, V. and Beelen, K. (2021). [*Classifying 19th Century British Library books using Crowdsourcing and Machine Learning*](https://living-with-machines.github.io/genre-classification/intro.html). Living with Machines.

## Use of generative AI

Google Gemini and OpenAI ChatGPT were occasionally used to solve specific coding issues and remove redundancies. They were not used to design the overall architecture of the models.

## Author

Victor Close · [GitHub](https://github.com/Victor280296)
