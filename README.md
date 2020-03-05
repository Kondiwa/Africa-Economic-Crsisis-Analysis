# Africa-Economic-Crsisis-Analysis

#importing the data into R
global_crisis<-read.csv('D://globalcrisis.csv')

#filtering the variables corresponding to African countries from the whole dataset containing global crisis economic data
africa_crisis<- global_crisis[grep("Central African Republic|CoteD Ivoire|Egypt|Ghana|Kenya|Mauritius|Morocco|Nigeria|South Africa|Tunisia|Zambia|Zimbabwe", global_crisis$Country), ]


##Data preparation/wrangling
#Eliminating some variables and only remaining with the relevant variables
#The following 15 variables were selected for further analysis
#This process also removes duplicate variables
africa_crisis1<-data.frame(africa_crisis$Year,africa_crisis$Country,
                           africa_crisis$Banking.Crisis,africa_crisis$Systemic.Crisis,
                           africa_crisis$Gold.Standard,africa_crisis$exch_usd,
                           africa_crisis$exch_usd_alt1,africa_crisis$exch_usd_alt2,
                           africa_crisis$exch_usd_alt3,africa_crisis$Domestic_Debt_In_Default,
                           africa_crisis$GDP_Weighted_default,africa_crisis$Inflation..Annual.percentages.of.average.consumer.prices,
                           africa_crisis$Independence,africa_crisis$Currency.Crises,
                           africa_crisis$Inflation.Crises)
#For easy interpretation, the above variables are renamed as follows.
names(africa_crisis1)[1:15] <-c("Year","Country","Banking Crisis",
                                "Systemic Crisis","Gold Standard",
                                "Exchange in USD","Exchange in alt1",
                                "Exchange in USD alt2","Exchange in usd lt3",
                                "Domestic Debt In Default","GDP Weighteddefault",
                                "Annual Inflation","Independence", "Currency Crises", 
                                "Inflation Crises")

colnames(africa_crisis1)
#Data cleaning
#checking and removing missing values from the data set
sum(is.na(africa_crisis1))
#The sum indicates that there are 0 missing cases. 
#Therefore, the dataset is perfect for conducting statistical analyses
africa_crisis1
#summary statistics
summary(africa_crisis1)
#Checking for outliers using ggplots
library(ggplot2)
#A box plot of Inflation Crisis by Countr
# observations (points) are overlayed and jittered
qplot(africa_crisis1$Year,africa_crisis1$`Inflation Crises`,
      data=africa_crisis1, geom=c("boxplot", "jitter"),
      fill=Country, main="Inflation Crisis by Country",
      xlab="", ylab="Inflation Crisis")
#A box plot of Annual Inflation rates by Countr

qplot(africa_crisis1$Country,africa_crisis1$`Annual Inflation`,
      data=africa_crisis1, geom=c("boxplot", "jitter"),
      fill=Country, main="Inflation Crisis by Country",
      xlab="", ylab="Inflation Crisis")

#data analysis
#
africa.data<-read.csv('D://africa.csv')
inflation<-africa.data$Inflation..Annual.percentages.of.average.consumer.prices
systemcrisis<-africa.data$Systemic.Crisis
bankingcrisis<-africa.data$Banking.Crisis
exchnageusd<-africa.data$exch_usd
inflationcrisis<-africa.data$Inflation.Crises
currencycrisis<-africa.data$Currency.Crises
regression_data<-data.frame(inflation,systemcrisis,bankingcrisis,
                            exchnageusd,inflationcrisis,currencycrisis)

#Data analysis
#testing for linear correlations
library(psych)
corr.test(regression_data,method = 'pearson')

#Regression ananlysis
reg.model<-lm(inflation~systemcrisis+bankingcrisis+exchnageusd+inflationcrisis+currencycrisis,data = regression_data)
reg.model
summary(reg.model)
#checking for the normality of the residuals
hist(reg.model$fitted.values,reg.model$residuals,ylim = c(0,0.005))
