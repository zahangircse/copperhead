# Places #

Copperhead, being a subset of Python, allows for code prototyping in the Python interpreter.  Code execution is determined by the use of _places_.  Currently, we support only two places:
  1. The Python interpreter, which is `copperhead.places.here`
  1. The default CUDA GPU, which is `copperhead.places.gpu0`

In the future, the places mechanism will be used to support several other places, such as:
  * x86 multi-core
  * Individual GPUs in a multi-GPU system
  * A multi-GPU place, which will distribute execution across multiple GPU sockets

# Execution #

Execution is explicitly controlled for blocks of code using the `with` statement:
```
with places.gpu0:
  pass
```

The default execution place is places.gpu0

# Data #
Data is managed by the Copperhead runtime through the `CuArray` class, which keeps a local copy of the data in the Python interpreter, as well as a remote copy of the data intended for use at a particular place.  Data is moved between places lazily.



