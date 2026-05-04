# Samsung Galaxy Battery Sentiment Analysis

A sentiment analysis study tracking how Reddit user opinions toward Samsung Galaxy battery 
performance evolved across three device generations (S22, S23, S24).

## Research Question

How has Reddit user sentiment toward Samsung Galaxy battery performance changed across 
the S22, S23, and S24 releases?

## Project Overview

Battery performance is one of the most frequently discussed aspects of smartphone 
satisfaction. This project collects and analyzes Reddit posts from device-specific subreddits 
to measure how sentiment around battery life, overheating, charging speed, and endurance 
has shifted across three consecutive Samsung Galaxy generations.

Dual sentiment models (VADER and TextBlob) are applied and compared, providing a 
cross-validated view of sentiment distributions and temporal trends.

## Data Collection

Data was collected using the **Python Reddit API Wrapper (PRAW)** from the following 
subreddits:

| Generation | Subreddits |
|------------|-----------|
| S22 | r/GalaxyS22 |
| S23 | r/GalaxyS23, r/GalaxyS23Ultra, r/GalaxyS23Plus |
| S24 | r/GalaxyS24, r/GalaxyS24Ultra, r/GalaxyS24Plus |

**Keywords used:**
battery OR "battery life" OR drain OR "screen on time" OR SOT OR charging OR overheating

- Minimum 500 posts per device generation
- Posts filtered to exclude NSFW content and downvoted posts (score < 0)
- Duplicates removed by post ID

> **Note:** Raw data is not included in this repository due to Reddit API Terms of Service.
> To reproduce the dataset, you will need your own Reddit API credentials. See the 
> notebook for collection instructions.

## Methodology

### Preprocessing
- Title and selftext concatenated into a single text field
- Text lowercased and stripped of emojis and extra whitespace
- Missing selftext replaced with empty strings

### Sentiment Analysis
Two lexicon-based sentiment models were applied:

- **VADER** — rule-based model designed for social media text
- **TextBlob** — general-purpose polarity scorer

Posts were classified as:
- **Positive:** score ≥ 0.05
- **Negative:** score ≤ −0.05
- **Neutral:** otherwise

## Key Findings

- **S22** exhibited the highest proportion of negative posts and the widest sentiment 
  variance, reflecting early frustration with battery drain, overheating, and standby loss
- **S23** showed a moderate shift toward neutrality with reduced negative outliers
- **S24** had the tightest score distribution and highest positive sentiment share, 
  suggesting improved user perception over successive generations
- Neutral sentiment was dominant across all three datasets, consistent with Reddit users 
  documenting real-world usage rather than expressing extreme opinions
- VADER and TextBlob showed moderate agreement, with S24 posts displaying the 
  strongest inter-model alignment

## Visualizations

| Figure | Description |
|--------|-------------|
| Figure 1 | Overall sentiment distribution (VADER and TextBlob) |
| Figure 2 | Sentiment comparison across Galaxy models |
| Figure 3 | Distribution of sentiment scores by model (boxplots) |
| Figure 4 | Agreement between VADER and TextBlob scores (scatterplot) |

## Stack

- Python 3.x
- PRAW (Reddit API)
- VADER (nltk)
- TextBlob
- pandas
- Matplotlib

## Setup

```bash
pip install -r requirements.txt
```

Add your Reddit API credentials to the notebook:
```python
reddit = praw.Reddit(
    client_id="YOUR_CLIENT_ID",
    client_secret="YOUR_CLIENT_SECRET",
    user_agent="YOUR_USER_AGENT"
)
```

## Limitations

- Only post text was analyzed — comment threads were excluded
- Reddit users are a self-selected population and may not represent all Samsung owners
- VADER and TextBlob can misclassify sarcasm, mixed-sentiment posts, or technical 
  descriptions of battery behavior
- Aspect-level sentiment (e.g., separating drain vs. heat vs. charging) was not applied

## Future Work

- Apply aspect-based sentiment analysis to isolate specific battery attributes
- Include comment threads for richer context
- Track sentiment changes pre- and post-firmware update releases
- Experiment with transformer-based sentiment models for improved accuracy

## Author

Preetha Venkatanarayanan  
Social Media Mining — Fall 2025  
Indiana University
