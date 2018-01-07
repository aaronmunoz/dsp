[Think Stats Chapter 3 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2004.html#toc31) (actual vs. biased)

```python
import nsfg
import thinkstats2
import thinkplot

resp = nsfg.ReadFemResp()
children_count = resp['numkdhh']
children_pmf = thinkstats2.Pmf(children_count, label='actual')

# bias the children count by the observed family size
biased_pmf = children_pmf.Copy(label='biased')

for x, p in children_pmf.Items():
    biased_pmf.Mult(x, x)

biased_pmf.Normalize()

thinkplot.Pmfs([children_pmf, biased_pmf])
thinkplot.Show(xlabel='Number of children in family', ylabel='PMF')
```
![](https://github.com/aaronmunoz/dsp/blob/master/statistics/images/q2_pmf.png)
