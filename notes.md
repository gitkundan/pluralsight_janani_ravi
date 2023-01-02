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
-- Inferential Stats to explain what is happening

**Steps in EDA**
1. usecols
2. dtype={'col1':'int','col2':'int'} for columns that are getting force-converted to floats
3. parse_dates=['Date'] list of date columns to convert from object to datetime. Another alternative way : bikesharing_data['dteday']=pd.to_datetime(bikesharing_data['dteday'])
4. df['Date'].dt.year to build additional columns for year, month, etc. for y-axis
5. Check for missing values : 
    (a) data.isnull().sum()
    (b) if there are missing values decide what to do :
        (i) Option A : drop missing values : df=unemployment_data.dropna(axis=0)
        (ii) Optiona B : make them 0 [excel_style] : df2=unemployment_data.fillna(axis=0,value=0)



5. plot : first line plot and then box plot
    crude_oil_data.plot(x='Date',y='U.S. Crude Oil ',figsize=(12,8),color='brown')
    plt.ylabel('Production')
    plt.title('US Crude Oil Production')
6. boxplot for the dependent(y) variable: 
    crude_oil_data.boxplot('U.S. Crude Oil ',figsize=(12,8)) #ommitting the col name will give box for all columns
    plt.ylabel('Production')
    plt.title('US Crude Oil Production')

    to compare two columns crude_oil_data[['Alaska','California']].boxplot(figsize=(12,8))

7. scatter plot to see relationship between two columns:
    plt.figure(figsize=(12,8))
    plt.scatter(bikesharing_data['temp'],
            bikesharing_data['cnt'],color='m')
    plt.title('Bike Sharing Daily')
    plt.xlabel('Temperature')
    plt.ylabel('Count')
    plt.show()

8. #create a grouped dataframe to roll-up the level of analysis and do EDA on the higher grain starting with bar graph
    year_data=crude_oil_data.groupby('Year',as_index=False).sum()
    year_data[['Year','U.S. Crude Oil ']]
    mean_prod_data=crude_oil_data.mean(numeric_only=True)[1:-3]
    mean_prod_data=crude_oil_data.mean(numeric_only=True)[1:-3]
    mean_prod_data.sort_values(ascending=False)

    plt.figure(figsize=(12,8))
    plt.bar(bikesharing_data['workingday'],
            bikesharing_data['registered'],color=['m','c'])
    plt.title('Bike Sharing Daily')
    plt.xlabel('Working Day')
    plt.ylabel('Registered Users')
    plt.show()

9. analyse relationship of part to whole : pie chart (to see contribution) as well as scatter 
    (to see relationship   between child and parent)
    plt.scatter(crude_oil_data['Texas'],crude_oil_data['U.S. Crude Oil '])

**Correlation**
1. pandas method : 
    (i) bikesharing_data['temp'].corr(bikesharing_data['cnt'],method='pearson') 
    (ii) spearman for ranked data (ordinal data ranked e.g. movie ratings) 
    (iii) pearson for continuous variable
    (iv) pandas method does not give the p-value; p-value needs to be be < 5% for 95% CI. So, maybe calculate corr across all columns pandas style and then look at p-value for interested columns
    (v) [Correlation_Matrix] See heatmap of pairwise corr across all columns : bikesharing_data.corr(numeric_only=True)
    (vi) Matplotlib heatmap:
        plt.matshow(bikesharing_data.corr(numeric_only=True),fignum=False,aspect='equal')
        columns=len(bikesharing_data.columns)
        plt.xticks(range(columns),bikesharing_data.columns)
        plt.yticks(range(columns),bikesharing_data.columns)
        plt.colorbar()
        plt.xticks(rotation=90)
        plt.show()
    

2. scipy method : 
    (i) from scipy.stats import pearsonr,spearmanr
    (ii) pearsonr(bikesharing_data['temp'],bikesharing_data['cnt'])
    (iii) spearmanr(bikesharing_data['temp'],bikesharing_data['cnt']) #for ordinal/ranking data (not actual values)
    (iii) gives p-value : p-value indicates that corr is not due to random i.e. it is not mere coincidence. pvalue needs to be small

**Autocorrelation**
How are the values correlated with T-1, T-2 values
Values between +1 and -1


**Vega/Altair**
1. Altair uses vega/vega-lite grammar which is json schema of the data and axes,colors,etc. like qlik
2. 