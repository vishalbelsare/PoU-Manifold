## Files description :

- `bumpfunction.py`  : Consists of a class containing the required smooth C-inf bump functions
- `create_charts.py` : Consists code to create individual charts of the manifold
- `main.py` 		 : Consists of `main` function which computes the global approximated value using PoU
- `regression.py` 	 : Consists of a function used to fit linear/ polynomial curves to data using OLS
- `visualization.py` : For visualizing spherical manifold and individual charts

## Partition of unity:

A [partition of unity](https://en.wikipedia.org/wiki/Partition_of_unity) is a useful, though technical, tool that helps us work in local coordinates. This can be a tricky matter when we’re doing things all over our manifold, since it’s almost never the case that the entire manifold fits into a single coordinate patch. A (smooth) partition of unity is a way of breaking the function with the constant value 1 up into a bunch of (smooth) pieces that are easier to work with.

More precisely, for any covering of X (a topological space; here it is a manifold, which is a topological space with additional properties) by open subsets {Uₘ},there exists a sequence of smooth nonnegative functions {ϴₙ}, on X, called a partition of unity, subordinate to the [open cover](https://en.wikipedia.org/wiki/Cover_(topology)#Cover_in_topology) {Uₘ} such that for every point, x ∈ X :
<sub></sub>
- the sum of all function values at x is 1, i.e, ∑ ϴₙ(x) = 1. Each θ<sub>i</sub> = ( φ<sub>i</sub> / ∑<sub>j</sub> φ<sub>j</sub> ) where we have taken φ<sub>j</sub> to be a bump function. (to be precise 3 bump functions for 3 charts therefore j = 3). By this normalization, the summation ∑n ϴₙ(x) comes out to be 1.

- 0 ≤ ϴₙ(x) ≤ 1 and all 'n'

- supp ϴₙ ⊆ Uₘ for each m, where 'supp' is the [support](https://en.wikipedia.org/wiki/Support_(mathematics)) of the function.

- The family of supports (supp ϴₙ) is locally finite, meaning that every point has a neighbourhood that intersects supp ϴₙ for only finitely many values of n

## Bump Functions:

A [*bump function*](https://en.wikipedia.org/wiki/Bump_function) is a function on Cartesian Space R^n, for some n ∈ R with values in the real numbers R

					b : R^n -> R  *such that*

1) **_b_** is smooth
2) **_b_** has compact support
 
## Global approximation

Partition of unity can be used to patch together local smooth objects into global ones.

## Approach:
- We have randomly sampled n = 100 points on a R<sup>3</sup> sphere. The intrinsic dimension of this spherical manifold is 2.

- We divide the manifold into 6 charts correponding to 6 R<sup>2</sup> discs and project the 3D points, lying on the sphere, into their respective 2-dimensional discs. We do this by ignoring/removing 'z' coordinate to project on x-y plane and similarly on the other 2 planes. Each 3D point therefore now lies in 3 different charts (R<sup>2</sup> discs)

- Corresponding to each of these 3 charts, we have introduced 3 different smooth bump functions necessary for Partitons of Unity.

- We then fit linear/ Polynomial functions, locally, on each chart by taking a random target sampled from a Gaussian distribution. 

- Final approximation for a point 'x' lying on the manifold is computed as : ∑<sub>i</sub> f<sub>i</sub>(x<sub>i</sub>) * φ<sub>i</sub>(x<sub>i</sub>) where f<sub>i</sub>(x<sub>i</sub>) and φ<sub>i</sub>(x<sub>i</sub>) are the linearly fitted function value of 'x' and the bump function value of 'x' in the i<sup>th</sup> chart, respectively. The summation is taken over all the i (here i = 3) charts a point lies in.    

## Possible further work : 

Trying to globally approximate any scalar valued function (R^n -> R) other than linearly fitted function

## Spherical Dataset description:

We have taken patches/ overlapping charts such that atmost 4 patches overlap anywhere on the sphere.

## Sample dataset:

1. [Spherical manifold dataset Image](images/sphere_manifold.png)
2. [Six charts of the S^2 manifold](images/charts.png)

## Evaluation:
We have reported the *Average test loss*, *Average training loss*, *MSE* and *Standard Deviation*. *Average test loss* comes out to be ~0.20. We have used k-fold cross validation method for evaluating the results where we set k = 10. The average error is computed across all 'k' trials.
