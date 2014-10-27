# Exponential Distribution Simulation and Analysis
Liang Dong  
22 October 2014  

# Introduction

In this pdf, the distribution of mean of 40 exponential(0.2)s will be simulated and analyzed in R using method rexp(n, lambda). The variable n is set to 40, and lambda is set to 0.2. The number of oberservations is set to 1000.

The mean value, standard deviation and variance of the distribution are caculated in this pdf, and are compared to theoretical value. 

The distribution graph is also comapred to the normal distribution on the same plot. Also, the confidence interval for 1.96, which is approximately 95% of the interval is provided in the last section.

# Preparation

First load the packages, set the global variable n, lambda and number of oberservations, and simualte 40 exponential(0.2)s for 1000 times.


```r
# set global chunk options
library(ggplot2)
nosim = 1000
lambda = 0.2 
n = 40
dat <- apply(matrix(rexp(40 * nosim, 0.2), nosim, 40, byrow = TRUE), 1, mean)
```

# Simulation Analysis

## Comparison of mean of simulation and theoretical value


```r
sim_mean <- mean(dat)
theo_mean <- 1/lambda
```

So the distribution is centered at **5.0549** and the theoretical mean is centered at **5**

## Comparison the variance of the simulation and theoretical value.


```r
sim_sd <- sd(dat)
theo_sd <- 1/lambda/sqrt(40)
sim_var <- var(dat)
theo_var <- theo_sd^2
```

So the standard deviation of the simulation is **0.7985** and the theoretical standard deviation is **0.7906**.

The variance of the simulation is **0.6375** and the theoretical variance is **0.625**

## Show that the distribution is approximately normal.


```r
dat_frame <- data.frame(dat)
colnames(dat_frame) <- 'mean'
ggplot(dat_frame, aes(x = mean)) + geom_histogram(aes(y=..density..), alpha = .20, binwidth=.3, colour = "black") + stat_function(fun = dnorm, arg = list(mean = 5, sd = sd(dat_frame$mean)), colour = "red") + xlab("Mean Value Distribution") + ylab("Density") + ggtitle("Distribution of Averages of 40 Exponential(0.2)s")
```

![plot of chunk plot](./stat_infer_files/figure-html/plot.png) 

We can concludes from the graph that the distribution is approximately the same as the normal distribution.

## Coverage of the confidence interval for 1/lambda


```r
interval <- sim_mean + c(-1, 1) * 1.96 * (sim_sd/sqrt(n))
```

The confidence interval for 1/lambda is **[4.8074, 5.3023]** 

