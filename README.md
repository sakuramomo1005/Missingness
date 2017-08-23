
\begin{table}[]
\centering
\caption{My caption}
\label{my-label}
\begin{tabular}{lllll}
\cline{1-3}
\multicolumn{1}{|c|}{Data type}                                                                                           & \multicolumn{1}{c|}{Author}                                                              & \multicolumn{1}{c|}{Imputation methods}                                                           & Analysis model & Software                                                                                          \\ \cline{1-3}
\multicolumn{1}{|c|}{Continuous}                                                                                          & \multicolumn{1}{c|}{\begin{tabular}[c]{@{}c@{}}Taljaard,\\   2008\end{tabular}}          & \multicolumn{1}{c|}{No imputation}                                                                &                &                                                                                                   \\ \cline{1-3}
\multicolumn{1}{|c|}{\begin{tabular}[c]{@{}c@{}}Cluster\\   mean imputation\end{tabular}}                                 & \multicolumn{1}{c|}{}                                                                    & \multicolumn{1}{c|}{}                                                                             &                &                                                                                                   \\ \cline{1-3}
\begin{tabular}[c]{@{}l@{}}Within\\   cluster MI (ABB)\end{tabular}                                                       &                                                                                          & SAS: PROC MI                                                                                      &                &                                                                                                   \\
\begin{tabular}[c]{@{}l@{}}Pooled\\   MI (ABB)\end{tabular}                                                               &                                                                                          & SAS: PROC MI                                                                                      &                &                                                                                                   \\
\begin{tabular}[c]{@{}l@{}}Standrad\\   regression MI\end{tabular}                                                        &                                                                                          & SAS: PROC MI                                                                                      &                &                                                                                                   \\
\begin{tabular}[c]{@{}l@{}}Mixed-effects\\   regression MI\end{tabular}                                                   &                                                                                          & R: pan                                                                                            &                &                                                                                                   \\
Andridge, 2010                                                                                                            & Ignoring clusters                                                                        &                                                                                                   & R: MICE        &                                                                                                   \\
\begin{tabular}[c]{@{}l@{}}Fixed\\   cluster effects\end{tabular}                                                         &                                                                                          & R: MICE                                                                                           &                &                                                                                                   \\
\begin{tabular}[c]{@{}l@{}}Random\\   cluster effects\end{tabular}                                                        &                                                                                          & R: pan                                                                                            &                &                                                                                                   \\
Hossain, 2016                                                                                                             & \begin{tabular}[c]{@{}l@{}}Cluster level analysis\\   (Unadjusted)\end{tabular}          &                                                                                                   &                &                                                                                                   \\
\begin{tabular}[c]{@{}l@{}}Cluster\\   level analysis (Adjusted)\end{tabular}                                             &                                                                                          &                                                                                                   &                &                                                                                                   \\
LMM                                                                                                                       &                                                                                          & R: lme4                                                                                           &                &                                                                                                   \\
MI                                                                                                                        &                                                                                          & R: jomo                                                                                           &                &                                                                                                   \\
                                                                                                                          & Ma, 2011                                                                                 & \begin{tabular}[c]{@{}l@{}}Complete case\\   analysis\end{tabular}                                & GEE/RE         & SAS: GENMOD/NLMXED                                                                                \\
Binary                                                                                                                    & Within cluster                                                                           & Logistic regression                                                                               & GEE/RE         & \begin{tabular}[c]{@{}l@{}}SAS: \\     MI\\     MIANALYZE\\     GENMOD\\     NLMIXED\end{tabular} \\
\begin{tabular}[c]{@{}l@{}}Propensity\\   score\end{tabular}                                                              & GEE/RE                                                                                   &                                                                                                   &                &                                                                                                   \\
MCMC                                                                                                                      & GEE/RE                                                                                   &                                                                                                   &                &                                                                                                   \\
\begin{tabular}[c]{@{}l@{}}Across\\   cluster\end{tabular}                                                                & Propensity score                                                                         & GEE/RE                                                                                            &                &                                                                                                   \\
\begin{tabular}[c]{@{}l@{}}Random\\   effect logistic regression\end{tabular}                                             & GEE/RE                                                                                   &                                                                                                   &                &                                                                                                   \\
\begin{tabular}[c]{@{}l@{}}Fixed\\   effect logistic rgerssion\end{tabular}                                               & GEE/RE                                                                                   &                                                                                                   &                &                                                                                                   \\
\begin{tabular}[c]{@{}l@{}}Ignore\\   cluster MI\\     Standard MI\end{tabular}                                           & Logistic regression                                                                      & GEE/RE                                                                                            &                &                                                                                                   \\
\begin{tabular}[c]{@{}l@{}}Propensity\\   score\end{tabular}                                                              & GEE/RE                                                                                   &                                                                                                   &                &                                                                                                   \\
MCMC                                                                                                                      & GEE/RE                                                                                   &                                                                                                   &                &                                                                                                   \\
Ma, 2012                                                                                                                  & \begin{tabular}[c]{@{}l@{}}Complete case\\   analysis\end{tabular}                       &                                                                                                   & SAS: GENMOD    &                                                                                                   \\
Standard MI                                                                                                               & Logistic regression                                                                      & \begin{tabular}[c]{@{}l@{}}SAS: \\     MI\\     MIANALYZE\\     GENMOD\\     NLMIXED\end{tabular} &                &                                                                                                   \\
MCMC                                                                                                                      &                                                                                          &                                                                                                   &                &                                                                                                   \\
Within cluster MI                                                                                                         & Logistic regression                                                                      &                                                                                                   &                &                                                                                                   \\
MCMC                                                                                                                      &                                                                                          &                                                                                                   &                &                                                                                                   \\
\begin{tabular}[c]{@{}l@{}}Fixed\\   effect MI\end{tabular}                                                               & Logistic regression                                                                      &                                                                                                   &                &                                                                                                   \\
                                                                                                                          & \begin{tabular}[c]{@{}l@{}}Complete\\   case analysis\end{tabular}                       & GEE                                                                                               & SAS: GENMOD    &                                                                                                   \\
\begin{tabular}[c]{@{}l@{}}Ma,\\   2013\end{tabular}                                                                      & RELR                                                                                     & SAS: NLMIXED                                                                                      &                &                                                                                                   \\ \cline{1-1}
\multicolumn{1}{|l|}{\begin{tabular}[c]{@{}l@{}}Standard\\   MI\end{tabular}}                                             & GEE/RE                                                                                   & \begin{tabular}[c]{@{}l@{}}SAS: MI, MIANALYZE,\\   GENMOD, NLMIXED\end{tabular}                   &                &                                                                                                   \\ \cline{1-1}
\begin{tabular}[c]{@{}l@{}}Within\\   cluster MI\end{tabular}                                                             & GEE/RE                                                                                   &                                                                                                   &                &                                                                                                   \\
Caille, 2014                                                                                                              & \begin{tabular}[c]{@{}l@{}}Complete case analysis\\   (Unadjusted)\end{tabular}          &                                                                                                   &                &                                                                                                   \\
\begin{tabular}[c]{@{}l@{}}Complete\\   case analysis (Adjusted)\end{tabular}                                             &                                                                                          &                                                                                                   &                &                                                                                                   \\
\begin{tabular}[c]{@{}l@{}}Bernoulli\\   single draw with paramether (Own group success rate)\end{tabular}                &                                                                                          &                                                                                                   &                &                                                                                                   \\
\begin{tabular}[c]{@{}l@{}}Bernoulli\\   single draw with paramether (other group success rate)\end{tabular}              &                                                                                          &                                                                                                   &                &                                                                                                   \\
\begin{tabular}[c]{@{}l@{}}MI\\   with logistic regression\end{tabular}                                                   &                                                                                          &                                                                                                   &                &                                                                                                   \\
\begin{tabular}[c]{@{}l@{}}MI\\   with Random effect logistic regression\end{tabular}                                     &                                                                                          &                                                                                                   &                &                                                                                                   \\
\begin{tabular}[c]{@{}l@{}}MI\\   with linear mixed effect regression model approach and simple rounding\end{tabular}     &                                                                                          &                                                                                                   &                &                                                                                                   \\
\begin{tabular}[c]{@{}l@{}}MI\\   with linear mixed effect regression model approach and adaptative rounding\end{tabular} &                                                                                          &                                                                                                   &                &                                                                                                   \\
\begin{tabular}[c]{@{}l@{}}MI\\   with approximate Bayesian Bootrasp\end{tabular}                                         &                                                                                          &                                                                                                   &                &                                                                                                   \\
Hossain, 2016                                                                                                             & \begin{tabular}[c]{@{}l@{}}Complete\\   case analysis\end{tabular}                       & \begin{tabular}[c]{@{}l@{}}Cluster level analysis\\   (Unadjusted/Adjusted)\end{tabular}          &                &                                                                                                   \\
\begin{tabular}[c]{@{}l@{}}Individual\\   level: GEE/RE\end{tabular}                                                      &                                                                                          &                                                                                                   &                &                                                                                                   \\
MMI                                                                                                                       & \begin{tabular}[c]{@{}l@{}}Cluster level analysis\\   (Unadjusted/Adjusted)\end{tabular} &                                                                                                   &                &                                                                                                   \\
\begin{tabular}[c]{@{}l@{}}Individual\\   level: GEE/RE\end{tabular}                                                      &                                                                                          &                                                                                                   &                &                                                                                                  
\end{tabular}
\end{table}

# Missingness methods

This session is about what softwares did the authors use and how they work


## Andridge, 2011
### Basic information
* Missing mechanism: MCAR, MAR
* Software: R
* Packages: mice, pan

The author analyzed missingness by applying imputations, includes fixed cluster effect MI, ingoring clusters MI, random cluster effects MI (MMI).

#### Data generation:
```ruby
##data generation
k=20;m=50;tau=0.5;rou=0.01;sigma=10
b=c()
x=matrix(NA,k,m)
y=matrix(NA,k,m)
e=matrix(NA,k,m)
for(j in 1:k){
  b[j]=rnorm(1,0,(sqrt(rou)*sigma))
  for(i in 1: m){
    x[j,i]=rnorm(1,0,1)
    e[j,i]=rnorm(1,0,sqrt((1-tau^2-rou)*sigma^2))
    y[j,i]=10+tau*sigma*x[j,i]+b[j]+e[j,i]
  }
}
##generate expit function
expit=function(x){
  y=exp(x)/(exp(x)+1)
  return(y)
}
```

#### Missingness generation:
```ruby
##MCAR
a0=0.5
pi_mcar=expit(a0) ## non missing proportion, the result is 0.622 
##MAR
a1=1
pi_mar=expit(a0+a1*x)
#if int=1 then missing
int=ifelse(pi_mar>0.5,0,1) # missing idicator
#missing results
yy=ifelse(int==1,NA,y)
```
#### Imputation methods
* The mice package is used for the fixed effects of cluster imputation adn imputation ignoring clusters
* The pan package is used for the mixed effects imputation. 

##### How the mice package work:

* m  – Refers to 5 imputed data sets
* maxit – Refers to no. of iterations taken to impute missing values
* method – Refers to method used in imputation. we used predictive mean matching. We can use methods(mice) to check the possible mehtods

```ruby
#missing
yy=ifelse(int==1,NA,y)

install.packages('mice')
library('mice')

##imputation ignore cluster 
data1=data.frame(y=c(yy),x=c(x))
data1_imp=mice(data1,m=10,maxit=10,mehtod='pmm')

##check imputed values
data1_imp$imp$y

##get complete data ( 2nd out of 10)
completeData = complete(data1_imp,2)

#build predictive model
fit <- with(data = data1_imp, exp = lm(y~x)) 

#combine results of all 5 models
combine <- pool(fit)
summary(combine)
```

It is weird that the pan package cannot work in my computer. I can install it successfully, but when I run it, it shuts down my R Studio.  


