[Think Stats Chapter 5 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2006.html#toc50) (blue men)

'''python
import scipy.stats

mu = 178
sigma = 7.7
dist = scipy.stats.norm(loc=mu, scale=sigma)

lower_bound_cm = (5*12 + 10) * 2.54
upper_bound_cm = (6*12 + 1) * 2.54
blue_man_population = dist.cdf(upper_bound_cm) - dist.cdf(lower_bound_cm)

print ('Percentage of the male population capapble of joining Blue Man Group: %f' % (blue_man_population * 100))
'''

>> Percentage of the male population capapble of joining Blue Man Group: 34.274684
