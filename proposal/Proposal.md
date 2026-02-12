## Enhancing Public Safety: A Comprehensive Analysis of Geospatial Shifts in Los Angeles and Prediction of Crime Volatility

### Team
Our team, Treeo, consists of three members:
- Ashley Rauch will act as the POC for the group - ashrauch4
- Madeyln Forster - mgforste
- Brealin Redecker (brealinredecker)

### Introduction
Our crime reporting dataset reflects all incidents of crime in the City of Los Angeles dating back to 2020, collected by The Los Angeles Police Department (LAPD). Ensuring the safety of the public is a fundamental responsibility of the government. Crime, of all levels, can lead to loss of life, physical injury, and significant economic and social impacts on individuals and communities. While a certain level of crime may be considered inevitable, we aim to uncover structural shifts in crime patterns and build a tool that predicts crime volatility and potential "hotspots". The tool will enable the development of evidence-based strategies in terms of resource allocation, prevention, and intervention to improve public safety. 

Many crime prediction models explore the association between a single factor, typically demographic data, and crimes. With the rise of AI and machine learning, predicting crime volatility is beginning to evolve from static hotspot mapping into predictive policing. Our approach will build on this by mapping dynamic systems and identifying when crime profiles change. This approach will allow stakeholders to distinguish between chronic crime areas and emerging high-volatility areas that may need more attention as a way to proactively deploy resources. Our dataset contains all the variables needed to successfully implement the approach and our models.

In Los Angeles, there was a peak in most crime categories during the pandemic. Since then, there has been an overall downward trend across many categories. However, crimes will always occur and the rates by neighborhoods are constantly changing. Success in this project will provide the LAPD and city administratives with a dyanmic resource allocation tool. It will ensure resources are present in emerging high-volatility zones rather than more stable ones as well as aid in future city infrastructure planning. More lives will be protected and the city will be a safer place to live.

### Literature Review
Currently, predictive policing is the main approach to predict and prevent future crimes by analyzing large sets of data (Lau). It utilizes a variety of computer algorithms, such as neural networks, deep learning models, and clustering. This method traditionally is subjected to "near-repeat victimization", meaning crimes are more likely to happen nearby previously reported crimes. However, recent studies (Haskins) have found these models are often too simple and creates a self-enforcing feedback loop where police go to the same neighborhoods due to recent history rather than where new crime is actually occurring. These models also come with limitations, specifically regarding lack of transparency and inclusion of biases, especially racial factors. The LAPD had intially implemented predictive policing and has since begun to reduce their programs. 

Effective prediction of crime volatility and geospatial shifts is important to a number of stakeholders, and its effective use can have a powerful impact. 

First, our primary and key stakeholder for this project is government authorities. Government authorities are responsible for public safety, and crime incidents are a major public safety concern. They aim to reduce the number of crimes, fatalities, injuries, and economic impacts in the areas they govern. For example, they are in charge of deploying limited personnel and resouces across a large and diverse city while maintaining efficiency and public trust. Current 'hotspot' models usually emphasize chronic high-crime areas which result in static deployment patterns and reinforce historical policing biases. Our model will be an analytical tool that can distiguish stable high-crime zones from emergencying high-volatility areas so teams like the LAPD will be able to better anticipate where crime risk is changing and be more effective.
Their needs are as follows:
1. Actionable Predictions: Teams require forward looking predictions that identify areas at elevated risk before crime surges occur. The outputs should be spatially specific and time bound.
2. Transparency: In order to maintain public trust, the model must be able to be clearly explained. Decision makers must understand why an area is flagged.
3. Adaptability to Changing Crime Patterns: Crime dynamics in Los Angeles shift significantly. The model must be capable of detecting structural changes over time rather than assuming patterns are static.

Secondly, the city residents are directly impacted by crimes. The individuals in communities that may be "high-policed" deserve transparency and equity, with evidence the model isn't biased and based on old data. 

### Data and Methods
#### Data
Our project will utilize data from 'data.gov' and is a crime data set that gives crime information from 2020-Present in Los Angeles. The link to our data can be found here: https://catalog.data.gov/dataset/crime-data-from-2020-to-present. The data has 28 columns, a combination of string, integer, and float features, with over a million rows of data. As the data is government data, it must be accurate, ensuring it is reliable for model use. Also, according to the Freedom of Information Act, they are legally obligated to disclose information — including crime data and records of misconduct — under public records laws. The data includes meta deta, such as that it was published by the Los Angeles Police Department (LAPD), it is publically available data, and it was last updated on January 2, 2026.

Metadata link: https://data.lacity.org/Public-Safety/Crime-Data-from-2020-to-Present/2nrs-mtv8/about_data
#### Methods
Our modeling approach, as of now, is going to be implementing supervised machine learning models, particularily regression and a tree-based model, to predict crime intensity and votality across spatial grid cells. To ensure operational revelance and transparency, our model will prioritize interpretable methods and forward-looking predicitons rather than prescriptive enforcement actions.

Before beginning to build our model, we need to complete the necessary preprocessing, which may include: removing duplicate or incomplete records, validating and filtering spatial coordinates, extracting temporal features such as month, year, and day of the week, creating lagged and rolling statistical features, and normalizing where necessary to ensure stable model performance.

First, we will need to take the crime incidents and aggregate them using a grid-based spatial framework, dividing LA into uniform geographic cells. Each incident will be assigned to a grid cell based on its latitude and longtitude. The crime counts will then be aggregated within each cell over fixed time intervals in order to produce a consistent spatiotemporal dataset.

The second step will be to identify shifts in crime patterns using change point detection techniques to the time series of crime counts within each grid cell. This will show us the statistically significant changes, giving us the ability to pinpoint crime behavior changes and document appropriately.

We would then want to create our baseline model using regressions. Creating interpretable baselines for predicting crime counts within each grid cell.
Then we would use tree-based models to predict future crime intensity and the probability that a grid cell will experience high crime volatility. This model is a good choice because it has the capability to capture nonlinear relationships and interactions between time, location, and historical crime behaviour.

Our model will be validated using a time aware technique such as rolling or walking-forward validation to simulate real-world forecasting conditions. Some of the metrics we can use for validation are MAE and RMSE for crime counts and precision, recall, and F1 score for the high-volatility areas.

### Project Plan
Period|Activity|Milestone|
|---|---|---|
|2/2 - 2/16|Data description and exploratory data analysis|Polished final dataset and completed data exploration
|2/16-3/2|Initial analysis and first regression model |Initial pass with cleaned data for baseline model
|3/2-3/16|Refinement and tuning of regression model, begin to work on random forest model|Finalized regression model and initial pass of random forest model
|3/16-3/30|Refinement and tuning of random forest model|Finalized random forest model
|3/30-4/13|Final evaluation and interpretation of the results of both models|Identify key takeaways from our models
|4/13-4/27|Finishing touches|Final report and slides

### Risks
There are several potential risks that may arise during this project.

The first key risk is data bias and reinforcement of historical policing patterns. It is the nature of crime data to reflect reported incidents which raises the possibility that the model may unintentionally emphasize areas that have historically recieved higher levels of police attention rather than the areas where crime risk is newly emerging. We must mitigate this risk by ensuring the model can predict the crime volatility and change.

The second key risk is model overfitting when using the tree-based models on data that can be considered high-dimensional. Overfitting will cause strong performance on the historical data but poor predictive accuracy when it comes to future time periods. We will need to mitigate this risk through using the time-aware validation methoids and compare their results against simpler regresion baselines.

The third key risk is our spatial aggregation choices. If we breakdown LA into grid cells that are too small, it will introduce noise and instability; however, if we breakdown LA into grid cells that are too large the crime patterns may become obscure. During our EDA we will need to explore different options for breaking up the locations and ensure we are selecting a grid size that balances predictive performance with interpretability.

In the event that any component of our project does not perform as expected, we will have to adapt our approach by researching new options or refining the methods at hand. An issue with dataset size can be resolved by using a smaller subset of our data. An issue with overfitting, can be resolved by utilizing more simplier models. If our geographical data is not giving us good insights we will troubleshoot and test different sizes.

### References
“Delivering Accountability: A Plan To Stop Crime in Our Communities.” Center for American Progress, 29 Jan. 2026, www.americanprogress.org/article/delivering-accountability-a-plan-to-stop-crime-in-our-communities/. 

Haskins, Caroline, et al. “Academics Confirm Major Predictive Policing Algorithm Is Fundamentally Flawed.” VICE, 9 Aug. 2024, www.vice.com/en/article/academics-confirm-major-predictive-policing-algorithm-is-fundamentally-flawed/. 

Lau, Tim. “Predictive Policing Explained.” Brennan Center for Justice, 1 Apr. 2020, www.brennancenter.org/our-work/research-reports/predictive-policing-explained. 

Turner, David. “Los Angeles County Crime Statistics & Trends (2020–2025).” Valley Alarm, 14 Oct. 2025, www.valleyalarm.com/los-angeles-crime-statistics/. 
