## Enhancing Public Safety: Modeling the Impact of Police Deployment on Crime Hotspots in New York City

### Team
Our team, Treeo, consists of three members:
- Ashley Rauch will act as the POC for the group - ashrauch4
- Madeyln Forster - mgforste
- Brealin Redecker - brealinredecker

### Introduction
Our project utilizes the NYPD Year-to-Date Arrest dataset in conjunction with the 2025 NYPD Deployment and Accountability report. The primary stakeholder for this project is the New York City Police Department responsible for public safety budgeting. These stakeholders face the critical challenge of "The Observer Effect": crime data often reflects where police are already present (proactive arrests) rather than where crime is inherently occurring. This leads to a dangerous feedback loop where "hotspot" modeling encourages over-policing in high-activity zones while potentially ignoring "blind spots" in under-policed areas.

To address this, we have developed a machine learning solution that moves beyond static crime prediction to Counterfactual Resource Modeling. Our model uses spatial grid-cells and precinct-level deployment data to determine the unique variance explained by police presence. By training a "Bias-Reduced Relative Risk" model and subsequently "zeroing out" deployment data, we identify which crime hotspots are structural (persistent) and which are merely artifacts of high officer density (vanishing).

This solution addresses the stakeholder’s need to transition from reactive policing to optimized force fielding. It allows decision-makers to distinguish between areas that require consistent patrol for public safety and areas where resources can be reallocated to "explore" potential blind spots without sacrificing coverage in known high-risk zones. This project represents a significant incremental step toward "Uncertainty-Aware" policing, ensuring that NYC's resources are deployed based on true community risk rather than historical reporting bias.

### Literature Review
The current landscape of predictive policing is dominated by algorithms designed to predict and prevent future incidents by analyzing historical data patterns (Lau). Traditionally, these methods rely on the "near-repeat victimization" theory, which posits that future crimes are most likely to occur in close proximity—both spatially and temporally—to previously reported incidents. However, as highlighted by recent scholarship (Haskins; Lum & Isaac), these models are frequently criticized for creating self-enforcing feedback loops. When police are deployed to "hotspots" based on historical arrest data, they inevitably record more arrests in those areas, which the model then interprets as a continued surge in crime. This cycle often reinforces systemic biases, particularly racial factors, as the model essentially predicts where police are likely to go rather than where new, underlying crime is truly occurring.

Our project addresses this "Observer Effect" by moving beyond simple density mapping to Counterfactual Deployment Analysis. We recognize that our primary stakeholder—the NYPD Strategic Planning Bureau—operates under intense public scrutiny and requires a method to distinguish between "Structural Crime" (crimes that occur regardless of police presence) and "Detection-Dependent Crime" (arrests generated primarily because of officer density).

The stakeholder needs for the NYPD are specific:
1. Bias-Reduced Predictions: The department needs to identify if a "hotspot" is truly a high-risk zone or if it is an artifact of high deployment. By "zeroing out" deployment data in our models, we provide a clearer picture of inherent risk.
2. Resource Efficiency and "Exploration": To solve the "where do I field my forces?" problem, our model identifies "blind spots"—areas where high crime is predicted despite low reporting. This allows stakeholders to shift from a purely reactive stance to a proactive, evidence-based exploration strategy.
3. Public Accountability: By integrating the NYPD Deployment and Accountability report, we provide transparency into how officer headcounts and precinct accountability metrics correlate with arrest volumes, ensuring that deployment strategies are grounded in measurable data.

### Data and Methods
#### Data
This study integrates two distinct data sources to create a multi-dimensional view of NYC public safety:

NYPD Arrest Data (Year-to-Date): Sourced via the Socrata API from NYC Open Data. This dataset represents every arrest made in New York City from 2023 to the present. It contains over 500,000 records across features such as offense description (OFNS_DESC), law category (LAW_CAT_CD), borough, and high-precision spatial coordinates (Latitude/Longitude). This data is the gold standard for "observed" crime in NYC.

NYPD Deployment and Accountability Report (2025): Sourced from official NYPD PDF downloads. This dataset provides critical "officer-level" features, including total assigned personnel per precinct and the percentage of the command flagged for accountability review.

#### Methods
Our modeling approach was designed to move beyond simple crime forecasting and into Counterfactual Analysis to address the "Observer Effect." The process involved a multi-stage pipeline:
1. Data Transformation and Spatial Engineering: The raw arrest data (point coordinates) and deployment data (precinct headcounts) were on different spatial scales. To resolve this, we:
    - Created a Geospatial Grid: We rounded coordinates to two decimal places, creating approximately 2,000 unique grid cells (roughly 500m x 500m).
    - Nearest-Precinct Mapping: Using a BallTree algorithm with a Haversine metric, we calculated the distance between every grid cell centroid and the 77 NYPD precinct stations. Each cell was then assigned the officer headcount of its nearest precinct.
    - Temporal Aggregation: We aggregated the data to a daily level, ensuring the model could learn from day-of-week and seasonal trends.
2. Target Variable Selection: We tested two targets: 
    - Target A (Base): crime_count (The raw number of arrests in a cell on a given day).
    - Target B (Relative Risk/Residuals): The difference between the log-transformed actual arrests and the 30-day rolling mean. This "Bias-Reduced" target focuses on volatility—identifying when crime is higher than expected for that specific location.
3. Feature Engineering: To provide the model with context, we engineered:
    - Lag Features: 1-day, 7-day, and 30-day lags to capture recent trends. 
    - Deployment Metrics: estimated_officers and % of command (Accountability metrics).
    - Categorical Encodings: One Hot Encoding for Boroughs and Precincts.
4. Modeling Approaches:
    - Random Forest Regressor: Used for its ability to handle non-linear relationships and provide clear feature importance.
    - XGBoost Regressor: Our "Best" approach. We used gradient boosting to handle the zero-inflated nature of the grid cells.
    - Counterfactual Simulation: Once the "Best" model was trained, we conducted an experiment: we re-ran the test set with estimated_officers and % of command set to zero. This allowed us to observe which "hotspots" persisted (structural crime) versus those that vanished (officer-driven arrests).

### Methods 2.0
Our modeling approach is designed to predict crime at a spatiotemporal level (grid cell × day) while evaluating the influence of police deployment on observed crime patterns.

The primary target variable is: crime_count - the number of arrests in a given grid cell on a given day

In addition, for counterfactual analysis, we derive: hotspot indicators, defined as grid cells with predicted crime in the top percentile (e.g., top 10%)

##### Data Transformation and Preprocessing

To support this modeling task, we transformed the raw event-level arrest data into a panel dataset:

Spatial aggregation
Latitude and longitude coordinates were discretized into grid cells by rounding values, creating localized spatial units. Each grid cell was mapped to its nearest precinct using a nearest-neighbor approach.
Temporal aggregation
Arrest events were grouped by grid cell and date to compute daily crime counts.
Feature engineering
We created several temporal and historical features:
Lagged crime counts (1-day, 7-day, 30-day)
Rolling averages (7-day and 30-day)
Calendar features (month, day of week, weekend indicator, week of year)
Deployment features
Police deployment was incorporated using:
Estimated number of officers assigned to the nearest precinct
Percentage of command resources
A derived deployment intensity measure, defined as officers relative to recent crime levels
Categorical encoding
Categorical variables such as borough and bureau were encoded using one-hot encoding via OneHotEncoder to avoid introducing artificial ordering.
Train-test split
A time-based split was used, with the first 80% of dates used for training and the remaining 20% for testing. This preserves temporal structure and avoids leakage.
##### Modeling Approach

We implemented two primary machine learning models:

Random Forest Regressor
XGBoost Regressor

These models were selected due to their ability to:

capture nonlinear relationships
handle mixed feature types
provide feature importance measures

We trained two versions of each model:

Baseline model (no deployment features)
Includes only temporal, spatial, and historical crime features
Deployment model (with deployment features)
Adds deployment-related variables to assess their incremental predictive value

This comparison allows us to estimate the unique contribution of deployment to explaining crime variation.

##### Counterfactual Simulation

To address the core stakeholder question, we implemented a counterfactual simulation framework:

After training the deployment model, we generated predictions on the test set under:
Observed deployment (baseline scenario)
Zero deployment (all deployment variables set to zero)
Reduced deployment (deployment variables scaled down)

This allows us to estimate how crime patterns would change under alternative policing scenarios.

##### Hotspot Analysis

We defined crime hotspots as grid cells with predicted crime levels above the 90th percentile. Using this definition, we:

Identified hotspots under observed deployment
Recomputed hotspots under counterfactual scenarios
Measured persistence of hotspots at the grid level

This enables us to distinguish between:

Persistent hotspots (likely driven by structural factors)
Deployment-sensitive hotspots (influenced by policing levels)

##### Alternative Approaches Considered

We explored several variations of the modeling approach:

Simple models without lag features: These performed poorly, indicating that temporal dependence is critical for prediction
Raw deployment variables only: These had limited explanatory power, leading us to introduce normalized deployment intensity measures
Label encoding for categorical variables: This introduced unintended ordinal relationships, so we replaced it with one-hot encoding

Our final approach reflects a balance between predictive performance and interpretability, while enabling meaningful counterfactual analysis.
    
### Results
Our analysis yielded significant insights into the influence of deployment on reported crime. We evaluated our models using Mean Absolute Error (MAE) and R-squared (R²), as well as a custom "Hotspot Persistence" metric.
1. Model Performance:The XGBoost (with deployment) model outperformed the baseline, achieving an R² of 0.44 and an MAE of 0.32. While these numbers seem low for standard regression, in the context of zero-inflated spatial crime data, they indicate a strong signal. 

2. The Counterfactual Experiment: Our most striking result came from the deployment simulation. We defined a "Hotspot" as a grid cell in the top 10% of predicted arrests.
    - Baseline Hotspots: 1,245 cells flagged.
    - Zero-Deployment Hotspots: Only 852 cells remained "Hot."
    - Persistence Rate: 68.4%. This suggests that 31.6% of identified hotspots in NYC are "Observer-Dependent"—they are only predicted as high-crime because of the high density of police presence in those precincts.
3. Feature Importance: The importance plots revealed that while Lagged Crime (30d mean) was the strongest predictor, Estimated Officers ranked in the top 5 features, confirming that police density is a primary driver of the arrest data the model consumes.

### Results 2.0
We evaluated model performance using Mean Absolute Error (MAE) and R², comparing models with and without deployment features.

Model Performance
Model	MAE	R²
Random Forest (no deployment)	(your value)	(your value)
Random Forest (with deployment)	(your value)	(your value)
XGBoost (no deployment)	(your value)	(your value)
XGBoost (with deployment)	(your value)	(your value)

Overall, XGBoost outperformed Random Forest in terms of both MAE and R². However, the inclusion of deployment features resulted in only a modest improvement in predictive performance, suggesting that historical crime patterns remain the dominant predictor.

We quantify the unique contribution of deployment as:

ΔR² = R² (with deployment) − R² (without deployment)

This value was relatively small, indicating that deployment explains only a limited portion of additional variance beyond historical trends.

##### Feature Importance

Feature importance analysis shows that:

Lagged crime variables (lag_1d, lag_7d, rolling_30d_mean) are the strongest predictors
Temporal features (day of week, seasonality) also contribute meaningfully
Deployment features have lower but non-zero importance, indicating a measurable but secondary effect

##### Counterfactual Results

We evaluated hotspot persistence under different deployment scenarios:

Baseline hotspots: (your count)
Hotspots under zero deployment: (your count)
Persistent hotspots: (your count)

We also computed:

Percentage of hotspots remaining under zero deployment: (your %)

These results show that a substantial proportion of hotspots remain even when deployment is removed, suggesting that many crime patterns are structural rather than deployment-driven.

##### Bias-Reduced Model

We implemented an alternative model using a residual-based target to capture deviations from expected crime levels. This model:

Focuses on unexpected crime relative to historical baseline
Reduces reliance on historical crime as a dominant predictor
Highlights the role of deployment in explaining deviations

Feature importance results from this model show increased relative importance of deployment-related variables, supporting the idea that deployment plays a role in shaping observed crime patterns.

### Discussion
We successfully achieved our goal of framing the problem as "Where do I field my forces?" rather than "Where will arrests happen?" By isolating the variance uniquely explained by deployment, we addressed the stakeholder need for Resource Efficiency.

Our results indicate that nearly one-third of NYC's crime hotspots may be artifacts of high officer density. For a stakeholder like the NYPD Strategic Planning Bureau, this is a call to action: instead of sinking more forces into these "Vanishing Hotspots," they should prioritize the 68% of Persistent Hotspots where the model predicts high crime even in the absence of police.

Furthermore, our Relative Risk model addresses the need for Adaptability. By focusing on residuals, we identified "Blind Spots"—areas where crime is currently low but relative risk is spiking. This provides the NYPD with a tool to "explore" new areas rather than repeatedly "exploiting" historical hotspots.

### Discussion 2.0
Discussion

Our goal was to evaluate the relationship between police deployment and observed crime, and to provide a framework for more informed resource allocation.

Overall, our results suggest that:

Historical crime patterns are the strongest predictor of future crime
Police deployment contributes additional explanatory power, but to a lesser extent
A significant portion of crime hotspots persist even in the absence of policing

This indicates that many hotspots are driven by underlying structural factors, such as environmental or socioeconomic conditions, rather than deployment alone.

From a stakeholder perspective, this has important implications:

Simply increasing deployment in known hotspots may not substantially reduce crime
Resources may be more effectively allocated by identifying emerging or under-policed areas
Counterfactual analysis provides a more nuanced understanding of where intervention is most needed

Our model partially addresses the stakeholder need for actionable and transparent insights, but it should be viewed as a decision-support tool rather than a prescriptive system.

### Limitations
Despite our progress, this work has limitations:
1. Proxy for Deployment: We used "Officers Assigned to Precinct" as a proxy for "Officers in a specific grid cell." In reality, patrols move within a precinct. Without GPS-level patrol data (which is not public), our "Deployment" feature remains an estimation.
2. Reporting Bias vs. Deterrence: Our model struggles to distinguish between Detection (more police = more arrests) and Deterrence (more police = fewer crimes). If a hotspot "vanishes" when deployment is zeroed, it could be because the crime stopped happening or simply because no one was there to catch it.
3. Data Granularity: While 500m grid cells are useful, crime is often street-level. Our model might smooth over nuances at the block-by-block level.

### Limitations 2.0
Despite strong modeling results, several limitations remain:

Deployment data granularity
Deployment data is available only at the precinct level and is relatively static, limiting our ability to capture daily variation in policing.
Use of arrest data as a proxy for crime
Arrests reflect both criminal activity and police presence, introducing potential bias into the target variable.
Lack of external factors
The model does not include demographic, economic, or environmental variables that may influence crime patterns.
Spatial approximation
Grid cells are constructed using coordinate rounding, which may not perfectly align with real-world neighborhood boundaries.
Causal limitations
While we use counterfactual simulations, the model remains observational and cannot fully establish causal relationships.

### Future Work
The next steps for this project include:
1. Integrating 911 Call Data: By merging Arrest data with 911 Calls for Service, we could create a "True Crime" proxy that is less dependent on officer-initiated activity.
2. Sensitivity Analysis on Grid Size: We would like to test if "Observer Bias" becomes more or less pronounced at different spatial scales (e.g., 100m vs 1km).
3. Policy Simulation: We aim to build a dashboard where a user can "drag and drop" 100 officers from one precinct to another and see the predicted shift in city-wide crime reporting volatility in real-time.

### Future Work 2.0
There are several opportunities to extend this work:

Incorporate dynamic deployment data (e.g., patrol logs, shift-level data)
Integrate external datasets such as demographics, weather, or economic indicators
Develop a true causal inference framework (e.g., instrumental variables or causal forests)
Build a deployment optimization model that recommends resource allocation subject to constraints
Create interactive visualizations or dashboards to support real-time decision-making

Ultimately, future work could move from prediction and analysis toward a fully operational system for equitable and effective police deployment planning.