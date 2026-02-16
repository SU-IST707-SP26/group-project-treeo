# WORKPLAN.md

## Active Plan

### Milestone 1: Data Acquisition
- [] M1.T1 — Download LA Open Data crime dataset
- [] M1.T2 — Initial exploratory data analysis
- [] M1.T3 — Identify crime types for prediction
- [] M1.T4 — Determine specific modeling techniques

### Milestone 2: Data Preparation
- [] M2.T1 — Clean crime data (remove nulls or duplicates, normalize fields)
- [] M2.T2 — Extract temporal features (hour, day, month, year)
- [] M2.T3 — Create basic features (lagged and rolling statistical features)
- [] M2.T4 — Identify if dimensionality reduction is necessary

### Milestone 3: Spatial Resolution
- [] M3.T1 — Validate and filter spatial coordinates
- [] M3.T2 — Divide the spatial data into uniform geographic cells
- [] M3.T3 — Map and aggregate crime within each cell
- [] M3.T4 — Implement change point detection techniques

### Milestone 4: Modeling Attempts
- [] M4.T1 — Train/test split by date
- [] M4.T2 — Logistic regression baseline
- [] M4.T3 — Random Forest model

### Milestone 5: Advanced Modeling
- [ ] M5.T1 — Implement spatial lag and rolling features
- [ ] M5.T2 — Time series models for temporal patterns
- [ ] M5.T3 — Refine and tune techniques with different hyperparamters
- [ ] M5.T4 — Combine and/or add other approaches

### Milestone 6: Evaluation and Visualization
- [ ] M6.T1 — Comprehensive test set evaluation using time aware techniques and other common metrics
- [ ] M6.T2 — Map visualizations of the LA area
- [ ] M6.T3 — Final documentation

---

## Changelog