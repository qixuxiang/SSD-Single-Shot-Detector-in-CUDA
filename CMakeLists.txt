cmake_minimum_required(VERSION 3.2)
project(ssd_cuda)

find_package(CUDA REQUIRED)
include_directories(${CUDA_INCLUDE_DIRS})
SET(CMAKE_C_COMPILER "/usr/bin/gcc-5")

SET(CMAKE_CXX_COMPILER "/usr/bin/g++-5")
set(CMAKE_C_STANDARD 11)
add_definitions(-std=c++11)

CUDA_ADD_EXECUTABLE(Main Main.h Main.cpp DNNLIB.h DNNLIB.cpp kernel.cu)  

# C++ list
LIST(APPEND CMAKE_CXX_FLAGS "-std=c++11 -O3 -ffast-math -Wall")

# CUDA list
LIST(APPEND CUDA_NVCC_FLAGS --compiler-options -fno-strict-aliasing -lineinfo -use_fast_math -Xptxas -dlcm=cg)
LIST(APPEND CUDA_NVCC_FLAGS --compiler-options -use_fast_math)
LIST(APPEND CUDA_NVCC_FLAGS -gencode arch=compute_35,code=sm_35)   
LIST(APPEND CUDA_NVCC_FLAGS -gencode arch=compute_50,code=sm_50) 
LIST(APPEND CUDA_NVCC_FLAGS -gencode arch=compute_61,code=sm_61)


