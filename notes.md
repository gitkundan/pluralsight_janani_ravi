References:
Introduction to Statistics, Jim Frost

**Univariate Analysis**
Things to look at:
--Frequency
--Dispersion : Range (sensitive to outliers), IQR (75% quartile - 25% quartile i.e. captures 50% of data), s.d (sample s.d. will have n-1 Bessel correction)
--Mean/Median (Central Tendency)
--Outlier : how to classify (option a: more than 3s.d. option b : 25%/75% +- 1.5 IQR)

**Bivariate Analysis**
--measure strength of relationship between varaiables : covariance (actual values, not scaled/standardized, positive cov means deviations around mean are in sync i.e. in same direction); correlation (scaled between +-1 , measures linear relationship)

**Multivariate Analysis**
--Cov matrix, corr matrix : heatmap with cov/corr for each set of data

**Inferential Statistics**
-- Hyp testing
-- Model Fitting (ML)

**Steps in EDA**
1. usecols
2. dtype={'col1':'int','col2':'int'} for columns that are getting force-converted to floats
3. parse_dates=['Date'] list of date columns to convert from object to datetime. Another alternative way : bikesharing_data['dteday']=pd.to_datetime(bikesharing_data['dteday'])
4. df['Date'].dt.year to build additional columns for year, month, etc. for y-axis
5. plot : first line plot and then box plot
    crude_oil_data.plot(x='Date',y='U.S. Crude Oil ',figsize=(12,8),color='brown')
    plt.ylabel('Production')
    plt.title('US Crude Oil Production')
6. boxplot for the dependent(y) variable: 
    crude_oil_data.boxplot('U.S. Crude Oil ',figsize=(12,8)) #ommitting the col name will give box for all columns
    plt.ylabel('Production')
    plt.title('US Crude Oil Production')

    to compare two columns crude_oil_data[['Alaska','California']].boxplot(figsize=(12,8))
7. #create a grouped dataframe to roll-up the level of analysis and do EDA on the higher grain starting with bar graph
    year_data=crude_oil_data.groupby('Year',as_index=False).sum()
    year_data[['Year','U.S. Crude Oil ']]
    mean_prod_data=crude_oil_data.mean(numeric_only=True)[1:-3]
    mean_prod_data=crude_oil_data.mean(numeric_only=True)[1:-3]
    mean_prod_data.sort_values(ascending=False)
8. analyse relationship of part to whole : pie chart (to see contribution) as well as scatter 
    (to see relationship   between child and parent)
    plt.scatter(crude_oil_data['Texas'],crude_oil_data['U.S. Crude Oil '])

**Correlation**
