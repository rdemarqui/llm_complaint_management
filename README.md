<p align="center">
  <h1>Decoding User Complaints: An Analysis using Mistral 7B LLM</h1>
</p>

<p align="center">
<img src="images\cover.png" class="center" width="45%"/>
</p>

## Overview
<p align="justify">
Analyzing user complaints is a crucial challenge for many organizations, involving understanding and effectively responding to customer concerns. One of the main challenges is managing the variety and complexity of complaints, which vary significantly in language and content, posing difficulties for accurate interpretation. Moreover, the high volume of complaints necessitates automated processes for efficient management. Effective analysis should identify underlying causes and trends, requiring sophisticated approaches that understand nuances and patterns in user complaints. Large Language Models (LLMs) are emerging as vital tools for dealing with these types of business problems.

<p align="justify">
In recent years, we have witnessed a surge in the development of open-source Large Language Models (LLMs), a phenomenon that is redefining the boundaries of Artificial Intelligence (AI) and Natural Language Processing (NLP). Among the most notable innovations in this area is the quantization of models, a technique that reduces model size and computational requirements, allowing its use in affordable machines while reducing budgetary costs.

<p align="justify">
This study aims to leverage these technological advancements, specifically employing the advanced LLM tool Mistral 7B [1], to analyze a comprehensive dataset of user complaints sourced from https://www.reclameaqui.com.br/. Through this analysis, we intend to demonstrate the potential and effectiveness of LLMs in interpreting and handling large-scale user feedback. This study can be replicado através do <code>02. LLM_analysis.ipynb</code> script.

## Objectives
<p align="justify">
Create a fast and automated system to categorize user complaints into one or more categories, providing insights into customer concerns and improving organizational response strategies.

## Technologies Used
* `python 3.9.16`
* `pandas 1.5.3`
* `numpy`
* `matplotlib`
* `sklearn`
* `seaborn 0.12.2`
* `selenium 4.14.0`
* `BeautifulSoup 4.11.2`
* `transformers 4.37.0`

## About the Data
<p align="justify">
The data was collected from the website reclameaqui.com, which is a Brazilian website with over 30 million registered consumers and 500,000 registered companies on the platform, where 1.5 billion pageviews occur annually [2]. A total of 7,000 distinct complaints from a telecommunications provider were collected. This complaints was classified by the users into 14 unique categories, therefore, we have a balanced dataset with 500 complaints per category.

## Methodology
**Data Extraction** <p align="justify">First, a script was created to scrape company data, and for this task, Python packages Selenium and BeautifulSoup were used. The script is available in the repository with the name <code>01. webscrapping_reclameaqui.ipynb</code>

**Data Cleaning** <p align="justify">To work with the complaints, we initially performed a simple cleaning, removing double spacing and converting all text to lowercase. We then replaced the mask inserted by 'reclame aqui' with a smaller one, aiming to only reduce the size of the text. Finally, we removed texts shorter than 3 characters as they lacked sufficient information for analysis.

**Stratification** <p align="justify">As this work is solely for study purposes and given the limitations of the Colab free tier, we performed a stratified sampling of the complaints, divided into two datasets. The first set contained 202 samples and served as the test dataset, and the second contained 2000 samples. As shown in the Figure 1, we maintained the characteristics of the original dataset when comparing the distribution of words.

<p align="center">
<img src="images\word_distrib.png" class="center" width="55%"/>
  <br><em>Figure 1 - Word distribution</em>
</p>

**Data Analysis** <p align="justify">LLM models have a limited context window. To facilitate classification by the model, we decided to limit the input text to 2000 characters. This decision was based on the sample distribution illustrated in the Figure 2. Upon examining the statistics of the word count per complaint, we found that the third quartile is at 143 words, which translates to approximately 1000 characters in text length. Therefore, limiting the text to 2000 characters was a conservative decision.

<p align="center">
<img src="images\word_correl.png" class="center" width="35%"/>
  <br><em>Figure 2 - Correlation between number of words and text size</em>
</p>

**Model Selection** <p align="justify">The free tier offered by Google Colab provides us with a T4 GPU with 16GB of VRAM. This is more than enough to load models with 7B parameters. There are several open-source models like Mistral, Falcon, Zephyr, and Openchat, and this list is likely to grow over time. In this study, we will use Mistral, which has shown excellent performance in various benchmarks. If you wish to use other models, changing the code is quite straightforward; it only requires modifying the instruction structure.

<p align="center">
<img src="images\mistral_prompt.jpeg" class="center" width="42%"/>
  <br><em>Figure 3 - Mistral prompt template</em>
</p>

**Prompt Engineering** <p align="justify">We set up some prompt patterns to test on the test dataset, including zero-shot and few-shot with one and two dialogues [3]. We also created prompts with the task before and after the complaint, to check how well the model retained information. The Table 1 describes each of the prompts.

<p align="center">
<img src="images\prompts.png" class="center" />
  <br><em>Table 1 - Prompt characteristics</em>
</p>

**Multi-label Evaluation** <p align="justify">To evaluate the prompts, we first manually labeled the 202 cases in the test dataset. To give an idea, this step took about 3 hours. As it is a multi-label classification problem, we used precision, recall, and f1-score metrics provided by the classification_report function of sklearn. There are several ways to aggregate metrics, such as micro-average, macro-average, weighted average, and samples average. In this study, we used samples average, which is specifically designed for multi-label scenarios. It calculates metrics like precision, recall, and F1-score for each instance individually and averages them, thus effectively evaluating the model's performance on each sample by considering all its labels. This makes it particularly useful for assessing how well the model predicts the label set for each individual sample. In the Table 2 is the score comparison for each of the prompts [4].

<p align="center">
<img src="images\score_compare.png" class="center" width="40%"/>
  <br><em>Table 2 - Prompt score comparison</em>
</p>

<p align="justify">
According to the Table 3, the prompt with the highest f1 score was the one with the task after the complaint description with a two-example few-shot (p_tsk_aft_2s). Below is the detailed score:

<p align="center">
<img src="images\datailed_score.png" class="center" width="40%"/>
  <br><em>Table 3 - Winner prompt detailed score</em>
</p>

**Classification** <p align="justify">Finally, after selecting the best-performing prompt based on f1-score, we applied the model to the validation dataset with 2000 examples. The model took about 1:30 hours to execute this task. Teh results can be seen in the next topic.

## Results and Conclusions
<p align="justify">
Although the dataset has a balanced distribution of labels, the Figure 4 shows that the majority of complaints at some point mention issues related to recharge/payment, cancellation of line/plan, wrongful charges, and plan/benefits.

<p align="center">
<img src="images\class_quantity.png" class="center" width="45%"/>
  <br><em>Figure 4 - Class quantity</em>
</p>

<p align="justify">
As we are using a labeled dataset, we can compare it with the labels applied by the model. In the co-occurrence matrix (Figure 6), the row data represent labels made by customers, and the columns are labels applied by the model. It can be observed that the labels applied by Mistral 7B align with those marked by customers, as indicated by the dark blue highlights in the co-occurrences.

<p align="center">
<img src="images\frequency_matrix.png" class="center" width="60%"/>
  <br><em>Figure 6 - Co-occurrence matrix</em>
</p>

In addition to verifying the effectiveness of Mistral 7B, we found some insights from this study:
* <p align="justify"><b>Prompt Sensitivity:</b> The model demonstrates high sensitivity to prompt structure. The sequence of phrases significantly impacts its performance.
* <p align="justify"><b>Few-Shot Prompting Efficacy:</b> Incorporating examples in multi-turn conversations, as part of few-shot prompting, notably enhances the model's scoring ability.
* <p align="justify"><b>Bias in Tag Usage:</b> The model exhibits a tendency to favor tags provided in examples, resulting in an increased recall rate.

<p align="justify"><b>Future improvements proposal:</b> This study was made using Mistral 7B from main branch quantization (4-bit, with Act Order and group size 128g)[5], but there are some other versions avaiable that could be a better score, despite the time processing. Also there are other LLM modelas as Falcon, Zephyr, Openchat that can do this task better. A comparation between thos model would be a good exercice.

## References
* [1] https://arxiv.org/abs/2310.06825
* [2] https://blog.reclameaqui.com.br/reclame-aqui-bate-recorde-de-reclamacoes-em-dezembro-de-2021/
* [3] https://www.analyticsvidhya.com/blog/2023/09/power-of-llms-zero-shot-and-few-shot-prompting/
* [4] https://towardsdatascience.com/evaluating-multi-label-classifiers-a31be83da6ea
* [5] https://towardsdatascience.com/introduction-to-weight-quantization-2494701b9c0c
