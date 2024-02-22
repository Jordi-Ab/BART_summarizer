# BART news summarizer

Fine tune a BART model to perform Abstractive summarization on news articles.

Our DataSet consists of 295,174 news articles scrapped from a Mexican Newspaper, along with its summary. 
For simplicity, the Spanish news articles were translated to English using `Helsinki-NLP/opus-mt-es-en` NLP model.

Summaries were created using `StableBeluga-7B`. I left the LLM running for several days (weeks) in order to get all the summaries. The teacher observations are then used for fine tunning a BART lightweight model.

The objective for this is to have a lightweight model that can perform summarization as good as `StableBeluga-7B`, much faster and with much less computing resources.

We achieved very similar summary results (.66 ROUGE1 and .90 cosine similarity) on a validation DataSet with the lightweight BART model, 3x faster predictions and considerably less GPU memory usage.

The lightweight BART model weights only 1.5GB while Stable Beluga weights 13GB.

Notebooks description:

`0-make_stable_beluga_summaries.ipynb` -> Feed the articles to the LLM in order to get the summary teacher observations.
`1-make_dateset.ipynb` -> Preprocess the summaries in order to make sure that input text and summary doesn't exceed 1024 tokens.
`2-fine_tune_BART.ipynb` -> Perform the BERT fine tuning task
`3-evaluate.ipynb` -> Evaluate the results of the fine tunned model

As next steps we could create a pure Spanish summarizer model by leveraging multilingual LLMs and Spanish BART versions in order to avoid loosing context of the article with translation.