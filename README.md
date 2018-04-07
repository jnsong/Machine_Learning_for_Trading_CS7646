# Georgia Tech OMCS CS7646 Assignment files 
#### Mike Tong
***
This repo contains assignment code for the 2018 Spring semester of the graduate course, Machine Learning for Trading. 
The data used for these projects is historical stock data for numerous tickers as csv files from 2000 to 2012.  
The util.py library is provided, which reads a csv file and returns a pandas.DataFrame with specific stock information.
***
[__Project 1 (Assess portfolio)__](http://quantsoftware.gatech.edu/Assess_portfolio): The purpose of this project is to establish portfolio performance metrics based on a specific allocation of different shares.  
The API this is built to is: 
```python
import datetime as dt

cr, adr, sddr, sr, ev = \
    assess_portfolio(sd=dt.datetime(2008,1,1), ed=dt.datetime(2009,1,1), \
    syms=['GOOG','AAPL','GLD','XOM'], \
    allocs=[0.1,0.2,0.3,0.4], \
    sv=1000000, rfr=0.0, sf=252.0, \
    gen_plot=False)
```
Which returns the cumulative returns (cr), average daily returns (adr), volatility (sddr), Sharpe ratio (sr), and the end value (ev).

***
[__Project 2 (Optimize something)__](http://quantsoftware.gatech.edu/Optimize_something): Simple project using scipy.optimize to generate a portfolio allocation that minimizes the Sharpe ratio.  
The API this project is built to is:
```python
import datetime as dt

allocs, cr, adr, sddr, sr = \
    optimize_portfolio(sd=dt.datetime(2008,1,1), ed=dt.datetime(2009,1,1), \
    syms=['GOOG','AAPL','GLD','XOM'], gen_plot=False)
```
Which returns a list of allocation values for the given ticker symbols.

***
[__Project 3 (Assess learners)__](http://quantsoftware.gatech.edu/Assess_learners): This project involved the implementation of a decision tree learner on various CSV files to generate regression outputs. The decision tree was implemented using a recursive method, a random tree learner, baggng learner, and bagging of bagging learners (insane learner) was also employed.  
The API this project is build to is

```python
import DTLearner as dt
import RTlearner as rt
import BagLearner as bl
import InsaneLearner as it

learner = dt.DTLearner(leaf_size = 1, verbose = False) # constructor
learner.addEvidence(Xtrain, Ytrain) # training step
Y = learner.query(Xtest) # query

learner = rt.RTLearner(leaf_size = 1, verbose = False) # constructor
learner.addEvidence(Xtrain, Ytrain) # training step
Y = learner.query(Xtest) # query

learner = bl.BagLearner(learner = al.ArbitraryLearner, kwargs = {"argument1":1, "argument2":2}, bags = 20, boost = False, verbose = False)
learner.addEvidence(Xtrain, Ytrain)
Y = learner.query(Xtest)

learner = it.InsaneLearner(verbose = False) # constructor
learner.addEvidence(Xtrain, Ytrain) # training step
Y = learner.query(Xtest) # query
```
These APIs return a query of results, which represent regression values generated by the different implementations.

***
[__Project 4 (Defeat learners)__](http://quantsoftware.gatech.edu/Defeat_learners): This project was to develop datasets that would be optimized for either a linear regression learner, or a decision tree, and do poorly for the other. 

***
[__Project 5 (Marketsim)__](http://quantsoftware.gatech.edu/Marketsim): The goal of this project was to develop a function that would accept a orders dataframe, which represented different stock symbols, quantity of shares, and whether it's a buy or sell. The output of this function is a single column dataframe that represents the value of the entire portfolio over the entirety of the orders dataframe date range.  
The API this project is built to is:
```python
portval = compute_portvals(orders_file = "./orders/orders.csv", start_val, commission = 9.95, impact = 0.005)
```
Which returns a dataframe with every date between the first and last dates in the orders file as its index, and the value of the portfolio over time. 

***
[__Project 6 (Manual strategy)__](http://quantsoftware.gatech.edu/Manual_strategy): The goal of this project is to develop a function that will generate an orders dataframe that will be evaluated with the Marketsim function. This orders dataframe is generated through the employment of various technical analysis methods.  
The API this project is build to is:
```python
df_trades = ms.testPolicy(symbol, sd, ed, sv)
```
Which returns a orders dataframe that can be run through a modified version of the Marketsim function to generate a portfolio value. 

***
[__Project 7 (QLearning robot)__](http://quantsoftware.gatech.edu/Qlearning_robot): The goal of this project is to develop a QLearner class that will provide a robot in a 2D world the ability to navigate using Q learning. This script establishes a Q-Table, and has the optional ability to implement Dyna-Q.
The API (pseudocode) this project is build to is:
```python
Instantiate the learner with the constructor QLearner()
s = initial_location
a = querysetstate(s)
s_prime = new location according to action a
r = -1.0
while not converged:
    a = query(s_prime, r) 
    s_prime = new location according to action a
    if s_prime == goal:
        r = +1
        s_prime = start location
    else if s_prime == quicksand:
        r = -100
    else:
        r = -1
```
Which will return the robot's cost of navigating to a location using the learning method.
