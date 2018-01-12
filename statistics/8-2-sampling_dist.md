[Think Stats Chapter 8 Exercise 2](http://greenteapress.com/thinkstats2/html/thinkstats2009.html#toc77) (sampling distribution)
## Running the experiment with sample sizes 10, 100, 1000, 10000
```python
import thinkstats2
import thinkplot
import numpy as np


def exponential_experiment(n = 10, lam = 2, m = 1000, print_output=True):
    means = []
    for _ in range(m):
        xs = np.random.exponential(1.0/lam, n)
        L = 1 / np.mean(xs)
        means.append(L)

    cdf = thinkstats2.Cdf(means)
    
    ci = cdf.Percentile(5), cdf.Percentile(95)
    standard_error = RMSE(means, lam)
    
    if print_output:
        thinkplot.Cdf(cdf)
        thinkplot.Config(xlabel='Sample mean',
                         ylabel='CDF')
        print('Sample Size: %d' % n)
        print('Confidence Interval: {0}'.format(ci))
        print('Error: ', RMSE(means, lam))
    
    return standard_error 

sample_sizes = [10, 100, 1000, 10000]
standard_errors = [exponential_experiment(n=x) for x in sample_sizes]

```
> > Sample Size: 10

> > Confidence Interval: (1.265692502043146, 3.4093647032642806)

> > Error: 0.7450320239501669


> > Sample Size: 100

> > Confidence Interval: (1.7013215348829434, 2.3653007278327127)

> > Error: 0.20708848741311825


> > Sample Size: 1000

> > Confidence Interval: (1.8905127214541659, 2.1119709226675805)

> > Error: 0.06702315338514128


> > Sample Size: 10000

> > Confidence Interval: (1.9662888793833311, 2.0333031032688957)

> > Error: 0.020681489081906493

> I've plotted sample size vs CDF with each of these trials (the curve is lighter with each sample size run above).
> ![](https://github.com/aaronmunoz/dsp/blob/master/statistics/images/q8_cdf_sample_sizes.png)

> This shows the confidence interval becoming smaller, closing in on mu(2) as sample size increases
## Plotting sample size vs error (sizes 1 to 1000)
```python
sample_sizes = range(1, 1001)
standard_errors = [exponential_experiment(n=x, print_output=False) for x in sample_sizes]

thinkplot.Scatter(sample_sizes, standard_errors, alpha=0.5)
thinkplot.Config(xlabel='Sample size',
                 ylabel='Standard Error',
                 axis=[0, 1001, 0, 1],
                 legend=False)
```
> ![](https://github.com/aaronmunoz/dsp/blob/master/statistics/images/q8_sample_v_error.png)

> As can be seen from the plot, as sample size increases, standard error decreases

