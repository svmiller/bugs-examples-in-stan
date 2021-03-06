
# Unidentified: over-parameterization of normal mean {#unidentified}

The following example illustrates the need for caution in diagnosing convergence, and is based on an example appearing in Carlin and Louis' Bayes and Empirical Bayes Methods for Data Analysis, 2nd edition, p174.

Consider a model of the mean, in which it it the additive sum of two parameters,
$$
\begin{aligned}[t]
y &\sim \mathsf{Normal}(\mu, 1) \\
\mu &= \theta_1 + \theta_2
\end{aligned}
$$
The data have no information about about either $\theta_1$ and $\theta_2$, but the data are informative about $\mu = \theta_1 + \theta_2$.
The likelihood function for the two unidentified parameters ($\theta_1$, $\theta_2$) has a ridge along the line,
$$
\left\{ q_1, q_2 : \bar{y} = q_1 + q_2 \right\} ,
$$
where $\bar{y}$ is the mean of the observed data.

In the Bayesian approach, we are obliged to specify priors over the model parameters.  Proper priors ensure unimodal posteriors for $q_1$ and $q_2$, and can be used to the sample from the posterior for this problem.  But as Carlin and Louis show (see their Q25, p191), we need to be careful with models of this type.  The posteriors for theta are not identical to the prior (the posterior standard deviations are 7.05, while the prior standard deviations used below are 10), suggesting that the data are somewhat informative about both theta parameters, when this is not the case.  An inexperienced user of Markov chain Monte Carlo methods might fail to recognize that the q parameters are not identified, and naively report the posterior summaries for theta generated by the software.  On the other hand, note that the identified parameter $m = q_1 + q_2$  is well behaved.



```r
library("rstan")
#> Loading required package: ggplot2
#> Loading required package: StanHeaders
#> rstan (Version 2.15.1, packaged: 2017-04-19 05:03:57 UTC, GitRev: 2e1f913d3ca3)
#> For execution on a local, multicore CPU with excess RAM we recommend calling
#> rstan_options(auto_write = TRUE)
#> options(mc.cores = parallel::detectCores())
mod_unidentified <- stan_model("stan/unidentified.stan")
#> In file included from file452878d1498c.cpp:8:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/src/stan/model/model_header.hpp:4:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math.hpp:4:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math/rev/mat.hpp:4:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math/rev/core.hpp:12:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math/rev/core/gevv_vvv_vari.hpp:5:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math/rev/core/var.hpp:7:
#> In file included from /Users/jrnold/Library/R/3.4/library/BH/include/boost/math/tools/config.hpp:13:
#> In file included from /Users/jrnold/Library/R/3.4/library/BH/include/boost/config.hpp:39:
#> /Users/jrnold/Library/R/3.4/library/BH/include/boost/config/compiler/clang.hpp:196:11: warning: 'BOOST_NO_CXX11_RVALUE_REFERENCES' macro redefined [-Wmacro-redefined]
#> #  define BOOST_NO_CXX11_RVALUE_REFERENCES
#>           ^
#> <command line>:6:9: note: previous definition is here
#> #define BOOST_NO_CXX11_RVALUE_REFERENCES 1
#>         ^
#> In file included from file452878d1498c.cpp:8:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/src/stan/model/model_header.hpp:4:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math.hpp:4:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math/rev/mat.hpp:4:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math/rev/core.hpp:42:
#> /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math/rev/core/set_zero_all_adjoints.hpp:14:17: warning: unused function 'set_zero_all_adjoints' [-Wunused-function]
#>     static void set_zero_all_adjoints() {
#>                 ^
#> In file included from file452878d1498c.cpp:8:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/src/stan/model/model_header.hpp:4:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math.hpp:4:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math/rev/mat.hpp:4:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math/rev/core.hpp:43:
#> /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math/rev/core/set_zero_all_adjoints_nested.hpp:17:17: warning: 'static' function 'set_zero_all_adjoints_nested' declared in header file should be declared 'static inline' [-Wunneeded-internal-declaration]
#>     static void set_zero_all_adjoints_nested() {
#>                 ^
#> In file included from file452878d1498c.cpp:8:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/src/stan/model/model_header.hpp:4:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math.hpp:4:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math/rev/mat.hpp:11:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math/prim/mat.hpp:59:
#> /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math/prim/mat/fun/autocorrelation.hpp:17:14: warning: function 'fft_next_good_size' is not needed and will not be emitted [-Wunneeded-internal-declaration]
#>       size_t fft_next_good_size(size_t N) {
#>              ^
#> In file included from file452878d1498c.cpp:8:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/src/stan/model/model_header.hpp:4:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math.hpp:4:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math/rev/mat.hpp:11:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math/prim/mat.hpp:298:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math/prim/arr.hpp:39:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math/prim/arr/functor/integrate_ode_rk45.hpp:13:
#> In file included from /Users/jrnold/Library/R/3.4/library/BH/include/boost/numeric/odeint.hpp:61:
#> In file included from /Users/jrnold/Library/R/3.4/library/BH/include/boost/numeric/odeint/util/multi_array_adaption.hpp:29:
#> In file included from /Users/jrnold/Library/R/3.4/library/BH/include/boost/multi_array.hpp:21:
#> In file included from /Users/jrnold/Library/R/3.4/library/BH/include/boost/multi_array/base.hpp:28:
#> /Users/jrnold/Library/R/3.4/library/BH/include/boost/multi_array/concept_checks.hpp:42:43: warning: unused typedef 'index_range' [-Wunused-local-typedef]
#>       typedef typename Array::index_range index_range;
#>                                           ^
#> /Users/jrnold/Library/R/3.4/library/BH/include/boost/multi_array/concept_checks.hpp:43:37: warning: unused typedef 'index' [-Wunused-local-typedef]
#>       typedef typename Array::index index;
#>                                     ^
#> /Users/jrnold/Library/R/3.4/library/BH/include/boost/multi_array/concept_checks.hpp:53:43: warning: unused typedef 'index_range' [-Wunused-local-typedef]
#>       typedef typename Array::index_range index_range;
#>                                           ^
#> /Users/jrnold/Library/R/3.4/library/BH/include/boost/multi_array/concept_checks.hpp:54:37: warning: unused typedef 'index' [-Wunused-local-typedef]
#>       typedef typename Array::index index;
#>                                     ^
#> 8 warnings generated.
```

Use very large scales for this; though the behavior is still present with weakly informative scales.

```r
data_unidentified <- list(
  y = 0,
  theta_mean = rep(0, 2),
  theta_scale = rep(100, 2)
)
```

```r
fit_unidentified <- sampling(mod_unidentified, data = data_unidentified,
                             refresh = -1)
```

```r
fit_unidentified
#> Inference for Stan model: unidentified.
#> 4 chains, each with iter=2000; warmup=1000; thin=1; 
#> post-warmup draws per chain=1000, total post-warmup draws=4000.
#> 
#>           mean se_mean    sd    2.5%    25%   50%   75%  97.5% n_eff Rhat
#> theta[1]  2.14    3.17 72.33 -143.32 -42.92  1.26 48.84 144.24   520 1.01
#> theta[2] -2.13    3.17 72.34 -144.19 -48.87 -1.48 43.01 142.92   520 1.01
#> mu        0.00    0.02  0.99   -1.98  -0.67  0.03  0.68   1.94  3548 1.00
#> lp__     -1.02    0.04  1.06   -4.02  -1.38 -0.68 -0.28  -0.02   579 1.01
#> 
#> Samples were drawn using NUTS(diag_e) at Wed May 31 08:42:20 2017.
#> For each parameter, n_eff is a crude measure of effective sample size,
#> and Rhat is the potential scale reduction factor on split chains (at 
#> convergence, Rhat=1).
```



This example is derived from Simon Jackman, "Unidentified: over-parameterization of normal mean", 2007-07-24, [URL](https://web-beta.archive.org/web/20070724034211/http://jackman.stanford.edu:80/mcmc/unidentified.odc).
