# Lession 1

https://www.youtube.com/watch?v=GCoP2w-Cqtg

## Notes

### Intro

- Represent everything as vectors
- Treat "what is a good image?" as a dataset problem: How often does this caption appear with this image on the internet.
- z ~ Pdata (.|y) - Conditional generation means sampling the data distribution
- A generative model converts samples from an initial distribution into samples from the data distribution

- If struggling, focus on understanding the flow component first before the diffusion component.

- Trajectory: X[0, ^] -> Rd, t -> Xt - A solution to an ODE.
    -  A function of time. Given a time t gives you a vector Xt. In 2D this is
       a point moving through space with a trajectory Xy
- Vector field: u Rd x [0, ^] -> Rd - Defines an ODE.
    (x, t) -> ut(x)
    - Gives you directions at every point
- Ordinary differential equation (ODE). Describes conditions on a trajectory.
    - A trajectory should start a specific point (initial condition).  X=X0
    - We want to follow the vector field.
    - d/dt Xt = ut(xt)
- Flow - collection of trajectories that follow the ODE.
    - psi: Rd x [0, ^] -> Rd
    - Collection of solutions for an ODE that follow initial conditions
- Key takeaway: Implicitly, in all practical cases unique solutions to ODE/flows exist

- How to generate objects:
  - t=0
  - Set step size h=1/n
  - Draw a sample Xo ~ Pinit
  - For i = 1, ..., n-1 do
      - Xt+h = Xt + hu(Xt)
      - t <- t + h
  - return X1

  - Brownian motion is a stochastic process
    - A specific kernel of a gausian process.
    - Wo = 0
    - Gausian increments: Wt - Ws ~ N(0, (t-s)Id) ^ (0, s, t)
        - Variance increases with time
    - Independent increments: Wt1 - Wt0, ...., Wtn - Wtn-m are independent

- Numerical SDE simulation - sampling from an SDE

- Sampling from diffusion model - Euler-Maruyama method
  - t = 0
  - Set step size h = 1/n
  - Draw a sample Xo ~ Pinit
  - For i = 1, ..., n-1 do
    - Draw a sample e ~ N(0, Id)
    - Xt+h = Xt + hu(Xt) + gt root(h) e
    - t <- t + h
  - return X1
