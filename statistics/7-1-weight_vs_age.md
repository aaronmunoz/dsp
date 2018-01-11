[Think Stats Chapter 7 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2008.html#toc70) (weight vs. age)

## Scatterplot
```python
import first

def SampleRows(df, nrows, replace=False):
    indices = np.random.choice(df.index, nrows, replace=replace)
    sample = df.loc[indices]
    return sample

live, firsts, others = first.MakeFrames()
live = live.dropna(subset=['agepreg', 'totalwgt_lb'])

thinkplot.Scatter(live.agepreg, live.totalwgt_lb, alpha=0.05)
thinkplot.Config(xlabel='Mother\'s Age',
                 ylabel='Weight (lb)',
                 axis=[13, 45, 3, 15],
                 legend=False)
```
>> ![](https://github.com/aaronmunoz/dsp/blob/master/statistics/images/q7_scatter.png)
## Percentile Plot
```python
bins = np.arange(13, 48, 5)
indices = np.digitize(live.agepreg, bins)
groups = live.groupby(indices)

ages = [group.agepreg.mean() for i, group in groups]
cdfs = [thinkstats2.Cdf(group.totalwgt_lb) for i, group in groups]

for percent in [75, 50, 25]:
    weights = [cdf.Percentile(percent) for cdf in cdfs]
    label = '%dth' % percent
    thinkplot.Plot(ages, weights, label=label)
    

thinkplot.Config(xlabel="Mother's age",
                 ylabel='Birth weight (lbs)',
                 xlim=[14, 45], legend=True)
```
>> ![](https://github.com/aaronmunoz/dsp/blob/master/statistics/images/q7_percentile.png)
## Coefficients
```python
# Pearson's correlation
from thinkstats2 import MeanVar
import math

def pearsons_corr(xs, ys):
    xs = np.asarray(xs)
    ys = np.asarray(ys)

    meanx, varx = MeanVar(xs)
    meany, vary = MeanVar(ys)
    denom = math.sqrt(varx * vary)
    
    corr = Cov(xs, ys, meanx, meany) / denom
    return corr

print (pearsons_corr(live.agepreg, live.totalwgt_lb))

# Spearman's
from thinkstats2 import SpearmanCorr

print (SpearmanCorr(live.agepreg, live.totalwgt_lb))
```
>> Pearson's: 0.0688339703541
>> Spearman's: 0.0946100410966
