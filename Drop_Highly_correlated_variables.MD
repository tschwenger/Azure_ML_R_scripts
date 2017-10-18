# This is an R script to run for dropping highly correlated variables. 

** This is to get rid of columns that essentially fit themselves that make the selected algorithm for ML less predictive 

```{r,message=FALSE,warning=FALSE}
## R script below

# Map 1-based optional input ports to variables
d <- maml.mapInputPort(1) # class: data.frame

library(caret)

# this looks for highly positively correlated and highly negatively correlated pairs of columns so that we can drop them from our predictive model
descrCor <-  cor(d)


# the findcorreclation column will find all the highly correlated columns 
highlyCorDescr <- findCorrelation(descrCor, cutoff = .90)

# d is the new overwritten data frame and this drops the except for the highly correlated pairs
d <- d[,-highlyCorDescr]

# Select data.frame to be sent to the output Dataset port
maml.mapOutputPort("d")


## this essentially drops all the redundant columns that we don't need in the prediction model
```
