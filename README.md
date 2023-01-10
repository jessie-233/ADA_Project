# ADA Project (Milestone 3)
## Title: How American political efforts affect their annual greenhouse gas (GHGs) emissions
## Abstract
Climate change is one of the world’s top topics today, and reducing greenhouse gas emissions is a heavy responsibility of the governments of major countries. However, there also exists objections. As the largest emitter of carbon dioxide per capita in the world, how did American politicians care about it, and what are their attitudes towards it? In this project we are eager to see how much the American politicians focus on the global warming topic and how their attitudes change throughout the 12 years of 2008-2020. By comparing the result with the actual total annual greenhouse gas emissions in the United States, we try to develop the real impact of American political efforts on their actual emissions, and how it is correlated. Additionally, we are also curious about the different demographic distribution among politicians with positive and negative attitudes towards reducing carbon dioxide emissions, which may give us some insights on what might have resulted in the negative attitudes.
## Research Questions
### Task 1: The real impact of American political efforts on their actual emissions, and how it is correlated
---
#### Task 1.1: How much did American politicians care about global warming
Calculate the number of occurrences of the quotations related to climate change issues every year from 2008 to 2020 (assuming that the number of occurrence of the topic in the newspaper is related with the politicians' attention to it), and divide it by the total number of quotations of the year.

**Expected result:** *political attention rate* = proportion of the quotations related to climate change issues every year

---
#### Task 1.2: How did the political attitudes towards mitigating global warming fluctuate between 2008-2020
Apply sentiment analysis to the quotations and score them from -1 to 1, with 0 as neutral, and 1 as most positive attitude. Then categorize them by certain score threshold into three sentiment groups: "NEGATIVE", "NEUTRAL" and "POSITIVE".

**Expected result:** *political support rate* = the fraction of quotations with positive attitudes

---
#### Task 1.3: What is the real impact of American political efforts on their actual emissions
Together with the actual annual greenhouse gas emissions data, construct a regression analysis of 
$$
\footnotesize
\begin{aligned} 
 emissions = & f(political\ attention\ value,\ political \ support\ rate)
\end{aligned}
$$ to see how significantly political efforts can affect th actual emissions.

*Discuss:* The casualty relationship is impossible to detect in this context, because the change of CO~2~ emissions can be also due to various non-political reasons, for example, the 2008 financial crisis and  COVID-19 pandemic.

---
### Task 2: How do politicians’ demographic factors affect their attitudes to this issue 

Demographic Factors: party affiliation, nationality, gender, ethnic group, occupation,  religion, age, education level

Show different demographic distribution among speakers with positive and negative attitudes, and analyze what might have resulted in the negative attitudes.

## Proposed additional datasets
-   Metadata about the speakers in the Quotebank dataset (speaker_attributes.parquet): We will assign each speaker his party affiliation, age, gender, ethnic group, academic degree, religion from this dataset
    
-   Total annual greenhouse gas emissions in the United States from 2008 to 2019: the data is in csv format with a shape of (8,12). Columns are years from 2008 to 2019. Rows are GHG emissions in 7 sectors, including transportation, electricity generation, industry, agriculture, commercial, residential, and U.S. territories. Last row is the total amount of GHG in all 7 sectors. We plan to draw a line stacked chart ([one example here](https://github.com/epfl-ada/ada-2021-project-dataminers/blob/main/pics/us-ghg-emissions.png?raw=true)) to visualize the trend and use the data to perform a regression analysis with the results from quotebank.
(Source: EPA's annual Inventory of the U.S. Greenhouse Gas Emissions and Sinks [Greenhouse Gas Inventory Data Explorer | US EPA](https://cfpub.epa.gov/ghgdata/inventoryexplorer/#allsectors/allsectors/allgas/econsect/all))
## Methods
![workflow](https://raw.githubusercontent.com/jessie-233/Pics/main/workflow.png)
<center><b>Workflow</b></center>

* **Information retrieval**: collect climate change related quotations for each year
	* method: basic search engine using regular expression
	
* **Sentiment analysis**: assign each quotation a sentiment score (from -1 to 1, with 0 as neutral, and 1 as most positive attitude)
	* method: using `nltk` [Vader](https://github.com/cjhutto/vaderSentiment) toolkit

* **Observational study**: visualize demographic distribution among speakers with positive and negative attitudes, and analyze what might have resulted in the negative attitudes
	* method: turn categorical columns into dummy variables $\rightarrow$ use `causalinference` package to estimate Inverse Propensity Score Weight (IPSW) and calculate Average Treatment Effect (ATE) $\rightarrow$ compare ATE of each group and draw conclusions
  
## Contributions 
**Maocheng Xu**: Wiki data cleaning, Sentiment analysis, Webpage visualization
**Yu Zhou**: Computing platform construction, Matched observational study
**Yinghui Jiang**: Quotes data cleaning, Webpage copywriting
**Jingqi Liu**: Quotation retrieval, plotting figures during data analysis, regression analysis
