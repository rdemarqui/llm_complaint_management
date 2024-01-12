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
This study aims to leverage these technological advancements, specifically employing the advanced LLM tool Mistral 7B [1], to analyze a comprehensive dataset of user complaints sourced from https://www.reclameaqui.com.br/. Through this analysis, we intend to demonstrate the potential and effectiveness of LLMs in interpreting and handling large-scale user feedback.

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
<p align="justify">
<b>data extraction:</b> First, a script was created to scrape company data, and for this task, Python packages Selenium and BeautifulSoup were used. The script is available in the repository with the name `01. webscrapping_reclameaqui.ipynb`

<p align="justify">
<b>Data Cleaning:</b> To work with the complaints, we initially performed a simple cleaning, removing double spacing and converting all text to lowercase. We then replaced the mask inserted by 'reclame aqui' with a smaller one, aiming to only reduce the size of the text. Finally, we removed texts shorter than 3 characters as they lacked sufficient information for analysis.

<p align="justify">
<b>Stratification:</b> As this work is solely for study purposes and given the limitations of the Colab free tier, we performed a stratified sampling of the complaints, divided into two datasets. The first set contained 202 samples and served as the test dataset, and the second contained 2000 samples. As shown in the figure below, we maintained the characteristics of the original dataset when comparing the distribution of words.

<p align="justify">
<b>Data Analysis:</b> LLM models have a limited context window. To facilitate classification by the model, we decided to limit the input text to 2000 characters. This decision was based on the sample distribution illustrated in the figure below. Upon examining the statistics of the word count per complaint, we found that the third quartile is at 143 words, which translates to approximately 1000 characters in text length. Therefore, limiting the text to 2000 characters was a conservative decision.

<p align="justify">
<b>Model Selection:</b> The free tier offered by Google Colab provides us with a T4 GPU with 16GB of VRAM. This is more than enough to load models with 7B parameters. There are several open-source models like Mistral, Falcon, Zephyr, and Openchat, and this list is likely to grow over time. In this study, we will use Mistral, which has shown excellent performance in various benchmarks. If you wish to use other models, changing the code is quite straightforward; it only requires modifying the instruction structure.

<p align="justify">
<b>Prompt Engineering:</b> We set up some prompt patterns to test on the test dataset, including zero-shot and few-shot with one and two dialogues. We also created prompts with the task before and after the complaint, to check how well the model retained information. The table below describes each of the prompts.

<p align="justify">
<b>Multi-label Evaluation:</b> To evaluate the prompts, we first manually labeled the 202 cases in the test dataset. To give an idea, this step took about 3 hours. As it is a multi-label classification problem, we used precision, recall, and f1 score metrics provided by the classification_report function of sklearn. There are several ways to aggregate metrics, such as micro-average, macro-average, weighted average, and samples average. In this study, we used samples average, which is specifically designed for multi-label scenarios. It calculates metrics like precision, recall, and F1-score for each instance individually and averages them, thus effectively evaluating the model's performance on each sample by considering all its labels. This makes it particularly useful for assessing how well the model predicts the label set for each individual sample. Below is the score comparison for each of the prompts.

According to the table above, the prompt with the highest f1 score was the one with the task after the complaint description with a two-example few-shot (p_tsk_aft_2s). Below is the detailed score:

<p align="justify">
<b>Classification:</b> Finally, after selecting the best-performing prompt, we applied the model to the validation dataset with 2000 examples. The model took about 1:30 hours to execute this task. Teh results can be seen on the next topic.

## Results and Conclusions
Some findings in this study:
* The model is very sensitive to the prompt. The order of phrases matter.
* Using examples in multi-turn conversation, as a few-shot prompting improved model score.
* Model tends to use more the tag given as a example, increasing recall.

<b>Future improvements proposal:</b> This study was made using Mistral 7B from main branch quintization (4-bit, with Act Order and group size 128g), but there are some other versions avaiable that could be a better score, despite the time processing. Also there are other LLM modelas as Falcon, Zephyr, Openchat that can do this task better. A comparation between thos model would be a good exercice.

## References
* [1] https://arxiv.org/abs/2310.06825
* [2] https://blog.reclameaqui.com.br/reclame-aqui-bate-recorde-de-reclamacoes-em-dezembro-de-2021/
* https://www.analyticsvidhya.com/blog/2023/09/power-of-llms-zero-shot-and-few-shot-prompting/
