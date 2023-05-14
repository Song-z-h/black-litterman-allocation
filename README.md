# black-litterman-allocation

# Operations Research Project

zhaohui.song@studio.unibo.it

### Portfolio Optimization problem

Imagine that we have a portfolio of N assets to invest in.  For each asset $i$, we have xi money to invest into the assets. As a total, we have W0 money at the beginning of the year.  During the year, we will have T times to rebalance the portfolio, without further injecting money into the pool, we want to maximize the wealth at time T. As constraints, we want to keep a part of the money invested in different fields: $\alpha$% in the industrial field, $\beta$% in the banking field, and $\gamma$% in the technological field. All the investments should be within the $\rho$ ratings.

### Formalizing the terms

$a_t = (a_{1,t}, a_{2,t}, ...., a_{N,t})$ Percentage invested in industry at time t

$b_t = (b_{1,t}, b_{2,t}, ...., b_{N,t})$ Percentage invested in banking at time t

$c_t = (c_{1,t}, c_{2,t}, ...., c_{N,t})$ Percentage invested in technologies at time t

$p_t = (p_{1,t}, p_{2,t}, ...., p_{N,t})$ Rating of invested assets at time t

$0 \le \alpha, \beta, \gamma, \rho \le 1$

For time t = 1, ….., T, if the T is one year, an example can be the first day of January, February, ….., December.

$x_{t} = (x_{1,t}, x_{2,t}, ....., x_{N,t})$ decision variables that indicate for a given time $t$ in the year, the amount of money invested in each of the N assets.

$\xi_t = (\xi_{1,t}, \xi_{2,t}, ........, \xi_{N, t})$ indicates for a given time $t$ in the year, the return from each of the N asset.

$W_t$ indicates for a given time $t$ in the year.

### Constraints

The total wealth for a given time t should be the sum of all money invested → $\sum_{i=1}^N x_t = W_t$ .

At time $t$ = 0, we have our constant $x_0$ to be invested,  → $\sum_{i=1}^N x_0 = W_0$ . 

At $t$ = 1, our money is the previously invested money multiplied by the returns for each asset → $ x_1 = x_0 \xi_1$ and $\sum_{i=1}^N x_1 = W_1$ should hold. 

At $t$ = T-1, we will have our $x_{T-1} = x_{T-2}\xi_{T-1}$, our wealth will be $\sum_{i=1}^N x_{T-1} = W_{T-1}$

### The rational and objective function

By thinking of the problem in the setup of dynamic programming, at the time T, we will have all the money back, thus, our objective is maximizing the Wt at the time T.

$$
\max z = W_T
$$

At time t = T-1 is the last time we could rebalance the money, we also want to maximize the optimal value $Q_T$ we can have at the future time T, it’s the best value we can obtain from the pair of wealth $W_{T}$ and returns $\xi_{T}$ for all given known previous returns $\xi_{[t]} = (\xi_1, \xi_2, ........, \xi_t)$

$$
max z = W_{T} = Q_{T}(W_{T}, \xi_{[T]})|\xi_{[T-1]}  \\\\ 
$$

$$
s.t.\quad\quad                 W_{T} = \sum_{i=1}^N x_{i,T-1}  \xi_{i,T} \\ W_{T-1} = \sum_{i=1}^Nx_{i, T-1}
$$

In a simplified version without denoting dynamic programming, the objective function can be linear, and if we sample the $\xi_{i,T}$ value, it becomes a deterministic problem:

$$
max z = W_{T} = \sum_{i=1}^N x_{i,T-1}  \xi_{i,T}
$$

At time t = 0, it’s initial time we start to invest, we want to maximize the money we can have at time t = 1, so the objective function could be:

$$
max z = W_{1} = Q_{1}(W_{1}, \xi_{[1]})|\xi_{[0]}  \\\\ s.t.\quad\quad                 W_{1} = \sum_{i=1}^N x_{i,0}  \xi_{i,1}
$$

The $\xi_{[0]}$ is zero here, because we don’t have any returns at the initial time. Again, the Q function is the optimal value we can have for the pairs of W1 and $\xi_1$ at time t = 1. 

 $\xi_{i}$ is a stochastic variable,  we can sample it from the historical distribution $\xi_i$  ~ N( $\mu_i, \sigma_i)$, not to mention, different assets will have different distributions and volatilities. So we can calculate the expected value from the objective function → $max z = E[Q_{t+1}(W_{t+1}, \xi_{[t+1]}) | \xi_{[t]}]$

### The complete model

$$
max z = E[Q_{t+1}(W_{t+1}, \xi_{[t+1]}) | \xi_{[t]}]
$$

$$
st.\quad W_{t+1} = \sum_{i=1}^N x_{i,t}\xi_{i, t+1} 
$$

$$
W_t = \sum_{i=1}^N x_{i,t}
$$

$$
\sum_{i=1}^N x_{i,t}a_{i,t} \ge \alpha W_t 
$$

$$
\sum_{i=1}^N x_{i,t}b_{i,t} \ge \beta W_t \
$$

$$
\sum_{i=1}^N x_{i,t}c_{i,t} \ge \gamma W_t 
$$

$$
\sum_{i=1}^N x_{i,t}p_{i,t} \le \rho W_t 
$$

$$
x_{i,t} \ge 0 \quad \forall i = 1...n
$$
