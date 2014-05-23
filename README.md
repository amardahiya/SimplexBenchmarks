SimplexBenchmarks
=================
Benchmarks comparing individual operations of the Simplex method for linear programming in Julia and other languages. Uses modified version of **[jlSimplex]** to generate data from real instances.

[jlSimplex]: https://github.com/mlubin/jlSimplex

## To compile

* Run ```make``` in ```C++``` directory.
* Run ```javac runbench.java``` in the ```Java``` directory.

## To run

Be sure to have ```julia```, ```matlab```, ```pypy```, ```python2.7```, and ```java``` in your path. 
The GLPK julia package is used to extract the instance data from MPS format, install it with ``Pkg.add("GLPK")`` from a Julia prompt. Then run: ```julia runBenchmarks.jl```. The initial run will take a long time (up to an hour) as the iteration data are generated by running the simplex algorithm. Note that the iteration data (*.dump files) may require up to 800MB.

## Timings on a laptop (Intel i5-3320M, Julia 0.1):

	Geometric mean (relative to C++bnd):
			Julia	C++		C++bnd	matlab	PyPy	Python
	mtvec:	1.27	0.79	1.00	7.78	4.53	84.69	
	smtvec:	1.25	0.89	1.00	5.72	6.56	69.43	
	rto2:	1.67	0.86	1.00	5.68	4.54	70.95	
	srto2:	1.65	0.78	1.00	4.35	13.62	73.47	
	updul:	1.37	0.68	1.00	10.88	3.07	83.71	
	supdul:	1.84	0.68	1.00	17.83	8.57	81.48
		
	Key:
	mtvec = Matrix-transpose-vector product with non-basic columns
	smtvec = Hyper-sparse matrix-transpose-vector product
	rto2 = Two-pass dual ratio test
	srto2 = Hyper-sparse two-pass dual ratio test
	updul = Update dual iterate with cost shifting
	supdul = Hyper-sparse update dual iterate with cost shifting
	C++bnd = C++ with bounds checking

### Why didn't you implement a version in SciPy?

The simplex algorithm requires some unusual sparse linear algebra operations (e.g. sparse mat-sparse vec product) that, to my knowledge, aren't provided by SciPy. The code is also difficult to vectorize, so it's unclear if there is any benefit to using numpy arrays. Submissions are welcome. 

