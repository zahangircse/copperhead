### Copperhead has moved ###
Please see our new website at http://copperhead.github.com

### Introduction ###
Copperhead is a project to bring data parallelism to Python.  We define a small functional, data parallel subset of Python, which we then dynamically compile and execute on parallel platforms.  Currently, we target Nvidia GPUs, although in the future we envision supporting other platforms as well.

Here's a simple Copperhead program:
```
from copperhead import *
import numpy as np

@cu
def axpy(a, x, y):
  return [a * xi + yi for xi, yi in zip(x, y)]

x = np.arange(100, dtype=np.float64)
y = np.arange(100, dtype=np.float64)

with places.gpu0:
  gpu = axpy(2.0, x, y)

with places.here:
  cpu = axpy(2.0, x, y)
```

When `axpy` is called, the Copperhead runtime intercepts the call and compiles the function to CUDA.  It also converts the input arguments to `CuArray`s managed by the runtime, which are lazily copied to and from the execution place.  The programmer specifies the execution place using the `with` construct above: currently we support GPU execution places, as well as the Python interpreter (`places.here`), which allows for algorithm prototyping.

For more information about how Copperhead works, read our [Technical Report](http://www.eecs.berkeley.edu/Pubs/TechRpts/2010/EECS-2010-124.html).

Disclaimers: Copperhead is currently under development.  Many valid Copperhead programs do not yet compile, and the compiler does not produce helpful error messages.  Code that does compile and run may execute inefficiently, compared to hand-coded CUDA.  Join the mailing list and let us know of your experiences, but don't expect things to work right out of the box.