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
Currently, predictive policing is the main approach to predict and prevent future crimes by analyzing large sets of data(Lau). It utilizes a variety of computer algorithms, such as neural networks, deep learning models, and clustering. This method traditionally is subjected to "near-repeat victimization", meaning crimes are more likely to happen nearby previously reported crimes. However, recent studies (Haskins) have found these models are often too simple and creates a self-enforcing feedback loop where police go to the same neighborhoods due to recent history rather than where new crime is actually occurring. However, these models also come with limitations, specifically regarding lack of transparency and inclusion of biases, especially racial factors. The LAPD had intially implemented predictive policing and has since begun to reduce their programs. 

Effective prediction of crime volatility and geospatial shifts is important to a number of stakeholders, and its effective use can have a powerful impact. 

First, and the primary stakeholder, government authorities are responsible for public safety, and crime incidents are a major public safety concern. They aim to reduce the number of crimes, fatalities, injuries, and economic impacts in the areas they govern. If crime volatility can be accurately predicted, they are able to distribute resources more accurately. For example, the daily deployment of police officers and the reason why a zone may be high risk. Moreover, it is important for future city planning and infrastructure developments.

Secondly, the city residents are directly impacted by crimes. The individuals in communities that may be "high-policed" deserve transparency and equity, with evidence the model isn't biased and based on old data. 

### Data and Methods
#### Data
Our project will utilize data from 'data.gov' and is a crime data set that gives crime information from 2020-Present in Los Angeles. The link to our data can be found here: https://catalog.data.gov/dataset/crime-data-from-2020-to-present. The data has 28 columns, a combination of string, integer, and float features, with over a million rows of data. As the data is government data, it must be accurate, ensuring it is reliable for model use. Also, according to the Freedom of Information Act, they are legally obligated to disclose information — including crime data and records of misconduct — under public records laws. The data includes meta deta, such as that it was published by the Los Angeles Police Department (LAPD), it is publically available data, and it was last updated on January 2, 2026.

#### Methods
To start, we plan on computing transformations and preprocessing. We plan on converting date and times into cyclical features and spatial binning to divide Los Angeles into uniform areas to make the data manageable. 

In terms of modeling, based off the critics of current approaches, we aim to use reinforced machine learning. We aim to run a random forest model to predict severity of a crime based on area volatility, time, location, day of week, etc. We also want to employ k-means clustering to analyze trends over time and see how the crime clusters have changed from 2020 to 2025. This leads into change point detection, which will allow us to find the "structural breaks" in the crime time-series for each area. To evaluate the models, we will use precision-recall curves rather than simple accuracy as high-crime events are rarer than low-crime events, making it more effective.

### Project Plan
2/2-2/16: EDA, data cleaning, initial summary graphs/descriptions
2/16-3/2: Initial analysis, first model and its effectiveness
3/2-3/16: Build off of the first model, explore its errors and areas for improvement. Begin to work on second model while improving on the first model.
3/16-3/30: Finish second model and have the first model established and ready to go.
3/30-4/13: Identify takeaways from our models and add anything we might think is necessary.
4/13-4/27: Finishing touches/making the project easily understandable.


Risks
This needs to be completed. 

This section will describe potential risks to the project. This should include both potential pitfalls and roadblocks, as well as any approaches to mitigation. What will you do if some aspect of your plan fails?

Footnotes
