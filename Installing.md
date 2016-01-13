# Introduction #
Copperhead depends on a number of software packages:
  * Python 2.6 or 2.7
  * [CUDA](http://nvidia.com/cuda) 4.1 or better
  * Numpy 1.30 or better
  * Boost 1.38 or better
    * Only the boost\_python library is required
  * [CodePy](http://mathema.tician.de/software/codepy) 2012.1.1 or better
  * [Thrust](http://code.google.com/p/thrust) 1.2 or better

In addition, to build Copperhead, you will need
  * g++ 4.5
  * http://scons.org Scons (we tested with 2.0.0)

# Installation #
Copperhead has been tested on Python 2.6 & Python 2.7.  We'll consider moving to Python 3.x after Numpy moves.  Copperhead works on Linux and OS X.  Windows support will come in the future.

Currently, Copperhead has only one backend: a CUDA backend targeting Nvidia GPUs, although we hope to support other platforms in the future.  The CUDA backend requires the presence of a CUDA capable GPU, running CUDA 4.1 or better.  Install CUDA from Nvidia's webpage, and make sure you can compile and run CUDA programs before proceeding with the installation.  CUDA 4.1 includes Thrust, so separate installation is not necessary.

Copperhead uses CodePy for managing execution of C++ code on the host.  CodePy will be installed automatically during the setup process, so separate installation is not necessary.

Copperhead uses boost::python for binding C++ code to Python. You must build the boost\_python library before installing Copperhead. Note: it is imperative that your boost\_python library be built with the same compiler that your Python installation was built with.  For many Linux systems, it is probably best to install boost\_python from your package manager.  For example, on Ubuntu,
```
sudo apt-get install libboost-python-dev
```
will install the headers and a compatible library.

Once all these packages are in place, download Copperhead.

If your boost\_python headers and library are not installed in default locations, you will need to create a small file to direct the build process:
Please create a file named `siteconf.py` in the top directory, alongside `setup.py`.  In this file, describe your boost installation.  For example:
```
#!/usr/bin/python
BOOST_INC_DIR = "/home/username/boost_1_48_0"
BOOST_LIB_DIR = "/home/username/boost_1_48_0/stage/lib"
BOOST_PYTHON_LIBNAME = "boost_python"
```

The BOOST\_PYTHON\_LIBNAME variable should hold the name of the library that
you would pass to the linker if you were linking. On Linux, for example,
if the filename of the library is libboost\_python-gcc43.so, you would write
`BOOST_PYTHON_LIBNAME = "boost_python-gcc43"`

Running
```
python setup.py install
```

will install Copperhead in your python.  Like all Python packages, you will either need to install in a virtualenv or have root privileges and install in your system Python.  Once that's done, run the tests:

```
python tests/test_all.py
```