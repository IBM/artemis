Research project related to MCAS (https://github.com/IBM/mcas)
=======
# PyMM

PyMM is a python library that allows the storing and manipulation of existing heavily used types such as Numpy ndarray and PyTorch on Persistent Memory (e.g., Intel Optane Non-Volatile DIMMs). The key benefit of PyMM is its ability to persistently store program variables without the need to serialize or de-serialize (e.g. pickle).  Using PyMM, program variables are stored in logical groupings known as "shelves", which inherently map to different memory resources in the system.  Variables that exist on a shelf can be readily used with commonly used existing libraries including NumPy and PyTorch.

With PyMM a data type can be easily saved in Persistent Memory and directly transferred to the GPU/CPU without copying the data to DRAM. 
The advantage of PyMM means that:
- Persistency: after program or machine restarts, the data types on the shelf are immediately accessible to the program without the need to reload from a slower storage system or database.
- Capacity: support data-types that are beyond the DRAM capacity (up to 6TB ina single machine)

PyMM is implemented as a Python 3 library and CPython-based extension. The low-level index and memory management are taken from [MCAS](https://github.com/IBM/mcas) (Memory Centric Active Storage), which is a high-performance key-value store designed specifically for persistent memory and DRAM.

## Documentation

* [Overview](./info/pymm.md)
* [Examples](./examples/)


## How to Build

Update submodules
```bash
git submodule update --init --recursive
```


Run python dependencies
``` bash
./deps/install-python-deps.sh
``` 

Create Build directory
``` bash
mkdir build
cd build
``` 

Configure as debug build:

```bash
cmake -DCMAKE_BUILD_TYPE=Debug -DCMAKE_INSTALL_PREFIX:PATH=`pwd`/dist .. 
```

Build bootstrap libraries:

```bash
make bootstrap
```

Build everything else (-j optional for parallel build):

```
make -j install
```



## Verify 
```
$ python3
>>> import pymm
[--(PyMM)--] Version <current version> (CC=env)
[LOG]: Pymm extension
>>
```	

