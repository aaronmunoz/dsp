[Think Stats Chapter 6 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2007.html#toc60) (household income)

Code used for this problem
```python
def InterpolateSample(df, log_upper=6.0):
    """Makes a sample of log10 household income.

    Assumes that log10 income is uniform in each range.

    df: DataFrame with columns income and freq
    log_upper: log10 of the assumed upper bound for the highest range

    returns: NumPy array of log10 household income
    """
    # compute the log10 of the upper bound for each range
    df['log_upper'] = np.log10(df.income)

    # get the lower bounds by shifting the upper bound and filling in
    # the first element
    df['log_lower'] = df.log_upper.shift(1)
    df.loc[0, 'log_lower'] = 3.0

    # plug in a value for the unknown upper bound of the highest range
    df.loc[41, 'log_upper'] = log_upper
    
    # use the freq column to generate the right number of values in
    # each range
    arrays = []
    for _, row in df.iterrows():
        vals = np.linspace(row.log_lower, row.log_upper, row.freq)
        arrays.append(vals)

    # collect the arrays into a single sample
    log_sample = np.concatenate(arrays)
    return log_sample

import hinc
income_df = hinc.ReadData()

log_sample = InterpolateSample(income_df, log_upper=6.0)

sample = np.power(10, log_sample)

# print the values for the problem:
print('>> Median {0}\n'.format(Median(sample)))
mean = Mean(sample)
print('>> Mean {0}\n'.format(mean))
print('>> Skewness {0}\n'.format(Skewness(sample)))
print('>> PearsonMedianSkewness {0}\n'.format(PearsonMedianSkewness(sample)))

print('>> Percentage of households with income below the mean {0}'.format(cdf.Prob(mean) * 100))
```
## Output
>> Median 51226.45447894046

>> Mean 74278.70753118733

>> Skewness 4.949920244429583

>> PearsonMedianSkewness 0.7361258019141782

>> Percentage of households with income below the mean 66.0005879566872

## Running this again interpolating the data to 10 million

>> Median 51226.45447894046

>> Mean 124267.39722164685

>> Skewness 11.603690267537793

>> PearsonMedianSkewness 0.39156450927742087

>> Percentage of households with income below the mean 85.65630665207664

> As can be seen, as we interpolate the income to higher values, we can see the mean becoming increasingly skewed by high earners vs the rest of the population.
