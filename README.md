# COVID Trend Analysis

Using R to analyze COVID datasets based on county using various visualizations, data cleaning, regression analysis, LASSO techniques, residual tests, and more.

## Goal of the study: 

The goal of this study was to investigate the effectiveness of lockdowns in flattening the COVID curve, and to evaluate which county-level socioeconomic/demographic variables impacted the log death rate per 100,000 population using LASSO models. Throughout the project, we also show the dynamic evolution of state-level COVID cases and deaths.

## Data: 

The data includes: covid_county.csv, which contains county-level socioeconomic classification data from four tables (Income, Jobs, People, and County Classifications) from the USDA Economic Research Service. Covid_rates.csv contains daily cumulative numbers on infection and fatality for each county, and the data comes from the NY Times. Covid_intervention.csv contains county-level lockdown intervention data; this dataset is a manually compiled list of the dates that interventions/lockdown policies were implemented and lifted at the county level (source: JieYingWu’s github). To assemble the data, counties were uniquely identified using FIPS, with some cleaning for FIPS in NYC and only including states in the continental US. Additionally, we set the week of Jan 21, 2020 as the first week, and the dates are formatted properly. For data assembly, we merge the TotalPopEst2019 variable from the demographic data with covid_rates by FIPS. NA’s are replaced with zeroes. Lastly, we merge the demographic data sets by FIPS and output as covid_county.csv.

## Analyses: 

We conducted analyses of time series data (weekly and monthly) for different states, using heatmaps, spaghetti plots, and scatterplots for data visualization. We also used LASSO while forcing the factorized State variable in to analyze what variables impacted the response variable, which we put in log scale (log_total_death_per100k). Using lambda.1se, Anova, and backward elimination, we minimized our model, checked the linear model assumptions, and analyzed our summary of the model.

## Methods: 

The methods we use include LASSO model selection (forcing in certain variables, using penalty modification), k-fold cross validation, backward elimination, Anova analysis, summary statistics for linear and LASSO models, residual and Q-Q plots for linear model assumption analysis, and lubridate for time series analysis. We also use spaghetti plots, scatterplots, and heatmaps for data visualization. Packages: lm(), Anova, regsubsets(), glmnet(), cv.glmnet().

## Findings: 

Based on the final model, we can see that the state effect, controlling for other variables, significantly influences the log death rate per 100k. Several states show significant associations with the death rate, like California and Washington, among other states. For instance, California has a negative coefficient, with lower relative death rates, while some states like South Dakota and Montana have notably large positive coefficients, suggesting relatively higher death rates. Several other non-state variables show significant impact on the log death rate, such as PctEmpConstruction, PctEmpMining, and PctEmpAgriculture which exhibit negative coefficients, indicating that higher employment rates in these sectors are associated with lower COVID-19 death rates. Factors such as population density, age demographics (Age65AndOlderPct2010, Under18Pct2010), educational variables (Ed3SomeCollegePct, Ed5CollegePlusPct), migration rates (NetMigrationRate1019), and ethnic composition (WhiteNonHispanicPct2010, HispanicPct2010) also play significant roles in shaping the death rate. For instance, higher proportions of older adults and individuals with lower educational attainment are associated with higher death rates. Policy interventions to reduce the COVID death rate should be tailored to address state-specific needs, with increased help for states like Montana and South Dakota, which have higher relative death rates. Strategies should focus on enhancing healthcare infrastructure, promoting vaccination campaigns, implementing and enforcing public health measures (masks/social distancing), improving access to healthcare services (especially in rural areas/states), and providing adequate support to vulnerable populations, such as more accessible healthcare for the elderly and Hispanic populations.

## Limitations: 

To improve our model, we could have included some extra information, like the African American population percentage. The model could also be improved with more COVID-specific data, such as vaccination records based on the first dose, second dose, and booster, types of vaccines administered, data regarding masking and social distancing, and more. Our final model also could have had an income variable, or median household income, to analyze the economic impacts on the death rate. These other variables could be more informative for our LASSO model.
