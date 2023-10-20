# ECON615_IV
For this problem set, you will need to download census micro data for the 1971, 1981, 1991, 2001 and
2011 Canadian Census from IPUMS (https://international.ipums.org/international/). Select (at least) the
following variables:
• age, sex, educca, bplca1, inctot
You will also need to use the compulsory schooling law file posted on D2L

# Handling potential NaN values by dropping them for the 2SLS regression
analysis_df = merged_df.dropna(subset=['AGE', 'SEX', 'YEAR', 'BPLCA1', 'year_at_14', 'dropoutage', 'EDUCCA', 'INCTOT'])

# First Stage: Regress grade attainment on dropout age and control variables
endog = analysis_df['EDUCCA']
exog = sm.add_constant(analysis_df[['dropoutage', 'AGE', 'age^2', 'age^3', 'age^4', 'gender_2']])
instrument = analysis_df['dropoutage']

# Fit the first stage regression model
first_stage_model = IV2SLS(endog, exog, instrument=instrument).fit()

# Display the first stage regression results
first_stage_model.summary()
