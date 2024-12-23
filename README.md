# Time-Series
Labs for the Time series and sequence analysis course

## lab 1

Autoregressive models

## lab 2 

Kalman filter and EM algorithm

## lab 3

Nonlinear state space models and Sequential Monte Carlo

## lab 4

RNN's

# Example code for the em algorithm on gamma and epsilon (mu is fixed at 0.01) on the kalman filter


```Python

    from math import log as log

    num_iter = 100

    sigma_seas = 1 # initial values

    sigma_eps = 1
    
    sigma_mu = 0.01 # fixed value

    list_sigma_seas = [] # lists to save results

    list_sigma_eps = []

    loglikes = []

    for r in range(1,num_iter):
    
        # E-step
    
        Q = np.array([[sigma_mu**2, 0.], [0., sigma_seas**2]]) # setting up Q
        model = LGSS(T, R, Q, Z, sigma_eps**2, a1, P1) # getting model params
        kalle = kalman_filter(y[:800],model) # kalman filter
        loglikes.append(loglike(y[:800],kalle,0))# loglikelihood
        if (abs(0-loglikes[r-1]) < 0.001): # break if we are close to optima
          break
        smooth = kalman_smoother(y[:800],model,kalle) # run the smoothing function
        # M-step
    
        d = np.sum((smooth.eta_hat*smooth.eta_hat + smooth.eta_cov), axis=2)[1,1] # getting d from 
        sigma_seas = np.sqrt(d/n) # d devided by n(n) then square root to get standard deviation
        sigma_eps = np.sqrt((1/n) * np.sum(smooth.eps_hat**2+smooth.eps_var))
        list_sigma_seas.append(sigma_seas) # appending results
        list_sigma_eps.append(sigma_eps)
        
```






<br>
<br>
<div align="center">
  <img src="https://media1.tenor.com/m/ThADbNtGWcwAAAAd/stock-market.gif" width="600" height="600"/>
</div>
