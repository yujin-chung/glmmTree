# glmmTree
Predictive modeling of microbiome data using a phylogenetic tree-regularized generalized linear mixed model

# dependent R packages
install.packages('rrBLUP')
install.packages('Matrix')
nlme: https://cran.r-project.org/src/contrib/Archive/nlme/nlme_3.1-122.tar.gz
R CMD INSTALL nlme_3.1-122.tar.gz

# data in example
data1.rda
-
-
-
-
data2.rda



# example for continous outcome
library(rrBLUP)
library(Matrix)
source('lib.R')
source('glmmTreeg.R')

load('data1.rda')
lambda1=c(0.1,0.5)
lambda2=c(0.1,10)
obj.cv=cv.glmmTreeg(y=y.tr,Z=z.tr,X=NULL,D,lambda1=lambda1,lambda2=lambda2)
yhat=predict.cv.glmmTreeg(obj.cv,X=NULL,z.te)
plot(yhat,y.te,main='Continuous outcome')


# example for binary outcome
library(Matrix)
source('lib.R')
source('glmmTreeb.R')
load("data2.rda")
obj.cv=cv.glmmTreeb(y=y.tr,Z=z.tr,X=NULL,D,lambda1=c(1,2),lambda2=c(1,2))
yhat=predict.cv.glmmTreeb(obj.cv,X=NULL,z.te)
boxplot(yhat ~ y.te, main='Binary outcome')




