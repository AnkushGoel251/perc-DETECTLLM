# perc-DETECTLLM 


## About the DataSet 

* The dataset includes 804 opinion statements from the Reddit subcommunity /r/ChangeMyView (CMV) as studied by Tan et al., 2016, and 1,000 reviews from the Yelp reviews dataset as analyzed by Zhang et al., 2015.

* For news article writing, it comprises 1,000 news articles from XSum as per Narayan et al., 2018, and 777 news articles from TLDR_news.

* In the question answering category, it contains 1,000 answers from the ELI5 dataset as per Fan et al., 2019.

* For story generation, the dataset includes 1,000 human-written stories based on prompts from the Reddit WritingPrompts (WP) dataset as per Fan et al., 2018, and 1,000 stories from ROCStories Corpora (ROC) as per Mostafazadeh et al., 2016.

* In the commonsense reasoning category, it consists of 1,000 sentence sets for reasoning from HellaSwag as per Zellers et al., 2019a.

* For knowledge illustration, it includes 1,000 Wikipedia paragraphs from SQuAD contexts as per Rajpurkar et al., 2016.

* Lastly, for scientific writing, it contains 1,000 abstracts of scientific articles from SciGen as per Moosavi et al., 2021.

*DataSet Link* : [DataSet](https://drive.google.com/file/d/1Js1XhJjIaULrffQd3eZ7UK2q9RGXQjPd/view?usp=drive_link)



## About the Model : 

DetectGPT’s approach to distinguishing between machine-generated and human-written text is particularly relevant in today’s digital age, where AI language models are increasingly used to generate text. This could range from creating content for websites, drafting emails, to even generating news articles. As such, the ability to discern the origin of the text becomes crucial in various contexts, including but not limited to, academic integrity, content credibility, and information security.

The perturbation function, a key component of DetectGPT, is designed to introduce subtle changes to the text while preserving its overall meaning. This is a non-trivial task as it requires a careful balance between making meaningful modifications and maintaining the original intent of the text. The choice of perturbation function can significantly impact the performance of DetectGPT, making it an important area for further research and optimization.

The Perturbation Discrepancy Gap Hypothesis, which forms the theoretical foundation of DetectGPT, provides an interesting insight into the characteristics of machine-generated text. It suggests that machine-generated text is more sensitive to perturbations, resulting in larger discrepancies in log probabilities. This characteristic can be attributed to the fact that language models, when generating text, optimize for high-probability outputs, which often lie in areas of negative curvature in the log probability function.

DetectGPT’s thresholding mechanism is another critical aspect that requires careful calibration. The threshold needs to be set at a level that maximizes the accuracy of distinguishing between machine-generated and human-written text. It’s worth noting that this threshold may vary across different language models and datasets, necessitating a dynamic thresholding strategy.

In conclusion, DetectGPT represents a significant advancement in the field of AI language models. By providing a robust and scalable method to distinguish between machine-generated and human-written text, it opens up new possibilities for understanding and regulating the use of AI in text generation. However, like all models, DetectGPT is not without its limitations and areas for improvement, which present exciting opportunities for future research.


## Approach of `perc-DETECTLLM` : 

### 1. Model Methodology - 

*Data Manipulation*: The first step in our process involved manipulating the data to create a mixed dataset of human-written and machine-generated text. We achieved this by randomly selecting segments within human-written sentences and replacing them with corresponding segments generated by Language Models (LLMs). This process simulates a real-world scenario where human-written content might be interspersed with machine-generated text.

*Calculation of LLM Percentage Data (llm_perc_data)*: Once we have our mixed dataset, we calculated a metric called LLM percentage data for each sentence. This metric quantifies the proportion of each sentence that has been generated by an LLM. It is calculated as the ratio of the word count of the LLM-generated segment to the total word count of the sentence: 

**[ llm_perc_data = \frac{{\text{{len(word count of LLM-generated)}}}}{{\text{{len(word count of the sentence)}}}} ]**
                                  *{Make sure to change LaTex to Docs}*

This gives us a continuous value between 0 and 1, where 0 indicates no LLM-generated content and 1 indicates that the entire sentence is LLM-generated.

*Utilization of DetectGPT Model*: Next, we used the DetectGPT model to independently assess the likelihood of each sentence being machine-generated. DetectGPT provided an estimate, also a continuous value between 0 and 1, of how likely it is that a given sentence has been generated by an LLM.

*Bayesian Model Evaluation*: Finally, we combined the LLM percentage data and the DetectGPT assessment using Bayesian inference to estimate the overall percentage of LLM-generated text in our dataset. Bayesian inference allowed us to update our prior beliefs about the distribution of LLM-generated text based on the observed data.

The Bayesian update was performed using Bayes’ theorem:

**[ P(\text{{LLM-generated}} | \text{{data}}) = \frac{{P(\text{{data}} | \text{{LLM-generated}}) \times P(\text{{LLM-generated}})}}{{P(\text{{data}})}} ]**

*Notation* : 
* ( *P(\text{{LLM-generated}} | \text{{data}})* )is the posterior probability, or our updated belief about the proportion of LLM-generated text after observing the data.
* ( *P(\text{{data}} | \text{{LLM-generated}})* )is the likelihood, or the probability of observing our data given that a certain proportion of it is LLM-generated.
* ( *P(\text{{LLM-generated}})* )is the prior probability, or our initial belief about the proportion of LLM-generated text before observing the data.
* ( *P(\text{{data}})* )is the evidence, or the total probability of observing our data under all possible proportions of LLM-generated text.



## DetectGPT (Webapp)

### Introduction
This is the webapp for our implementation of detectGPT

### installation
pip install -r requirements.txt

### Usage

``` 4d
uvicorn main:app
```

```

## Acknowledgements
1. Mitchell, Eric, et al. "DetectGPT: Zero-Shot Machine-Generated Text Detection using Probability Curvature." arXiv preprint arXiv:2301.11305 (2023).

```

**authors** : 
* 1. Ankush Goel [https://github.com/AnkushGoel251]
* 2. Saibal Patra [https://github.com/SaibalPatraDS]
* 3. Vineet Kumar [https://github.com/krvneet]