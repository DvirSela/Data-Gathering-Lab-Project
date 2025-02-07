
<h1 align='center' style="text-align:center; font-weight:bold; font-size:2.5em"> Optimizing Job Recommendation Systems Using worker Profile Embeddings</h1>

<p align='center' style="text-align:center;font-size:1em;">
    Dvir Sela
    Peleg Michael
    Samuel Guetta
    <br/> 
    Technion - Israel Institute of Technology
</p>


<br>
<br>

# Contents
- [Overview](#Overview)
- [Abstract](#Abstract)
- [Running the code](#Running-the-code)
  - [Scraping](#Scraping) 🪥
  - [Assign workers to job listings](#Assign-Workers-to-Job-Listing)👜
  - [Running tests and visualiztions](#Running-tests-and-visualiztions) 🔬
  
# Overview

Our goal is to develop a recommendation system that helps companies and employers connect with job candidates who are the best fit for the job.

# Abstract

In today’s job market, connecting companies with the right people for the job is more challenging than ever. Common candidate evaluations rely on simple keyword searches or filters, which don't really capture the full picture of someone's skills, background, or career goals. This often results in job suggestions that miss the mark and fail to reflect a candidate's true potential.
To address this, we explored the use of machine-learning-based Natural Language Processing (NLP) embedding models to embed worker profiles and job listings into numerical vectors and meta industries - a broad representation of various industry categories that group similar sectors together. By turning text data, such as work experience, education, and job descriptions, into meaningful semantic vectors, we can better understand how similar a person’s profile is to a job posting.

# Running the code
Each following sections should be run in the order we describe. Farthermore, after scraping we uploaded the scraped data in to the given DataBricks server, and it should be taken into account when running localy. 
##  Scraping
The code for scraping [monster.com](https://www.monster.com/) jobs is found in [scraping.ipynb](Scraping%20Code/scraping.ipynb).<br>
You should provide a .env file with the following parameters:
```python
USER = 'USER'  # BrightData username
PASS = 'PASS'  # BrightData password
```
## Assign Workers to Job Listings
This is the main part of the code, that matches job listing into K users. The code is found in [main.ipynb](Databricks%20Code/main.ipynb).<br> 
You will be greeted with the following parameters, and can change them at your will to get different results:
```python
N = 20_000
seed = 42
k = 10
max_sentence_length = 512
show_null = True
save_to_dbfs = True
index_model = 1
models_list = ['all-MiniLM-L6-v2', # Bert
                'all-distilroberta-v1', # roberta
                'multi-qa-distilbert-cos-v1' # distilberta
                ]
```
The parameters are:
- `N` - number of samples
- `seed` - seed for randmoness
- `k` - number of users to get for each job listing
- `show_null` - bool, will determine if to show null checks or skip
- `save_to_dbfs` - bool, will determine if to save results to dbfs
- `index_model` - the index of the chosen model in the model list
- `models_list` - list of models to use for the embeddings
## Running tests and visualiztions
This is the part of the code that runs the tests and visualiztions.
- The notebook for plotting the T-SNE is [TSNE.ipynb](Databricks%20Code/TSNE.ipynb)
- The notebook for plotting meta-industry percentages is [TSNE.ipynb](Databricks%20Code/TSNE.ipynb)
- The notebook for running the test as mentioned in the report is [test.ipynb](Databricks%20Code/test.ipynb)
