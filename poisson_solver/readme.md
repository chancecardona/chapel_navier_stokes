## Poisson Solver

nsPoisson is a Navier Stokes library, particularly the Poisson Solver.
This supports 2 different termination conditions:
    1. Tolerance: relatie change in the L1 norm (of P pressure) is less than tol
    2. Iteration: timesteps maxed

Uses `+ reduce` to compute the relative change in p's L1 norm between iterations. 

Also defines the poisson kernel.

```bash
chpl nsPoisson.chpl --fast --set useTolerance=false
./nsPoisson --sourceMag=500 --makePlots=true
```

neumanBC = Von Neumann Boundary conditition:
    says y velocity of dp/dy at y = 0,yLen is also 0.
    (stationary on boundary).

## Distributed Poisson Soler

This version can be distributed across clusters or supercomputer cores via the 
distributed domain:

### Testing the distributed domains:
`const dom = blockDist.createDomain({1..8, 1..8}, targetLocales=Locales);`
```bash
chpl datapar-example.chpl --fast
./datapar-example -nl 4
```

### Actual Solver
`const space = stencilDist.createDomain({0..<nx, 0..<ny}, fluff=(1,1)),`

