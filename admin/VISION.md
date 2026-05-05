# VISION.md

## Current Vision

### Project: Enhancing Public Safety - A Comprehensive Analysis of Geospatial Shifts in Los Angeles and Prediction of Crime Volatility

**Primary Stakeholder:** New York City Police Department

**Problem Statement:** New York City first responders, specifically the police department, currently use simplified predictive policing approaches that are subject to circular polciing loops and include biases which make it difficult for departments to make informed decisions about resource allocation that best protects its citizens. 

**Solution:** We will build a machine learning model that identifies the impact of officer resource deployment on hotspots in NYC. By using spatial grid-cells, precinct-level deployment data and temporal patterns we will train models with and without deployment data to determine the unique variance explained by police presence. In turn, we aim to inform which crime hotspots are structural and which are because of many officers being deployed there.

---

## Version History

### Version 1.0 - Initial Vision

### Project: Enhancing Public Safety - A Comprehensive Analysis of Geospatial Shifts in Los Angeles and Prediction of Crime Volatility

**Primary Stakeholder:** Government authorities who need to make informed decisions that maximize public safety, specifically the LA Police Department

**Secondary Stakeholders:** 
- City residents (understanding crime and deployment patterns)
- City planning (infrastructure decisions)

**Problem Statement:** Los Angeles government authorities, specifically the police department, currently lack predictive information about crime volatility and hotspots throughout the city. Predictive policing approaches are too simple as they are subject to near-repeat victimization, lack transparency, and include biases which make it difficult for departments to make informed decisions about resource allocation that best protects its citizens. 

**Solution:** We will build a machine learning model that predicts crime counts and intensity based on geographic units in LA. We will incorporate temporal patterns and other factors which will allow stakeholders to distinguish between chronic crime areas and emerging high-volatility areas that may need more attention as a way to proactively deploy resources.

**Change Reason:** 
1. Our initial models were mostly based on temporal features that are able to strongly predict crime count, but without deployment data, we weren't doing anything different from the current predictive policing algorithms.
2. Pivoted to focus on modeling the impact of deployment in NYC since we were able to access estimated officers in precincts.