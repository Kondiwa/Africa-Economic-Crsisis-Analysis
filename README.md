# Africa-Economic-Crsisis-Analysis

Data Description
The data that was used for analysis was about the economic crisis for the African countries. The dataset contained a total of 2604 rows or entries and 15 columns. Therefore, the dimension of the data was 2604 by 15. The number of rows represented the number of observations. On the other hand, the number of columns represented the number of variables. The data contained 12 unique countries from Africa. The countries included: Central African Republic, Cote’ D Ivoire, Egypt, Ghana, Kenya, Mauritius, Morocco, Nigeria, South Africa, Tunisia, Zambia and                    Zimbabwe.
The 15 variables were a mixture of both numerical variables and categorical variables. The variables that were contained in the dataset were: Year, country, banking crisis, systemic crisis, gold standard, exchange in USD, exchange in alt1, exchange in USD alt2, exchange in USD lt3, domestic debt in default, GDP weighted default, annual inflation, independence, currency crises and inflation crises.  The categorical variables were numerically coded to facilitate easy statistical analyses. The present of a factor (i.e whether the country experienced banking crisis) was coded as 1. On the other, the absence of a factor was coded as 0. 

Data preparation
Data preparation involves getting the right data and in the right format for analysis. The study was based on the economic crisis of African countries.  The data that was used for analysis contained information about the global economic crisis. Therefore, the initial stage of data handling was filtering the variables corresponding to African countries from the whole dataset containing global crisis economic data. The data filtering was meant to eliminate the data that is not of interest hence leaving the most appropriate data. Using R, the data corresponding to African countries was obtained as follows:

global_crisis<-read.csv('D://globalcrisis.csv')
africa_crisis<-lobal_crisis[grep("Central|AfricanRepublic|CoteDIvoire|Egypt|Ghana|Kenya|Mauritius|Morocco|Nigeria|South Africa|Tunisia|Zambia|Zimbabwe", global_crisis$Country), ]

Data Transformation
Data transformation or data wrangling was done to have the sample data in the right format. The first data transformation that was conducted was the elimination of unnecessary variables. Some of the variables that were eliminated were repeated. There was a total of fifteen (15) variables that were selected for analysis. The sample dataset (data frame) was stored as africa_crisis1. The following R code was used to a sample using the 15 variables:
africa_crisis1<-data.frame(africa_crisis$Year,africa_crisis$Country,
                           africa_crisis$Banking.Crisis,africa_crisis$Systemic.Crisis,
                           africa_crisis$Gold.Standard,africa_crisis$exch_usd,
                           africa_crisis$exch_usd_alt1,africa_crisis$exch_usd_alt2,
                           africa_crisis$exch_usd_alt3,africa_crisis$Domestic_Debt_In_Default,
                           africa_crisis$GDP_Weighted_default,africa_crisis$Inflation..Annual.percentages.of.average.consumer.prices,
                           africa_crisis$Independence,africa_crisis$Currency.Crises,
                           africa_crisis$Inflation.Crises)

Data cleaning
Data cleaning or data cleansing is the process of identifying and removing unnecessary information from the data as well as adding the missing and necessary information. Data cleaning was done to check for duplicates as well as the possibility of repeated values corresponding to variables of interest. The first data cleaning activity was checking the cases of missing values. Using R, the following code was used to find out whether there were some cases of missing values in the data:
sum(is.na(africa_crisis1))
## [1] 0
The result of the check demonstrates that there were no cases (0) of missing values. Therefore, the dataset was suitable for conducting statistical analyses and making inferences about the population.
Data analysis
Having obtained a suitable sample from the dataset of the global economic crisis, several data analyses were conducted. The initial analysis was the summary statistics of the variables. 
summary(africa_crisis1)
##      Country     			Banking Crisis
##  Central African Republic: 217   0  :2477      
##  CoteD Ivoire            : 217   1  : 102      
##  Egypt                   : 217         
##  Ghana                   : 217                 
##  Kenya                   : 217                 
##  Mauritius               : 217                 
##  Systemic Crisis Gold Standard   Exchange in USD    Exchange in alt1
##  0  :2503        0  : 798                :1093              :2309   
##  1  :  89        1  : 286      n/a       : 193   0.000714286:  21   
##  n/a:  12        n/a:1520      0         : 113   0.714285999:  21   
##                                7.1429    :  21   0.4957     :   6   
##                                0.20661157:  19   174.9998762:   6   
##                                7.14E-27  :  15   0.4958     :   3   
in USD alt2  Exchange in usd lt3 Domestic Debt In Default
##         :2573                    :2602     0  :2556                
##  278    :   2         n/a        :   2     1  :  35                
##  n/a    :   2         0.000000027:   0     n/a:  13                
##  205    :   1         0.000000091:   0                             
##  220    :   1         0.000000107:   0                             
##  221    :   1         0.000000116:   0                             
##  GDP Weighteddefault Annual Inflation  Independence    Currency Crises  
##  0      :2355               :1606     Min.   :0.0000   Min.   :0.00000  
##  n/a    : 219        0      :  15     1st Qu.:0.0000   1st Qu.:0.00000  
##  0.06   :  11        2.7    :  12     Median :0.0000   Median :0.00000  
##  0.13   :   8        2.8    :  12     Mean   :0.3299   Mean   :0.05568  
##  0.4    :   6        1.9    :  11     3rd Qu.:1.0000   3rd Qu.:0.00000  
##  0.36   :   5        2.5    :  11     Max.   :1.0000   Max.   :2.00000  
##  (Other):   0        (Other): 937                                       
##  Inflation Crises
##     :   1        
##  0  :2481        
##  1  : 122        

Data visualization
	Data visualization is a way of representing data in figures in order to reveal the patterns and trends in the variables. The following visualization was conducted:
Visualization 1: A box plot of Inflation Crisis by Country
	A ggplot package in R was used to produce a boxblot of inflation crisis for all the countries in Africa. The purpose of the boxplot was to identify the patterns displayed byu the data as well as to investigate whether the data has some outliers. The R code that was used to obtain the plot was: 
		qplot(africa_crisis1$Year,africa_crisis1$`Inflation Crises`,
     		 data=africa_crisis1, geom=c("boxplot", "jitter"),
    	 	 fill=Country, main="Inflation Crisis by Country",
   	 	  xlab="", ylab="Inflation Crisis")

The resulting ggplot was as shown in the figure below:
 

Based on the results, we can see that there was one observation below zero for Zambia that could be considered as an outlier. The value is an outlier because it is considerably small. Similarly, there is some observation above 1 that can be considered as outliers (values falling under the Central African Republic). The values can be considered as outliers because they are considerably large. 

Visualization 2: A box plot of Annual Inflation rates by Country
The other visualization was a box plot of the annual inflation index for the countries. The R code that was used to obtain the plot is as follows:
qplot(africa_crisis1$Country,africa_crisis1$`Annual Inflation`,
     	 data=africa_crisis1, geom=c("boxplot", "jitter"),
     	 fill=Country, main="Inflation Crisis by Country",
    	  xlab="", ylab="Inflation Crisis")
The resulting ggplot was as follows:
 
Predictive models: Multiple Linear Regression Model
The regression model was used to showcase the nature of the associations between yearly inflation rates and the indicators of improved financial performance and overall economic development. The model predicts the expected annual rate of inflation based on system crisis, banking crisis, exchange in USD, inflation crisis and currency crisis. 

inflationcrisis+currencycrisis,data = regression_data)
reg.model
## lm(formula = inflation ~ systemcrisis + bankingcrisis + exchnageusd + 
##     inflationcrisis + currencycrisis, data = regression_data)
## Coefficients:
##     (Intercept)     systemcrisis    bankingcrisis      exchnageusd  
##       -20.38956        278.94517         26.56547          0.05825  
## inflationcrisis   currencycrisis  
##       179.72017        -22.16542

Predictive model review 
	summary(reg.model)
## lm(formula = inflation ~ systemcrisis + bankingcrisis + exchnageusd + 
##     inflationcrisis + currencycrisis, data = regression_data)
## Residuals:
##     Min      1Q  Median      3Q     Max 
## -548.76 -116.52   21.58   29.81 2614.65  
## Coefficients:
##                  Estimate Std. Error t value Pr(>|t|)    
## (Intercept)     -20.38956   28.27974  -0.721 0.471550    
## systemcrisis    278.94517  126.86984   2.199 0.028769 *  
## bankingcrisis    26.56547  121.49773   0.219 0.827092    
## exchnageusd       0.05825    0.01686   3.455 0.000641 ***
## inflationcrisis 179.72017   45.41532   3.957 9.75e-05 ***
## currencycrisis  -22.16542   43.01268  -0.515 0.606759    
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## Residual standard error: 328.2 on 264 degrees of freedom
## Multiple R-squared:  0.1888, Adjusted R-squared:  0.1734 
## F-statistic: 12.29 on 5 and 264 DF,  p-value: 1.006e-10

Based on the model summary, the R-squared value is 0.1888 (18.88%). The R squared value implies that the model explains 18.88% of the entire population. Even the value is low, we can see that the model makes some predictions hence it can be used for making inferences about the population. The value of the intercept is -20.38956, which represents the overall effect of the independent variables on the dependent variable. Therefore, a value of -20.38956 implies that an overall change independent variable (increase/decrease) by 1 unit will cause a corresponding change in the dependent variable by -20.38956 units.
The normality of the residuals was examined using a histogram. From the histogram below, we can see that the residuals do not follow a normal distribution. 
#checking for the normality of the residuals
hist(reg.model$fitted.values,reg.model$residuals,ylim = c(0,0.005))
 

