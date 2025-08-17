# Lession 1

https://www.youtube.com/watch?v=yFD-JSSG-D0

## Notes

- Condition - on a single point
- Marginal - across points
- Probability path: Interpolation between noise and data distributions.

- Diac distribution: Fancy way of saying it always returns the same value

### Conditional probabilty 

- Conditional probability - smoothly interpoilate between a guassian and the data point
    - pt(Iz) - distribution over R
    - p0(Iz) = Pinit - noise
    - p1(Iz) = dz - destination ("red dot")
- Example: Gaussian probability path
    - noise schedulers
       - alpha: 0 to 1 
       - beta: 1 to 0
    - we specify these as a design choice. common examples:
       - a = t
       - b = 1 - t
    - Given the variance 

### Marginal probabilty path

- Make datapoint set random. This means during training, draw a random sample
