# Is TweetSim measuring meaning, or just hashtags?

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/ShishirProjects/tweetsim-hashtag-shortcut/blob/main/tweetsim_hashtag_shortcut_final.ipynb)

Research poster project for the NLP module, Universität Trier · Shishir Saraswat · M.Sc. NLP

TweetSim, the tweet-similarity task in SuperTweetEval (Antypas et al., 2023), was built from tweet pairs that share a trending hashtag plus 20 % random pairs. This project tests how much of the benchmark score comes from that shortcut rather than from understanding the tweets.

## Where to look
- **[tweetsim_hashtag_shortcut_final.ipynb](tweetsim_hashtag_shortcut_final.ipynb)**: the full experiment with all outputs, from data loading to results tables and charts.

## Key results (Spearman × 100, TweetSim test set, n = 450)
- Every tweet contains a hashtag; 79 % of test pairs share one. Sharing one explains 63.7 % of the gold-score variance.
- A one-line rule "do the tweets share a hashtag?" scores **70.8**, close to the best published model (74.6) and above every zero-/few-shot model in the paper.
- The paper's fine-tuned models are reproduced: TimeLM-base 74.8 (paper 72.2), RoBERTa-base 74.7 (paper 74.4).
- On pairs that share a hashtag, every neural model loses 20–27 points.
- Deleting the shared hashtag costs 9.6–27.5 points; deleting the same number of random words costs 1.0–4.9.
- Without hashtags, zero-shot sentence embedders (60.6–66.0) beat the fine-tuned models (43.3–46.6).

## Method
- **Data:** `cardiffnlp/super_tweeteval`, subset `tweet_similarity` (450 train / 100 dev / 450 test), loaded from Hugging Face.
- **15 systems:** surface baselines, zero-shot sentence embedders, a zero-shot LLM (Qwen2.5-1.5B), and the paper's fine-tuned cross-encoders (TimeLM-base, RoBERTa-base; 3 seeds).
- **Tests:** original · shared hashtags deleted · same number of random words deleted · all hashtags removed.
- **Evaluation:** Spearman × 100 as in the paper, with 95 % bootstrap confidence intervals.

## Reproduce
Click **Open in Colab**, set *Runtime → Change runtime type → T4 GPU*, then *Runtime → Run all* (about 35 minutes).

## References
1. Antypas, D., et al. (2023). SuperTweetEval: A Challenging, Unified and Heterogeneous Benchmark for Social Media NLP Research. *Findings of EMNLP 2023*.
2. Loureiro, D., et al. (2022). TimeLMs: Diachronic Language Models from Twitter. *ACL 2022 System Demonstrations*.
3. Gururangan, S., et al. (2018). Annotation Artifacts in Natural Language Inference Data. *NAACL 2018*.
4. Geirhos, R., et al. (2020). Shortcut Learning in Deep Neural Networks. *Nature Machine Intelligence*.
