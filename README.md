# NumericalIntegration

[![Build Status](https://travis-ci.org/dextorious/NumericalIntegration.jl.svg?branch=master)](https://travis-ci.org/deXtoRious/NumericalIntegration.jl)

[![Coverage Status](https://coveralls.io/repos/dextorious/NumericalIntegration.jl/badge.svg?branch=master&service=github)](https://coveralls.io/github/dextorious/NumericalIntegration.jl?branch=master)

[![codecov.io](http://codecov.io/github/dextorious/NumericalIntegration.jl/coverage.svg?branch=master)](http://codecov.io/github/dextorious/NumericalIntegration.jl?branch=master)

This is a simple package to provide functionality for numerically integrating presampled data (meaning you can't choose arbitrary nodes). If you have the ability to evaluate your integrand at arbitrary points, please consider using better tools for the job (such as the excellent [FastGaussQuadrature.jl](https://github.com/ajt60gaibb/FastGaussQuadrature.jl)). 

Do note that while the code is trivial, it has not been extensively tested and does not focus on numerical precision. Issues, suggestions and pull requests are welcome.


## Example usage

```julia
# setup some data
x = collect(-π : π/1000 : π)
y = sin.(x)

# integrate using the default TrapezoidalFast method
integrate(x, y)

# integrate using a specific method
integrate(x, y, SimpsonEven())

# compute cumulative integral
Y = cintegrate(x, y)

# compute cumulative integral for each column of an array
z = [sin.(x) cos.(x) exp.(x/pi)]
Z = cintegrate(x, y)

```

The currently available methods are:
- Trapezoidal
- TrapezoidalEven
- TrapezoidalFast (default)
- TrapezoidalEvenFast
- SimpsonEven
- SimpsonEvenFast

Only Trapezoidal methods are available for cumumlative integrals.

All methods containing "Even" in the name assume evenly spaced data. All methods containing "Fast" omit basic correctness checks and focus on performance. Consequently, the fast methods will segfault or produce incorrect results if you supply incorrect data (vectors of different lengths, etc.).
