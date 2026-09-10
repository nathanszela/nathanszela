# Nathan Szelagowski

MSc Business Engineering — Data Analytics, Ghent University.
I work on the part of data science that happens before the model: understanding the business question, finding out what the data can and cannot support, and saying so plainly.

Available from **January 2027** for a six-month internship in Spain (data, analytics, or fintech), funded by an **Erasmus+ Traineeship for Graduates** grant. The tripartite Learning Agreement is provided by my university, so no Spanish *convenio de prácticas* is needed.

📍 Belgium → Spain · 🗣️ French (native), English (C1), Dutch (B2), Spanish (improving)
[LinkedIn](https://www.linkedin.com/in/nathan-szelagowski/) · nathan.szelagowski@gmail.com

---

## About this profile

Most of my work so far was done under university or client confidentiality agreements: the code and the data belong to the companies involved and are not mine to publish. What follows describes the methods and what I learned from them. I am happy to walk through any of it in detail, including the parts that did not work.

---

## Selected work

### Price suggestion for C2C resale — 1st place, in-class Kaggle competition
*MSc Machine Learning, UGent, with Crunch Analytics · team of 4 · Oct–Dec 2025*

Predicting the asking price a private seller sets for a second-hand item, from the listing title, description, brand, category and condition.

The pipeline that won it was a mixture of experts rather than one large model. We embedded six concatenated product fields with an LLM (Gemma, run locally through Ollama), clustered the embeddings with Mini-Batch K-Means into 14 groups that we mapped onto 8 readable themes, compressed to 200 principal components, then trained one specialised LightGBM per theme.

The reasoning: pricing a used iPhone and pricing a vintage handbag are different problems. One depends on specifications, the other on a subjective condition assessment. A single global model has to average over both.

We benchmarked the specialised models against fifteen alternatives under one evaluation harness: linear, ridge and lasso baselines, a GAM with smoothing splines, decision tree, bagging, random forest, BART, GBM, XGBoost, KNN, linear and polynomial SVR, and an MLP. Best validation RMSE was 26.5 for the specialised LightGBM, against 32.96 for the linear baseline and 26.8 for XGBoost.

One run went badly wrong: BART returned an RMSE of 821. We traced it to preprocessing rather than to the method, and reported it that way instead of quietly dropping the row from the table.

`R` `LightGBM` `XGBoost` `Ollama` `embeddings` `K-Means` `PCA`

---

### Water leak detection from household meter data
*Data analyst internship, Itineris (Ghent) · Jun–Jul 2025*

Itineris builds the billing and customer platform used by water and energy utilities. The assignment was advisory: recommend how leak detection should be approached for a US utility client, given only hourly consumption readings per meter.

Four weeks went into a data source nobody had used: roughly 600 undocumented XML files, one to three million rows each. No schema, no documentation. I reconstructed the structure field by field and reconciled it with the systems already in place.

The detection work started from the literature, which turned out to be mostly about pipeline sensors rather than individual meters, and mostly about data we did not have. What remained feasible on consumption data alone was a flow-variation approach (minimum night flow), tuned conservatively so that the leaks it flagged were the ones we could stand behind. Those conservative labels then trained a semi-supervised LightGBM over 284 time-series features selected with tsfresh.

The confusion matrix looked excellent. It should not have been trusted, and I said so in the final presentation: the model learned the rule-based labels, and train and test shared the same assumptions, so the apparent performance mostly measured agreement with the rule that generated the labels. The honest evaluation would require a technician checking a random sample of meters by hand, which is what I recommended.

`Python` `tsfresh` `LightGBM` `time series` `XML`

---

### Hotel investment feasibility study, California
*MSc Prescriptive Analytics, UGent, with Lighthouse · team of 6 · Feb–May 2026*

Where should a hotel group put its next California property, and what would it be worth? We treated it as a valuation problem rather than a ranking exercise: net present value from a ten-year unlevered DCF, with yield on cost and IRR reported alongside for triangulation.

Two models fed the revenue line. Average daily rate came from a CatBoost regressor over 113 features covering property specification, amenities, location, demographics and competitive context, validated with stratified 5-fold cross-validation by destination and interpreted with SHAP. Occupancy came from a four-step forecast combining two years of climatology with published industry consensus, carrying an explicit confidence band.

The cost side was built bottom-up rather than as a percentage of revenue: county-level accommodation wages, municipal hospitality wage ordinances with their scheduled increases, payroll load, and property tax under California's acquisition-value rule.

Of 552 candidate listings, two cleared a positive NPV. A 5,000-draw Monte Carlo over six uncertain inputs put the probability of a positive outcome just under 60% for both, with ADR estimation error dominating the variance. The recommendation was framed accordingly: a base case worth pursuing subject to re-underwriting, not a buy signal.

The client's data is confidential and is not reproduced here.

`Python` `CatBoost` `SHAP` `Monte Carlo` `DCF` `R Shiny` `geospatial`

---

### Master's thesis — natural disasters and multinational affiliates
*UGent · 2025–2026 · defence September 2026*

An empirical study of how natural disaster shocks affect the activity of multinational firms' foreign affiliates, on a firm-level panel of over 100,000 observations. Estimation with PPML and high-dimensional fixed effects, clustered standard errors, and robustness checks across alternative measures of disaster intensity.

Part of the work was arguing about what the disaster data actually measures. Reporting thresholds change over time and across countries, which mechanically affects any count-based measure, and results that ran against the expected sign are reported rather than dropped.

---

## What I am doing next

- Power BI, to the PL-300 standard (September 2026)
- Spanish, intensive course and immersion (October–December 2026)
- A Discord bot for clan-war management in Python, which will be the first thing on this profile with actual code attached

---

*Everything above was produced under academic or client confidentiality. Code and data are not published. Happy to discuss the methods and the trade-offs in an interview.*
