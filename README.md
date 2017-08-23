
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

Above all, R and SAS are mostly used software and the packages include **SAS: MI, MIANALYZE, GENMOD, NLMIXED; R: jomo, pan, lme4, MICE, geepack.**

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
1. The default is pmm, which means Predictive Mean Matching. We can use 'methods(mice)' command to check what mehtods do it have. For example:
2. PMM (Predictive Mean Matching)  – For numeric variables
3. logreg(Logistic Regression) – For Binary Variables( with 2 levels)
4. polyreg(Bayesian polytomous regression) – For Factor Variables (>= 2 levels)
5. Proportional odds model (ordered, >= 2 levels)
* maxit: Number of iterations taken to impute missing values
 
The usual precess of using mice:
1. First using mice to do multiple imputation to fill in the missing data
2. Analyze each complete dataset separately based on the analysis model.
3. Use command `pool()` to pool all the the results together based on Rubin's rules. (mice package contains function `pool()`)

#### * lme4
lme4 is a package for fitting linear and generalized linear mixed-effects models.For fitting a linear mixed-effects model (LMM) to data, via REML or maximum likelihood, we can usually use the command in lme4, `lmer()` 
```ruby
fit=lmer(formula, data)
```
* Formula:  Random-effects terms are distinguished by vertical bars (|) separating expressions for design matrices from grouping factors

### In SAS
In SAS, when doing the mulitple imputation, there are usually three steps that using different process steps.
* 1. Imputation: proc mi
```ruby
proc mi data=example out=outmi seed=1234; 
var y x1 x2 x3;
run;
```
* 2. Analysis: proc genmod/nlmxied (fix in some models)
* 3. Pooling: proc mianalyze

#### * MI
MI is a multiple imputation procedure in SAS.

Following statements are available for MI procedure:
```ruby
PROC MI < options > ;
  BY variables ;
  CLASS variables ;
  EM < options > ;
  FCS < options > ;
  FREQ variable ;
  MCMC < options > ;
  MNAR options ;
  MONOTONE < options > ;
  TRANSFORM transform (variables< / options >) < . . . transform (variables< / options >) > ;
  VAR variables ;
```
* The EM statement uses the EM algorithm to compute the maximum likelihood estimate (MLE) of the data with missing values, assuming a multivariate normal distribution for the data
* The MCMC statement uses a Markov chain Monte Carlo method to impute values for a data set with an arbitrary missing pattern, assuming a multivariate normal distribution for the data.

The MI procedure also has options as:
* Data details:
  DATA= , OUT= ,
* Imputation Details
  NIMPUTE= specifies number of imputations;
  SEED=specifies seed to begin random number generator
  
  After using MI step, SAS will generate nimp full tables. 
  
#### * MIANALYZE
The MIANALYZE procedure reads parameter estimates and associated standard errors or covariance matrix
that are computed by the standard statistical procedure for each imputed data set. The MIANALYZE
procedure then derives valid univariate inference for these parameters

The following statements are available in the MIANALYZE procedure:
```ruby
PROC MIANALYZE < options > ;
  BY variables ;
  CLASS variables ;
  MODELEFFECTS effects ;
  < label: > TEST equation1 < , . . . , < equationk > > < / options > ;
  STDERR variables ;
 ```
The required MODELEFFECTS statement lists the effects to be analyzed. The variables in the statement that
are not specified in a CLASS statement are assumed to be continuous.

The PROC MIANALYZE and MODELEFFECTS statements are required for the MIANALYZE procedure.
The rest of this section provides detailed syntax information for each of these statements, beginning with the
PROC MIANALYZE statement

#### * GENMOD
The GENMOD procedure fits a generalized linear model to the data by maximum likelihood estimation of the parameter vector
Usually used when GEE analysis .

SAS support gives us a good example:
```ruby
***Generate the data;
data six;
   input case city$ @@;
   do i=1 to 4;
      input age smoke wheeze @@;
      output;
   end;
   datalines;
1 portage   9 0 1  10 0 1  11 0 1  12 0 0
2 kingston  9 1 1  10 2 1  11 2 0  12 2 0
3 kingston  9 0 1  10 0 0  11 1 0  12 1 0
4 portage   9 0 0  10 0 1  11 0 1  12 1 0
5 kingston  9 0 0  10 1 0  11 1 0  12 1 0
6 portage   9 0 0  10 1 0  11 1 0  12 1 0
7 kingston  9 1 0  10 1 0  11 0 0  12 0 0
8 portage   9 1 0  10 1 0  11 1 0  12 2 0
9 portage   9 2 1  10 2 0  11 1 0  12 1 0
10 kingston  9 0 0  10 0 0  11 0 0  12 1 0
11 kingston  9 1 1  10 0 0  11 0 1  12 0 1
12 portage   9 1 0  10 0 0  11 0 0  12 0 0
13 kingston  9 1 0  10 0 1  11 1 1  12 1 1
14 portage   9 1 0  10 2 0  11 1 0  12 2 1
15 kingston  9 1 0  10 1 0  11 1 0  12 2 1
16 portage   9 1 1  10 1 1  11 2 0  12 1 0
;
run;
****Analyze the data by genmod;
proc genmod data=six ;
   class case city ;
   model  wheeze = city age smoke  /  dist=bin;
   repeated  subject=case / type=exch covb corrw;
run;
```

* CLASS statement: point out the ordinary variables
* MODEL statement: refers the fited logistice model. Here it is a logistic regression model with response variable wheeze and independent variables city, age and smoke.
* REPEATED statement: invokes the GEE method, specifies the correlation structure, and controls the displayed output from the GEE model. 
* subject = : must in the coass statement. The option SUBJECT=CASE specifies that individual subjects be identified in the input data set by the variable case. 
* The esitmates and GEE Model Information and Covariance Matrix will be in the output.
* corrw: This asks to see the working correlation matrix.

In Ma's paper and Hossain's paper, we need to estimate **log-odds** of parameters.

However, unlike PROC LOGISTIC, PROC GENMOD does not provide odds ratio estimates for logistic models by default. When fitting a model in PROC GENMOD, odds ratios are only possible when the response is binary or multinomial (DIST=BIN or DIST=MULT) and the link involves a logit function (LINK=LOGIT or LINK=CUMLOGIT).

* `EXP option` can be used in an appropriate ESTIMATE statement to obtain an odds ratio estimate and confidence interval. 

For example:
```ruby
proc genmod data=six descending;
         class case city;
         model wheeze = city age smoke / dist=bin;
         repeated subject=case / type=exch;
         estimate "log O.R. Age" age 1 / exp;
         estimate "log O.R. Kingston vs Portage" city 1 -1 / exp;
         lsmeans city / ilink exp diff cl;
         lsmestimate city 'Kingston vs Portage' 1 -1 / exp cl;
         run;
```

#### * NLMIXED
The NLMIXED procedure fits nonlinear mixed models. PROC NLMIXED fits nonlinear mixed models by maximizing an approximation to the likelihood integrated over the random effects. 
Usually used when RELR analysis.

**NLMIXED compared to MIXED**
* The proc nlmixed can fit to nonlinear model while proc mixed only works on linear model
* The proc mixed can perform both maximum likelihood and restricted maximum likelihood (REML) estimation, while proc nlmixed can only perform maximum likelihood. 
* The proc mixed need assumption of normally distribution, while proc nlmixed can analyze normal, binomial, poisson and so on. 

An example: 
```ruby
proc nlmixed data=infection;
         parms beta0=-1 beta1=1 s2u=2;
         eta = beta0 + beta1*t + u;
         expeta = exp(eta);
         p = expeta/(1+expeta);
         model x ~ binomial(n,p);
         random u ~ normal(0,s2u) subject=clinic;
         predict eta out=eta;
         estimate ’1/beta1’ 1/beta1;
         run;
```
* PARMS statement defines the parameters and their starting values. (I think this process is confusing) 
* The next three statements define pij 
* MODEL statement defines the conditional distribution of xij to be binomial.
* The RANDOM statement defines u to be the random effect with subjects defined by the clinic variable.
* The PREDICT statement constructs predictions for each observation in the input data set.
* The ESTIMATE statement requests an estimate of the reciprocal of beta1.

Here in Ma's and Hossain's paper, to estimate log odds, we can just add an estimate statement: `estiamte 'log odds' log(beta1)`

## More detailed examples
* R, continuous: Andridge, 2011
* SAS, continuous: Taljaard, 2008


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

## Taljaard, 2008
* Taljaard used SAS and t sample t test.
* The used estimators are type 1 and type 2 error.
* Taljaard only considered response Y, no covariates

We can firstly generation the simulation data:

```ruby
***********generate the full data***;
data type2_example;
k=6; m=30; rou=0.1; sigma=15; mu=75; delta=-0.2*sigma;
std_u=sqrt(rou*sigma**2);
std_e=sqrt(sigma**2-rou*sigma**2);
do i= 1 to k;
   x=1;
   u=rand('normal',0,std_u);
   do j=1 to m;
    e=rand('normal',0,std_e);
	y=mu+u+e+delta;
	ind=rand('uniform');
	output;
	end; 
end;
do i= 1 to k;
   x=0;
   u=rand('normal',0,std_u);
   do j=1 to m;
    e=rand('normal',0,std_e);
	y=mu+u+e;
	ind=rand('uniform');
	output;
	end; 
end;
run;
proc print data=type2_example;run;
```
And then generate missing values in the generated dataset.

We can use the MCAR missingness mechanism as an example: Under MCAR, the missing probablility is 30%.

```ruby
***********generate missing values***;
data missing;
set type2_example;
yy=y;
if ind>0.7 then yy=.;
run;
proc print data=missing;run;
```
#### Analysis of the results
1. We can firstly use complete case analysis to analyze the results. There is no covariates so we just do unajusted CCA.

```ruby
**pull out complete case;
data fulls;
  set missing;
  where yy^=.;
run;
proc print data=fulls;run;
  
** Two sample t test;
proc ttest data=fulls
class x; *the idicator of intervention;
  var yy; 
run;
```
2. The author also used mean imputation. There is a proc step called `proc standard`, which can help do the mean imputation
```ruby
**mean imputaion;
proc standard data=missing out=mean_imp replace; 
run;
proc print data=mean_imp;run;

** Two sample t test;
proc ttest data=mean_imp
class x; *the idicator of intervention;
  var yy; 
run;
```
3. Multiple imputation.

```ruby
** MI;
proc mi data=missing out=mid seed=123;
var yy;
run;

proc print data=mid;run;
*proc print data=missing;run;

proc ttest data=mid;
class x; *the idicator of intervention;
  var yy; 
run;
```
#### Questions
1. The author only mentioned `proc mi` in the multiple imputation. She did not mention how to combine the MI results. I don't know what she did after generation multiple full data sets. Only applied two sample t test on the multiple data sets?


The problem here is that only based on these packages, we may cannot calculate the effects that are in the papers, just like estimate SE, coverage percentage. 
