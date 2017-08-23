
### Continuous

| Author | Methods | Software |
| --- | --- | --- |
| Taljaard, 2008 | Within cluster MI (ABB) | SAS: PROC MI |
| | Pooled MI (ABB) | SAS: PROC MI |
| | Standrad regression MI | SAS: PROC MI |
| | Mixed-effects regression MI	|	R: pan |
| Andridge, 2010 | Ignoring clusters | R: MICE |
|	|	Fixed cluster effects	|	R: MICE |
|	|	Random cluster effects	|	R: pan |
|Hossain, 2016 |	Cluster level analysis (Unadjusted)	| |
| |Cluster level analysis (Adjusted)	| |
|	|	LMM	 |	R: lme4 |
|	|	MI 	|	R: jomo |

### Binary

| Author | Missing Handling Methods | Analysis Methods | Software |
| --- | --- | --- | --- |
| Ma, 2011 | Complete case analysis |	GEE/RE |	SAS: GENMOD/NLMXED |
| |	Within cluster Logistic regression |	GEE/RE |	SAS: |
MI
MIANALYZE
GENMOD
NLMIXED"
		Propensity score	GEE/RE	
		MCMC	GEE/RE	
	Across cluster 	Propensity score	GEE/RE	
		Random effect logistic regression	GEE/RE	
		Fixed effect logistic rgerssion	GEE/RE	
	"Ignore cluster MI
Standard MI "	Logistic regression	GEE/RE	
		Propensity score	GEE/RE	
		MCMC	GEE/RE	


Ma, 2012	Complete case analysis 			SAS: GENMOD
	Standard MI  		Logistic regression	"SAS: 
MI
MIANALYZE
GENMOD
NLMIXED"
			MCMC	
	Within cluster MI		Logistic regression	
			MCMC	
	Fixed effect MI		Logistic regression	
	Complete case analysis 		GEE	SAS: GENMOD
Ma, 2013			RELR	SAS: NLMIXED
	Standard MI		GEE/RE	SAS: MI, MIANALYZE, GENMOD, NLMIXED
	Within cluster MI		GEE/RE	




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


