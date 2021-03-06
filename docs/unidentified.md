
# Unidentified: Over-Parameterization of a Normal Mean {#unidentified}

The following example illustrates the need for caution in diagnosing convergence, and is based on an example appearing in @CarlinLouis2000a [p174].

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

Bayesian models require the specification of priors for model parameters.  Proper priors will ensure unimodal posteriors for $q_1$ and $q_2$, and
can be used to sample from the posterior for this problem. @CarlinLouis2000a show (see their Q25, p191) the dangers of models of this
type.  The posteriors for $\theta$ are not identical to the prior (the posterior
standard deviations are 7.05, while the prior standard deviations used below
are 10), suggesting that the data are somewhat informative about both $\theta$
parameters, when this is not the case.  An inexperienced user of Markov chain
Monte Carlo methods might fail to recognize that the $q$ parameters are not
identified, and naively report the posterior summaries for theta generated by
the software.  On the other hand, note that the identified parameter $m = q_1 +
q_2$ is well behaved


```r
library("rstan")
#> Loading required package: ggplot2
#> Loading required package: StanHeaders
#> rstan (Version 2.17.3, GitRev: 2e1f913d3ca3)
#> For execution on a local, multicore CPU with excess RAM we recommend calling
#> options(mc.cores = parallel::detectCores()).
#> To avoid recompilation of unchanged Stan programs, we recommend calling
#> rstan_options(auto_write = TRUE)
mod_unidentified <- stan_model("stan/unidentified.stan")
#> In file included from file197e546fe7ff.cpp:8:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/src/stan/model/model_header.hpp:4:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math.hpp:4:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math/rev/mat.hpp:4:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math/rev/core.hpp:12:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math/rev/core/gevv_vvv_vari.hpp:5:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math/rev/core/var.hpp:7:
#> In file included from /Users/jrnold/Library/R/3.4/library/BH/include/boost/math/tools/config.hpp:13:
#> In file included from /Users/jrnold/Library/R/3.4/library/BH/include/boost/config.hpp:39:
#> /Users/jrnold/Library/R/3.4/library/BH/include/boost/config/compiler/clang.hpp:200:11: warning: 'BOOST_NO_CXX11_RVALUE_REFERENCES' macro redefined [-Wmacro-redefined]
#> #  define BOOST_NO_CXX11_RVALUE_REFERENCES
#>           ^
#> <command line>:6:9: note: previous definition is here
#> #define BOOST_NO_CXX11_RVALUE_REFERENCES 1
#>         ^
#> In file included from file197e546fe7ff.cpp:8:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/src/stan/model/model_header.hpp:4:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math.hpp:4:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math/rev/mat.hpp:4:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math/rev/core.hpp:14:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math/rev/core/matrix_vari.hpp:4:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math/rev/mat/fun/Eigen_NumTraits.hpp:4:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math/prim/mat/fun/Eigen.hpp:4:
#> In file included from /Users/jrnold/Library/R/3.4/library/RcppEigen/include/Eigen/Dense:1:
#> In file included from /Users/jrnold/Library/R/3.4/library/RcppEigen/include/Eigen/Core:531:
#> /Users/jrnold/Library/R/3.4/library/RcppEigen/include/Eigen/src/Core/util/ReenableStupidWarnings.h:10:30: warning: pragma diagnostic pop could not pop, no matching push [-Wunknown-pragmas]
#>     #pragma clang diagnostic pop
#>                              ^
#> In file included from file197e546fe7ff.cpp:8:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/src/stan/model/model_header.hpp:4:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math.hpp:4:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math/rev/mat.hpp:4:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math/rev/core.hpp:14:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math/rev/core/matrix_vari.hpp:4:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math/rev/mat/fun/Eigen_NumTraits.hpp:4:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math/prim/mat/fun/Eigen.hpp:4:
#> In file included from /Users/jrnold/Library/R/3.4/library/RcppEigen/include/Eigen/Dense:2:
#> In file included from /Users/jrnold/Library/R/3.4/library/RcppEigen/include/Eigen/LU:47:
#> /Users/jrnold/Library/R/3.4/library/RcppEigen/include/Eigen/src/Core/util/ReenableStupidWarnings.h:10:30: warning: pragma diagnostic pop could not pop, no matching push [-Wunknown-pragmas]
#>     #pragma clang diagnostic pop
#>                              ^
#> In file included from file197e546fe7ff.cpp:8:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/src/stan/model/model_header.hpp:4:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math.hpp:4:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math/rev/mat.hpp:4:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math/rev/core.hpp:14:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math/rev/core/matrix_vari.hpp:4:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math/rev/mat/fun/Eigen_NumTraits.hpp:4:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math/prim/mat/fun/Eigen.hpp:4:
#> In file included from /Users/jrnold/Library/R/3.4/library/RcppEigen/include/Eigen/Dense:3:
#> In file included from /Users/jrnold/Library/R/3.4/library/RcppEigen/include/Eigen/Cholesky:12:
#> In file included from /Users/jrnold/Library/R/3.4/library/RcppEigen/include/Eigen/Jacobi:29:
#> /Users/jrnold/Library/R/3.4/library/RcppEigen/include/Eigen/src/Core/util/ReenableStupidWarnings.h:10:30: warning: pragma diagnostic pop could not pop, no matching push [-Wunknown-pragmas]
#>     #pragma clang diagnostic pop
#>                              ^
#> In file included from file197e546fe7ff.cpp:8:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/src/stan/model/model_header.hpp:4:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math.hpp:4:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math/rev/mat.hpp:4:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math/rev/core.hpp:14:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math/rev/core/matrix_vari.hpp:4:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math/rev/mat/fun/Eigen_NumTraits.hpp:4:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math/prim/mat/fun/Eigen.hpp:4:
#> In file included from /Users/jrnold/Library/R/3.4/library/RcppEigen/include/Eigen/Dense:3:
#> In file included from /Users/jrnold/Library/R/3.4/library/RcppEigen/include/Eigen/Cholesky:43:
#> /Users/jrnold/Library/R/3.4/library/RcppEigen/include/Eigen/src/Core/util/ReenableStupidWarnings.h:10:30: warning: pragma diagnostic pop could not pop, no matching push [-Wunknown-pragmas]
#>     #pragma clang diagnostic pop
#>                              ^
#> In file included from file197e546fe7ff.cpp:8:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/src/stan/model/model_header.hpp:4:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math.hpp:4:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math/rev/mat.hpp:4:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math/rev/core.hpp:14:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math/rev/core/matrix_vari.hpp:4:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math/rev/mat/fun/Eigen_NumTraits.hpp:4:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math/prim/mat/fun/Eigen.hpp:4:
#> In file included from /Users/jrnold/Library/R/3.4/library/RcppEigen/include/Eigen/Dense:4:
#> In file included from /Users/jrnold/Library/R/3.4/library/RcppEigen/include/Eigen/QR:17:
#> In file included from /Users/jrnold/Library/R/3.4/library/RcppEigen/include/Eigen/Householder:27:
#> /Users/jrnold/Library/R/3.4/library/RcppEigen/include/Eigen/src/Core/util/ReenableStupidWarnings.h:10:30: warning: pragma diagnostic pop could not pop, no matching push [-Wunknown-pragmas]
#>     #pragma clang diagnostic pop
#>                              ^
#> In file included from file197e546fe7ff.cpp:8:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/src/stan/model/model_header.hpp:4:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math.hpp:4:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math/rev/mat.hpp:4:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math/rev/core.hpp:14:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math/rev/core/matrix_vari.hpp:4:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math/rev/mat/fun/Eigen_NumTraits.hpp:4:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math/prim/mat/fun/Eigen.hpp:4:
#> In file included from /Users/jrnold/Library/R/3.4/library/RcppEigen/include/Eigen/Dense:5:
#> In file included from /Users/jrnold/Library/R/3.4/library/RcppEigen/include/Eigen/SVD:48:
#> /Users/jrnold/Library/R/3.4/library/RcppEigen/include/Eigen/src/Core/util/ReenableStupidWarnings.h:10:30: warning: pragma diagnostic pop could not pop, no matching push [-Wunknown-pragmas]
#>     #pragma clang diagnostic pop
#>                              ^
#> In file included from file197e546fe7ff.cpp:8:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/src/stan/model/model_header.hpp:4:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math.hpp:4:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math/rev/mat.hpp:4:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math/rev/core.hpp:14:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math/rev/core/matrix_vari.hpp:4:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math/rev/mat/fun/Eigen_NumTraits.hpp:4:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math/prim/mat/fun/Eigen.hpp:4:
#> In file included from /Users/jrnold/Library/R/3.4/library/RcppEigen/include/Eigen/Dense:6:
#> In file included from /Users/jrnold/Library/R/3.4/library/RcppEigen/include/Eigen/Geometry:58:
#> /Users/jrnold/Library/R/3.4/library/RcppEigen/include/Eigen/src/Core/util/ReenableStupidWarnings.h:10:30: warning: pragma diagnostic pop could not pop, no matching push [-Wunknown-pragmas]
#>     #pragma clang diagnostic pop
#>                              ^
#> In file included from file197e546fe7ff.cpp:8:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/src/stan/model/model_header.hpp:4:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math.hpp:4:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math/rev/mat.hpp:4:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math/rev/core.hpp:14:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math/rev/core/matrix_vari.hpp:4:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math/rev/mat/fun/Eigen_NumTraits.hpp:4:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math/prim/mat/fun/Eigen.hpp:4:
#> In file included from /Users/jrnold/Library/R/3.4/library/RcppEigen/include/Eigen/Dense:7:
#> In file included from /Users/jrnold/Library/R/3.4/library/RcppEigen/include/Eigen/Eigenvalues:58:
#> /Users/jrnold/Library/R/3.4/library/RcppEigen/include/Eigen/src/Core/util/ReenableStupidWarnings.h:10:30: warning: pragma diagnostic pop could not pop, no matching push [-Wunknown-pragmas]
#>     #pragma clang diagnostic pop
#>                              ^
#> In file included from file197e546fe7ff.cpp:8:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/src/stan/model/model_header.hpp:4:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math.hpp:4:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math/rev/mat.hpp:4:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math/rev/core.hpp:36:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math/rev/core/operator_unary_plus.hpp:7:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math/prim/scal/fun/constants.hpp:4:
#> In file included from /Users/jrnold/Library/R/3.4/library/BH/include/boost/math/constants/constants.hpp:13:
#> In file included from /Users/jrnold/Library/R/3.4/library/BH/include/boost/math/tools/convert_from_string.hpp:15:
#> In file included from /Users/jrnold/Library/R/3.4/library/BH/include/boost/lexical_cast.hpp:32:
#> In file included from /Users/jrnold/Library/R/3.4/library/BH/include/boost/lexical_cast/try_lexical_convert.hpp:42:
#> In file included from /Users/jrnold/Library/R/3.4/library/BH/include/boost/lexical_cast/detail/converter_lexical.hpp:52:
#> In file included from /Users/jrnold/Library/R/3.4/library/BH/include/boost/container/container_fwd.hpp:61:
#> /Users/jrnold/Library/R/3.4/library/BH/include/boost/container/detail/std_fwd.hpp:27:1: warning: inline namespaces are a C++11 feature [-Wc++11-inline-namespace]
#> BOOST_MOVE_STD_NS_BEG
#> ^
#> /Users/jrnold/Library/R/3.4/library/BH/include/boost/move/detail/std_ns_begin.hpp:18:34: note: expanded from macro 'BOOST_MOVE_STD_NS_BEG'
#>    #define BOOST_MOVE_STD_NS_BEG _LIBCPP_BEGIN_NAMESPACE_STD
#>                                  ^
#> /Applications/Xcode.app/Contents/Developer/Toolchains/XcodeDefault.xctoolchain/usr/include/c++/v1/__config:439:52: note: expanded from macro '_LIBCPP_BEGIN_NAMESPACE_STD'
#> #define _LIBCPP_BEGIN_NAMESPACE_STD namespace std {inline namespace _LIBCPP_NAMESPACE {
#>                                                    ^
#> In file included from file197e546fe7ff.cpp:8:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/src/stan/model/model_header.hpp:4:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math.hpp:4:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math/rev/mat.hpp:12:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math/prim/mat.hpp:83:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math/prim/mat/fun/csr_extract_u.hpp:6:
#> In file included from /Users/jrnold/Library/R/3.4/library/RcppEigen/include/Eigen/Sparse:26:
#> In file included from /Users/jrnold/Library/R/3.4/library/RcppEigen/include/Eigen/SparseCore:66:
#> /Users/jrnold/Library/R/3.4/library/RcppEigen/include/Eigen/src/Core/util/ReenableStupidWarnings.h:10:30: warning: pragma diagnostic pop could not pop, no matching push [-Wunknown-pragmas]
#>     #pragma clang diagnostic pop
#>                              ^
#> In file included from file197e546fe7ff.cpp:8:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/src/stan/model/model_header.hpp:4:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math.hpp:4:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math/rev/mat.hpp:12:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math/prim/mat.hpp:83:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math/prim/mat/fun/csr_extract_u.hpp:6:
#> In file included from /Users/jrnold/Library/R/3.4/library/RcppEigen/include/Eigen/Sparse:27:
#> In file included from /Users/jrnold/Library/R/3.4/library/RcppEigen/include/Eigen/OrderingMethods:71:
#> /Users/jrnold/Library/R/3.4/library/RcppEigen/include/Eigen/src/Core/util/ReenableStupidWarnings.h:10:30: warning: pragma diagnostic pop could not pop, no matching push [-Wunknown-pragmas]
#>     #pragma clang diagnostic pop
#>                              ^
#> In file included from file197e546fe7ff.cpp:8:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/src/stan/model/model_header.hpp:4:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math.hpp:4:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math/rev/mat.hpp:12:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math/prim/mat.hpp:83:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math/prim/mat/fun/csr_extract_u.hpp:6:
#> In file included from /Users/jrnold/Library/R/3.4/library/RcppEigen/include/Eigen/Sparse:29:
#> In file included from /Users/jrnold/Library/R/3.4/library/RcppEigen/include/Eigen/SparseCholesky:43:
#> /Users/jrnold/Library/R/3.4/library/RcppEigen/include/Eigen/src/Core/util/ReenableStupidWarnings.h:10:30: warning: pragma diagnostic pop could not pop, no matching push [-Wunknown-pragmas]
#>     #pragma clang diagnostic pop
#>                              ^
#> In file included from file197e546fe7ff.cpp:8:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/src/stan/model/model_header.hpp:4:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math.hpp:4:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math/rev/mat.hpp:12:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math/prim/mat.hpp:83:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math/prim/mat/fun/csr_extract_u.hpp:6:
#> In file included from /Users/jrnold/Library/R/3.4/library/RcppEigen/include/Eigen/Sparse:32:
#> In file included from /Users/jrnold/Library/R/3.4/library/RcppEigen/include/Eigen/SparseQR:35:
#> /Users/jrnold/Library/R/3.4/library/RcppEigen/include/Eigen/src/Core/util/ReenableStupidWarnings.h:10:30: warning: pragma diagnostic pop could not pop, no matching push [-Wunknown-pragmas]
#>     #pragma clang diagnostic pop
#>                              ^
#> In file included from file197e546fe7ff.cpp:8:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/src/stan/model/model_header.hpp:4:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math.hpp:4:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math/rev/mat.hpp:12:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math/prim/mat.hpp:83:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math/prim/mat/fun/csr_extract_u.hpp:6:
#> In file included from /Users/jrnold/Library/R/3.4/library/RcppEigen/include/Eigen/Sparse:33:
#> In file included from /Users/jrnold/Library/R/3.4/library/RcppEigen/include/Eigen/IterativeLinearSolvers:46:
#> /Users/jrnold/Library/R/3.4/library/RcppEigen/include/Eigen/src/Core/util/ReenableStupidWarnings.h:10:30: warning: pragma diagnostic pop could not pop, no matching push [-Wunknown-pragmas]
#>     #pragma clang diagnostic pop
#>                              ^
#> In file included from file197e546fe7ff.cpp:388:
#> In file included from /Users/jrnold/Library/R/3.4/library/rstan/include/rstan/rstaninc.hpp:3:
#> In file included from /Users/jrnold/Library/R/3.4/library/rstan/include/rstan/stan_fit.hpp:36:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/src/stan/services/optimize/bfgs.hpp:11:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/src/stan/optimization/bfgs.hpp:9:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/src/stan/optimization/lbfgs_update.hpp:6:
#> In file included from /Users/jrnold/Library/R/3.4/library/BH/include/boost/circular_buffer.hpp:54:
#> In file included from /Users/jrnold/Library/R/3.4/library/BH/include/boost/circular_buffer/details.hpp:20:
#> In file included from /Users/jrnold/Library/R/3.4/library/BH/include/boost/move/move.hpp:30:
#> In file included from /Users/jrnold/Library/R/3.4/library/BH/include/boost/move/iterator.hpp:27:
#> /Users/jrnold/Library/R/3.4/library/BH/include/boost/move/detail/iterator_traits.hpp:29:1: warning: inline namespaces are a C++11 feature [-Wc++11-inline-namespace]
#> BOOST_MOVE_STD_NS_BEG
#> ^
#> /Users/jrnold/Library/R/3.4/library/BH/include/boost/move/detail/std_ns_begin.hpp:18:34: note: expanded from macro 'BOOST_MOVE_STD_NS_BEG'
#>    #define BOOST_MOVE_STD_NS_BEG _LIBCPP_BEGIN_NAMESPACE_STD
#>                                  ^
#> /Applications/Xcode.app/Contents/Developer/Toolchains/XcodeDefault.xctoolchain/usr/include/c++/v1/__config:439:52: note: expanded from macro '_LIBCPP_BEGIN_NAMESPACE_STD'
#> #define _LIBCPP_BEGIN_NAMESPACE_STD namespace std {inline namespace _LIBCPP_NAMESPACE {
#>                                                    ^
#> In file included from file197e546fe7ff.cpp:8:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/src/stan/model/model_header.hpp:4:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math.hpp:4:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math/rev/mat.hpp:4:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math/rev/core.hpp:44:
#> /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math/rev/core/set_zero_all_adjoints.hpp:14:17: warning: unused function 'set_zero_all_adjoints' [-Wunused-function]
#>     static void set_zero_all_adjoints() {
#>                 ^
#> In file included from file197e546fe7ff.cpp:8:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/src/stan/model/model_header.hpp:4:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math.hpp:4:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math/rev/mat.hpp:4:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math/rev/core.hpp:45:
#> /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math/rev/core/set_zero_all_adjoints_nested.hpp:17:17: warning: 'static' function 'set_zero_all_adjoints_nested' declared in header file should be declared 'static inline' [-Wunneeded-internal-declaration]
#>     static void set_zero_all_adjoints_nested() {
#>                 ^
#> In file included from file197e546fe7ff.cpp:8:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/src/stan/model/model_header.hpp:4:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math.hpp:4:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math/rev/mat.hpp:12:
#> In file included from /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math/prim/mat.hpp:58:
#> /Users/jrnold/Library/R/3.4/library/StanHeaders/include/stan/math/prim/mat/fun/autocorrelation.hpp:17:14: warning: function 'fft_next_good_size' is not needed and will not be emitted [-Wunneeded-internal-declaration]
#>       size_t fft_next_good_size(size_t N) {
#>              ^
#> 19 warnings generated.
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
#> theta[1]  1.20    3.41 70.86 -139.24 -43.10  1.23 47.67 143.20   432 1.01
#> theta[2] -1.19    3.41 70.88 -143.60 -47.68 -1.24 43.03 139.04   432 1.01
#> mu        0.01    0.02  0.99   -2.00  -0.67  0.03  0.69   1.93  3596 1.00
#> lp__     -1.00    0.05  1.03   -3.68  -1.40 -0.68 -0.27  -0.02   503 1.01
#> 
#> Samples were drawn using NUTS(diag_e) at Fri Apr 20 01:22:45 2018.
#> For each parameter, n_eff is a crude measure of effective sample size,
#> and Rhat is the potential scale reduction factor on split chains (at 
#> convergence, Rhat=1).
```

This example is derived from Simon Jackman, "Unidentified: over-parameterization of normal mean", 2007-07-24, [URL](https://web-beta.archive.org/web/20070724034211/http://jackman.stanford.edu:80/mcmc/unidentified.odc).
