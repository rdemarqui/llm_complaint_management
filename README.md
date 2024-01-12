<div align="center">
  <h1>Decoding User Complaints: An Analysis using Mistral 7B LLM</h1>
</div>

<p align="center">
<img src="images\cover.png" class="center" width="45%"/>
</p>

## Overview
Analyzing user complaints is a crucial challenge for many organizations, involving understanding and effectively responding to customer concerns. One of the main challenges is managing the variety and complexity of complaints, which vary significantly in language and content, posing difficulties for accurate interpretation. Moreover, the high volume of complaints necessitates automated processes for efficient management. Effective analysis should identify underlying causes and trends, requiring sophisticated approaches that understand nuances and patterns in user complaints. Large Language Models (LLMs) are emerging as vital tools for dealing with these types of business problems.

In recent years, we have witnessed a surge in the development of open-source Large Language Models (LLMs), a phenomenon that is redefining the boundaries of Artificial Intelligence (AI) and Natural Language Processing (NLP). Among the most notable innovations in this area is the quantization of models, a technique that reduces model size and computational requirements, allowing its use in affordable machines while reducing budgetary costs.

This study aims to leverage these technological advancements, specifically employing the advanced LLM tool Mistral 7B [1], to analyze a comprehensive dataset of user complaints sourced from (reclameaqui.com.br)[https://www.reclameaqui.com.br/]. Through this analysis, we intend to demonstrate the potential and effectiveness of LLMs in interpreting and handling large-scale user feedback.

## Objectives
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
The data was collected from the website reclameaqui.com, which is a Brazilian website with over 30 million registered consumers and 500,000 registered companies on the platform, where 1.5 billion pageviews occur annually [2]. A total of 7,000 distinct complaints from a telecommunications provider were collected. This complaints was classified by the users into 14 unique categories, therefore, we have a balanced dataset with 500 complaints per category.

## Methodology
First, a script was created to scrape company data, and for this task, Python packages Selenium and BeautifulSoup were used. The script is available in the repository with the name `01. webscrapping_reclameaqui.ipynb`

To do

## Results and Conclusions
Some findings in this study:
* The model is very sensitive to the prompt. The order of phrases matter.
* Using examples in multi-turn conversation, as a few-shot prompting improved model score.
* Model tends to use more the tag given as a example, increasing recall.

**Future improvements proposal:** This study was made using Mistral 7B from main branch quintization (4-bit, with Act Order and group size 128g), but there are some other versions avaiable that could be a better score, despite the time processing. Also there are other LLM modelas as Falcon, Zephyr, Openchat that can do this task better. A comparation between thos model would be a good exercice.

## References
* [1] https://arxiv.org/abs/2310.06825
* [2] https://blog.reclameaqui.com.br/reclame-aqui-bate-recorde-de-reclamacoes-em-dezembro-de-2021/
* https://www.analyticsvidhya.com/blog/2023/09/power-of-llms-zero-shot-and-few-shot-prompting/
