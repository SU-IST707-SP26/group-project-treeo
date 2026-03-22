# WORKLOG.md
## 2026-03-22 - Searching for Data

**Context**: Find possible datasets that could be incorporated for policing and reporting

**Work Completed**:
- Found possible additional datasets regarding current policing and reporting (Ashley)
    - https://bjs.ojp.gov/library/publications/criminal-victimization-2024 - includes crimes not reported and why
    - https://www.icpsr.umich.edu/web/DSDR/series/57 - track changes in deployment and crime reporting over many jurisdictions
    - https://direct.mit.edu/rest/article/107/6/1734/117710/Smartphone-Data-Reveal-Neighborhood-Level-Racial - uses anonymized smartphone pings to track where police officers actually spend their time during their shifts

**Impact**: Download data that can be incorporated into our models

---

## 2026-03-06 - Modeling and Finalize Checkpoint

**Context**: Began modeling process.

**Work Completed**:
- Cleaned the dataset - filtering for assaults, removing columns with many nulls, clean date and time columns, handle missing values, encode categorical variables (Ashley)
- Created temporal features - year, month, day of week
- Created a spatiotemporal dataset - divided data into geographic cells and included time periods (Brealin)
- Built a baseline linear regression model (Brealin)
- Built a clustering model (Maddy)
- Finalized the midterm checkpoint and transferred modeling results into the document (Ashley)

**Files Created**:
- `checkpoint/models/baseline_models.ipynb` (Brealin)
- `checkpoint/Cleaning Dataset.ipynb` (Ashley)

**Impact**: M2.T1, M2.T2, M2.T3, M3.T1, M3.T2, M4.T1 complete. Beginning the modeling process

---

## 2026-02-27 - Project Meeting

**Context**: Met with the professor about direction of project (Ashley, Maddy)

**Work Completed**:
- Subset the data as there is too many rows currently - pick one type of crime to explore
- Be aware of the noise in the data and how reporting and logging of crimes is not always reliable
- Look for more datasets to bring in, especially current police deployment and its influence on crime reporting
- Identified near term (predicting hotspots) and far term goals (incorporating police presence - could be theoretical)

**Impact**: Solid plan moving forward

---

## 2026-02-22 - Finalize EDA and Begin Checkpoint

**Context**: Finalize EDA and plan for midterm checkpoint

**Work Completed**:
- Complete more EDA, creating histograms, scatterplots, and correlation matrix (Ashley)
- Create submission file and plan for midterm checkpoint (Maddy)
- Begin working on midterm checkpoint (Maddy)

**Files Created**:
- `checkpoint/submission.ipynb`

**Impact**: M1.T2, M1.T3, M1.T4 complete.

---

## 2026-02-15 - Project Planning

**Context**: Created intial workplan for the project

**Work Completed**:
- Finalized workplan.md (Ashley)

---

## 2026-02-08 - Project Kickoff (Team)

**Context**: Set up project infrastructure and complete initial EDA

**Work Completed**:
- Downloaded LA crime dataset from Data.gov Open Portal (Maddy)
- Dataset has 28 columns and over 1 million observations over a 6 year period
- Set up repository structure (admin/, work/, data/)
- Created initial VISION.md (Ashley)

**Files Created**:
- `checkpoint/Exploratory Data Analysis.ipynb`

**Impact**: M1.T1 complete. Project infrastructure in place
