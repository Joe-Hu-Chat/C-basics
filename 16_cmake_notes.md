CMake is a cross-platform build system generator that facilitates the building, testing, and packaging of software.

Example `CMakeLists.txt`
```cmake
cmake_minimum_required(VERSION 3.10)
project(HelloWorld)

add_executable(HelloWorld helloworld.cpp)

```



Building with CMake

1. Create a Build Directory

```bash
mkdir build
cd build
```

2. Run CMake

```bash
cmake ..
```

3. Build the Project

```bash
cmake --build .
```



Toolchain File:

A toolchain file is a CMake script that specifies various variables related to the build environment, such as:

- Compiler paths
- Target platform information
- Library and include paths





A CMake toolchain file example:

```cmake
set(CAMEK_FIND_ROOT_PATH "/opt/riscv64-lp64d/bin")
set(CMAKE_C_COMPILER "riscv64-unknown-linux-gnu-gcc")
set(CMAKE_CXX_COMPILER "riscv64-unknown-linux-gnu-g++")
set(CMAKE_SYSTEM_NAME Linux)
set(CMAKE_SYSTEM_PROCESSOR riscv64)
set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -march=rv64imafdc -mabi=lp64")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -march=rv64imafdc -mabi=lp64")
```



Configuration options:

```bash
# initial configuration
cmake ../opencv
 
# print all options
cmake -L
 
# print all options with help message
cmake -LH
 
# print all options including advanced
cmake -LA
```

Most popular and useful are options starting with `WITH_`, `ENABLE_`, `BUILD_`, `OPENCV_`.
