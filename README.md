# TikTok Claims Classification

## Overview

This project develops an end-to-end machine learning framework for classifying TikTok video content as either a claim or an opinion.

The analysis evaluates how classification performance changes depending on the information available to the model, with particular attention to engagement signals, moderation-time metadata, transcription text, robustness, and practical deployment considerations.

## Objectives

- Classify TikTok videos as claims or opinions
- Compare engagement-aware and moderation-time prediction scenarios
- Evaluate transcription-based NLP classification
- Assess sensitivity to explicit lexical cues
- Identify important predictive features
- Evaluate the practical implications of model deployment

## Dataset

The analysis uses structured TikTok video metadata, engagement variables, and transcription text.

The target variable represents whether the video is classified as a claim or an opinion.

> Note: The raw dataset is not included in this repository where redistribution is not permitted.

## Methodology

The project follows an end-to-end data science workflow:

1. Data loading and inspection
2. Data cleaning and quality assessment
3. Exploratory data analysis
4. Target analysis
5. Feature engineering
6. Model preparation
7. Engagement-aware modeling
8. Moderation-time modeling
9. Natural language processing
10. Lexical robustness assessment
11. Model evaluation
12. Feature importance analysis
13. Business and moderation interpretation
14. Recommendations

## Modeling Scenarios

### Scenario A — Engagement-Aware

Uses observed engagement and metadata variables.

This scenario evaluates maximum predictive performance when post-publication engagement information is available.

### Scenario B — Moderation-Time

Excludes accumulated engagement variables.

This provides a more deployment-oriented assessment of prediction using information that is more likely to be available near publication.

### NLP — Transcription-Based

TF-IDF features extracted from video transcription text are used with Logistic Regression.

A lexical robustness test is additionally performed by removing selected explicit lexical cues.

## Models

The project evaluates:

- Logistic Regression
- Random Forest
- TF-IDF + Logistic Regression
- Lexical-Robustness TF-IDF

## Key Results

| Model | Scenario | Accuracy | Precision | Recall | F1 | ROC-AUC |
|---|---|---:|---:|---:|---:|---:|
| Logistic Regression | Engagement-Aware | 99.37% | 100.00% | 98.75% | 99.37% | 99.71% |
| Random Forest | Engagement-Aware | 99.61% | 100.00% | 99.22% | 99.61% | 99.74% |
| Logistic Regression | Moderation-Time | 61.49% | 82.38% | 29.92% | 43.89% | 64.06% |
| Random Forest | Moderation-Time | 60.94% | 75.03% | 33.61% | 46.42% | 63.71% |
| TF-IDF + Logistic Regression | Transcription | 100.00% | 100.00% | 100.00% | 100.00% | 100.00% |
| Lexical-Robustness TF-IDF | Transcription | 100.00% | 100.00% | 100.00% | 100.00% | 100.00% |

## Key Findings

### 1. Engagement signals were highly predictive

The Engagement-Aware Random Forest achieved an F1-score of 99.61% and ROC-AUC of 99.74%.

However, these results depend on engagement variables that may accumulate after publication and therefore may not be available during initial moderation.

### 2. Moderation-time metadata was substantially weaker

Removing engagement variables reduced Random Forest F1-score to 46.42% and ROC-AUC to 63.71%.

This demonstrates the importance of information availability when evaluating moderation models.

### 3. Transcription text was highly predictive

The transcription-based models achieved perfect test-set performance in this dataset.

The same performance remained after the selected lexical-cue robustness test.

However, this result should not be interpreted as evidence of production-ready performance. Independent external validation is required to assess generalizability.

### 4. Engagement variables dominated tabular feature importance

Feature-importance analysis identified engagement variables as dominant predictive signals among the tabular features.

These results represent predictive associations and should not be interpreted as causal relationships.

## Business & Moderation Implications

The results suggest that machine learning can potentially support content-moderation workflows by helping prioritize and classify content.

However, model selection should consider:

- Information availability
- Predictive performance
- Robustness
- Generalizability
- Interpretability
- Human oversight

Engagement metrics may be more appropriate as contextual or prioritization signals once they become available rather than as primary signals for initial moderation.

## Recommendations

- Use machine learning as a moderation-support system rather than an autonomous decision-maker.
- Separate features according to when they become available.
- Treat engagement metrics as contextual or prioritization signals.
- Validate transcription-based NLP models on independent datasets.
- Maintain human review for uncertain or high-impact cases.
- Monitor model performance over time.
- Periodically retrain and reassess models using newly labeled data.

## Limitations

- The dataset may contain structural patterns that do not generalize to naturally occurring TikTok content.
- Engagement variables may introduce timing limitations for initial moderation.
- Perfect NLP performance requires independent external validation.
- Feature importance indicates predictive association rather than causation.
- Additional validation on external datasets is required before operational deployment.
