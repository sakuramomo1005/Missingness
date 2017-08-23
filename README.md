
# Missing Data Programming Methods

This is a summary about the softwares and pacakges that were used in the 9 papers that handling missing data. The summary contains:
* A summary table of the 9 papers' programming methods
* A summary of how to use these packages
* Some detailed examples

## Summary Tabel
The following is the table that compare the softwares and packages that were used in those 9 papers.
### Continuous Outcomes

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

### Binary Outcomes

| Author | Missing Handling Methods | Analysis Methods | Software |
| --- | --- | --- | --- |
| Ma, 2011 | Complete case analysis | GEE/RE |	SAS: GENMOD/NLMXED |
| | Within cluster MI | GEE/RE | SAS: MI, MIANALYZE, GENMOD, NLMIXED" |
| | Across cluster MI | GEE/RE | SAS: MI, MIANALYZE, GENMOD, NLMIXED" |
| | Standard MI | GEE/RE | SAS: MI, MIANALYZE, GENMOD, NLMIXED" |
| Ma, 2012 |	Complete case analysis 	| | SAS: GENMOD | 
| | Standard MI  | Logistic regression | SAS: MI, MIANALYZE, GENMOD, NLMIXED" |
| | Within cluster MI | Logistic regression | SAS: MI, MIANALYZE, GENMOD, NLMIXED" |
| | Fixed effect MI | Logistic regression | SAS: MI, MIANALYZE, GENMOD, NLMIXED" |
| Ma, 2013 | Complete case analysis |GEE |SAS: GENMOD |
| | | RELR | SAS: NLMIXED |
| | Standard MI	| GEE/RE |SAS: MI, MIANALYZE, GENMOD, NLMIXED |
| | Within cluster MI | GEE/RE| SAS: MI, MIANALYZE, GENMOD, NLMIXED |
| Caille, 2014 | MI | Linear mixed effects regression model | R: pan |
| | MI | RELR, ABB | SAS: GENMOD MI |
| Hossain, 2016| MMI | GEE | R: jomo, geepack |
| | MMI | RELR | R: jomo, lme4 |

Above all, R and SAS are mostly used software and the packages include SAS: MI, MIANALYZE, GENMOD, NLMIXED; R: jomo, pan, lme4, MICE, geepack.

## How to use these packages?

### In R
#### * jomo
jomo is a package for multilevel multiple imputation. Novel aspects of 'jomo' are the possibility of handling binary and categorical data through latent normal variables.
 ```ruby
 imp=jomo(Y,clus=clus,nburn=nburn,nbetween=nbetween,nimp=nimp, meth="fixed")
 # or 
 imp=jomo(Y,clus=clus,nburn=nburn,nbetween=nbetween,nimp=nimp, meth="random")
 ```
* clus: A data frame, or matrix, containing the cluster indicator for each observation
* nburn: Number of burn in iterations. Default is 1000.
* nbetween: Number of iterations between two successive imputations. Default is 1000.
* nimp: Number of Imputations. Default is 5.
* Attention: If Y is binary data, then Y must be factors

If we have a data frame, dim=(m,n). After doing jomo, the dim will be (m*(nimp+1),n). We can do analysis based on each m * n data frame and then pool them together. jomo package does not have a pooling function. 

#### * pan
It is weird that the pan package cannot work in my computer. I can install it successfully, but when I run it, it shuts down my R Studio.
#### * mice
mice is also a multiple imputation mehtods function. mice assumes that the missing data are Missing at Random (MAR)
```ruby
imp=mice(data,m=5,maxit=50,meth='pmm',seed=500)
```
* m=5: Number of imputed datasets. Five is the default value.
* meth='pmm': The imputation method.
...The default is pmm, which means Predictive Mean Matching. We can use 'methods(mice)' command to check what mehtods do it have. For example:
⋅⋅⋅1. PMM (Predictive Mean Matching)  – For numeric variables
⋅⋅⋅2. logreg(Logistic Regression) – For Binary Variables( with 2 levels)
⋅⋅⋅3. polyreg(Bayesian polytomous regression) – For Factor Variables (>= 2 levels)
⋅⋅⋅4. Proportional odds model (ordered, >= 2 levels)
* maxit: Number of iterations taken to impute missing values
 
The usual precess of using mice:
1. First using mice to do multiple imputation to fill in the missing data
2. Analyze each complete dataset separately based on the analysis model.
3. Use command `pool()` to pool all the the results together based on Rubin's rules. (mice package contains function `pool()`)

#### * lme4

### SAS
#### * MI

#### * MIANALYZE

#### * GENMOD
GEE
#### * NLMIXED
RELR

## More detailed examples
* R, continuous: Andridge, 2011
* SAS, continuous: Taljaard, 2008
* R, binary: Hossain, 2016
* SAS, binary: Ma, 2012


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
* method – Refers to method used in imputation. We used predictive mean matching. We can use 'methods(mice)' to check the possible mehtods

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


