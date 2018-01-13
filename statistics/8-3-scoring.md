[Think Stats Chapter 8 Exercise 3](http://greenteapress.com/thinkstats2/html/thinkstats2009.html#toc77)

---
## Using the method provided in the workbook for simulating the games
```python
def SimulateGame(lam):
    """Simulates a game and returns the estimated goal-scoring rate.

    lam: actual goal scoring rate in goals per game
    """
    goals = 0
    t = 0
    while True:
        time_between_goals = random.expovariate(lam)
        t += time_between_goals
        if t > 1:
            break
        goals += 1

    # estimated goal-scoring rate is the actual number of goals scored
    L = goals
    return L
    
number_of_games = 10000
lam = 2

simulated_goals = [SimulateGame(lam) for _ in range(number_of_games)]
simulated_games_rmse = RMSE(simulated_goals, lam)
simulated_games_mean_error = MeanError(simulated_goals, lam)
print ('RMSE for simulated games: {0}'.format(simulated_games_rmse))
print ('Mean Error for simulated games: {0}'.format(simulated_games_mean_error))
```
> > RMSE for simulated games: 1.4190489773083943
> > Mean Error for simulated games: 0.0199

> A mean error of 0.0199 indicates that this is an unbiased estimator
---
