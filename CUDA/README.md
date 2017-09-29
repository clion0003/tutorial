# 从0开始学习cuda和caffe源码阅读
## 0. CUDA的安装和caffe的安装
> CUDA is a parallel computing platform and application programming interface (API) model created by Nvidia. -[ 维基百科 ](https://en.wikipedia.org/wiki/CUDA)

CUDA是使用**NVIDIA**显卡进行并行运算的一种方式，目前经常被用于加速深度学习。

CUDA安装相关文档：http://docs.nvidia.com/cuda/cuda-quick-start-guide/index.html。

在CUDA安装完毕以后，CUDA会生成CUDA samples，这些是CUDA的一些例子，windows默认目录在C:\ProgramData\NVIDIA Corporation\CUDA Samples。ubuntu和mac下设置完环境变量以后，可以使用cuda-install-samples-8.0.sh(8.0版本的cuda)来安装例子。

> Caffe is a deep learning framework, originally developed at UC Berkeley. It is open source, under a BSD license. It is written in C++, with a Python interface. -[ 维基百科 ](https://en.wikipedia.org/wiki/Caffe_(software))

caffe是目前比较火的**深度学习加速框架**，主要采用了CUDA进行加速。

caffe官网：http://caffe.berkeleyvision.org/

caffe安装：http://caffe.berkeleyvision.org/installation.html

建议在ubuntu下使用caffe，因为可以直接apt-get：sudo apt install caffe-cuda

##  1.初学CUDA
**学习文档：**

http://docs.nvidia.com/cuda/cuda-c-programming-guide/index.html

   主要介绍了CUDA的编程模式，和基本的GPU架构

**推荐书单：**
大规模并行处理器编程实战(Programming Massively Parallel Processors: A Hands-on Approach) 1-6章

CUDA并行程序设计:GPU编程指南（CUDA Parallel Programming: GPU Programming Guide）

**推荐公开课：**
https://developer.nvidia.com/educators/existing-courses#2

**推荐阅读源码：**
在cuda目录下的，0_simple/matrixMul, vectorAdd, simpleStreams, simpleTemplates, simpleZeroCopy, UnifiedMemoryStreams, simpleMultiCopy

**阶段目标：**基本理解GPU的运算方式，能用CUDA写出一些简单的运算，了解GPU和CPU之间memory的拷贝方式，了解GPU的global memory，shared memory的区别和使用方式，了解CUDA stream。

## 2.深入了解CUDA
**学习文档：**
http://docs.nvidia.com/cuda/cuda-c-best-practices-guide/index.html

**推荐书单：**
: 大规模并行处理器编程实战(Programming Massively Parallel Processors: A Hands-on Approach) 7-20章
: CUDA范例精简（CUDA by Example）
: GPU高性能编程CUDA实战（ CUDA by Example: an Introduction to General-Purpose GPU Programming）

注：以上书单都是通过具体的例子来阐述GPU优化的方式，阅读一本即可，内容大同小异。

**推荐源码阅读：** 3_Imaging和4_Finace目录下的所有例子，可以挑自己感兴趣的算法进行选取和阅读。

**阶段目标：**
了解GPU的运作方式，理解tiled-based优化方法，理解GPU中各个参数对程序运行效率的影响，理解GPU在面对分支操作时的运行方式。

## 3.使用已有的CUDA加速库
**学习文档：**
: Cublas: http://docs.nvidia.com/cuda/cublas/index.html
: Curand: http://docs.nvidia.com/cuda/curand/index.html
: Cusparse: http://docs.nvidia.com/cuda/cusparse/index.html
: Thrust: http://docs.nvidia.com/cuda/thrust/index.html
: CuDNN: http://docs.nvidia.com/deeplearning/sdk/index.html

**推荐源码阅读：**
0_simple/matrixMulCUBLAS, 7_CUDALibraries下部分代码
Caffe源码（主要是用了Cublas和CuDNN两个库）

**阶段目标：**学会阅读NVIDIA关于加速库的文档，学会使用这些库（尤其是Cublas和CuDNN）的API调用，能够比较速度

## 4.学会使用工具分析CUDA程序性能
**学习文档：**
http://docs.nvidia.com/cuda/profiler-users-guide/index.html

nvprofiler是一个非常好的，拥有图形界面的profile工具，使用起来也非常方便，在ubuntu下只需要nvprof ./[exec]的形式就能进行简单的性能分析，复杂的性能分析需要借助nsight软件进行分析。

**阶段目标：**学会使用nvprof工具分析cuda程序的性能，能够观察到kernel的运行时间轴，分析cache miss/hit率，明白cuda程序的瓶颈所在，是运算密集型还是访存密集型，访存上cache的hit率能不能进一步提高，等等。

## 5.使用内嵌汇编指令对CUDA程序进行优化*
**学习文档：**
http://docs.nvidia.com/cuda/parallel-thread-execution/index.html

**推荐源码阅读：**
0_simple/inlinePTX，以及各种程序在nvcc编译时加入--keep字段，程序将会保留ptx指令*.ptx

**阶段目标：**
理解汇编程序在GPU上的运行方式，学会写内嵌PTX程序。用PTX指令进行优化

## 6.Caffe源码分析和阅读

cafe主要的计算部分的源码位置为：
https://github.com/BVLC/caffe/tree/master/src/caffe/layers

caffe源码分析未完待续

