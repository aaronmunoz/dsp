[Think Stats Chapter 4 Exercise 2](http://greenteapress.com/thinkstats2/html/thinkstats2005.html#toc41) (a random distribution)

## Generating the random numbers and PMF:
```python
import numpy as np
import thinkstats2
import thinkplot

random_numbers = np.random.random(size=1000)
pmf = thinkstats2.Pmf(random_numbers, label='random_number')

thinkplot.pmf(pmf, linewidth=0.1)
thinkplot.Show(xlabel='Number', ylabel='PMF')
```

Resulting Image:

## Generating the CDF:

```python
cdf = thinkstats2.Cdf(random_numbers, label='random_number')

thinkplot.cdf(cdf)
thinkplot.Show(xlabel='Number', ylabel='CDF')
```
