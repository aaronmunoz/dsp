[Think Stats Chapter 2 Exercise 4](http://greenteapress.com/thinkstats2/html/thinkstats2003.html#toc24) (Cohen's d)

```python
import thinkstats2
import nsfg
import thinkplot
import math

def cohens_d(group1, group2):
    diff = group1.mean() - group2.mean()

    var1 = group1.var()
    var2 = group2.var()
    n1, n2 = len(group1), len(group2)

    pooled_var = (n1 * var1 + n2 * var2) / (n1 + n2)
    d = diff / math.sqrt(pooled_var)
    return d

preg = nsfg.ReadFemPreg()
live = preg[preg.outcome == 1]

firsts = live[live.birthord == 1]
others = live[live.birthord != 1]

print('Cohen\'s coefficient using weight: %f' % cohens_d(firsts.totalwgt_lb, others.totalwgt_lb))
print('Cohen\'s coefficient using pregnancy length: %f' % cohens_d(firsts.prglngth, others.prglngth))

print('Effect size is very small in both cases, though weight has a bigger effect size than pregnancy length')
```
