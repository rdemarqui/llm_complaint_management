<div align="center">
  <h1>LLM at Work: Decoding Customer Feedback</h1>
</div>

<p align="center">
<img src="images\cover.png" class="center" width="45%"/>
</p>

## Overview
Analyzing user complaints is a crucial challenge for many organizations, involving understanding and effectively responding to customer concerns. One of the main challenges is the variety and complexity of complaints, which can vary in language and content, making accurate interpretation difficult. Moreover, the high volume of complaints necessitates automated processes for efficient management. Effective analysis should identify underlying causes and trends, requiring sophisticated approaches that understand nuances and patterns in user complaints, large Language Models (LLM) are emerging as vital tools for deal with this type of business problem.

In recent years, we have witnessed a surge in the development of open-source Large Language Models (LLM), a phenomenon that is redefining the boundaries of artificial intelligence and natural language processing. Among the most notable innovations in this area is the quantization of models, a technique that optimizes performance without significantly compromising accuracy, allowing its use in affordable machines while reducing budgetary costs.

This study aims to explore these technological advancements, specifically using the advanced LLM tool Mistral 7B, to analyze a vast collection of complaints gathered from the website [reclameaqui.com.br](reclameaqui.com.br). Through this analysis, we intend to demonstrate the potential and effectiveness of LLMs in interpreting and handling large-scale user feedback.

## Objectives
Create a fast and automated system to categorize user complaints into one or more categories.

## Technologies Used
* `python 3.9.16`
* `pandas 1.5.3`
* `selenium 4.14.0`
* `BeautifulSoup 4.11.2`
* `seaborn 0.12.2`
* `transformers 4.37.0`
  
## About the Data
The data was collected from the website reclameaqui.com, which is a Brazilian website with over 30 million registered consumers and 500,000 registered companies on the platform, where 1.5 billion pageviews occur annually [1]. A total of 7,000 distinct complaints from a telecommunications provider were collected. This complaints was classified by the users into 14 unique categories, therefore, we have a balanced dataset with 500 complaints per category.

## Methodology
First, a script was created to scrape company data, and for this task, Python packages Selenium and BeautifulSoup were used. The script is available in the repository with the name `01. webscrapping_reclameaqui.ipynb`

To do

## Results and Conclusions
To do

## References
* [1] https://blog.reclameaqui.com.br/reclame-aqui-bate-recorde-de-reclamacoes-em-dezembro-de-2021/
* https://www.analyticsvidhya.com/blog/2023/09/power-of-llms-zero-shot-and-few-shot-prompting/
