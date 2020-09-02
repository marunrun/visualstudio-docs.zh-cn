---
title: 安装 Visual Studio Tools for AI
description: 介绍了如何安装 Visual Studio Tools for AI
keywords: ai, visual studio
author: jillre
ms.author: jillfra
manager: jillfra
monikerRange: vs-2017
ms.date: 11/13/2017
ms.topic: conceptual
ms.workload:
- multiple
ms.openlocfilehash: ffa8c7634c0d97dd24ff69814ae73ad5ff12928b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "88800198"
---
# <a name="installation"></a>安装

可以在 Windows 64 位操作系统上安装 Visual Studio Tools for AI。

## <a name="install-visual-studio-tools-for-ai"></a>安装 Visual Studio Tools for AI

此扩展适用于 Visual Studio 2015、Visual Studio 2017、社区版或更高版本。

可以从 [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=ms-toolsai.vstoolsai-vs2017) 或 Visual Studio 中下载工具：

1. 依次选择“工具”   > “扩展和更新”  。

   ![Visual Studio 中的“扩展和更新”菜单](media/installation/extensions.png)

2. 在“扩展和更新”  对话框的左侧，选择“联机”  。
3. 在右上角的搜索框中，键入或输入“tools for ai”。
4. 从结果中选择“Visual Studio Tools for AI”  。
5. 选择“下载”。

## <a name="prepare-your-local-machine"></a>准备本地计算机
在本地计算机上定型深度学习模型前，请先确保已安装适用的先决条件工具。 这包括确保已安装 NVIDIA GPU（若有）的最新驱动程序和库。 还要确保已安装 Python 和 Python 库（如 NumPy、SciPy），以及你打算在项目中使用的相应深度学习框架（如 Microsoft Cognitive Toolkit (CNTK)、TensorFlow、Caffe2、MXNet、Keras、Theano、PyTorch 和 Chainer）。

> [!NOTE]
> 以下各小节中的软件简介摘自其主页。

### <a name="nvidia-gpu-driver"></a>NVIDIA GPU 驱动程序

深入学习框架利用 NVIDIA GPU 让机器按照针对真实人工智能的速度、准确性和规模进行学习。 如果计算机具有 NVIDIA GPU 卡，请参阅 [NVIDIA 驱动程序下载](https://www.nvidia.com/Download/index.aspx)或尝试更新操作系统以安装最新驱动程序。

### <a name="cuda"></a>CUDA

[CUDA](https://developer.nvidia.com/cuda-zone) 是 NVIDIA 发明的并行计算平台和编程模型。 它利用 GPU 的强大功能显著提高了计算性能。 当前，深入学习框架需要 CUDA 工具包 8.0。

安装 CUDA

- 访问此[站点](https://developer.nvidia.com/cuda-80-ga2-download-archive)，下载 CUDA 并安装它。
- 确保安装 CUDA 运行时库，然后将 CUDA 二进制文件路径添加到 %PATH% 或 $Path 环境变量。
- 在 Windows 上，此路径在默认情况下为“C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v8.0\bin”。

![在 Windows 上安装 CUDA](media/installation/install_cuda_win.png)

### <a name="cudnn"></a>cuDNN

[cuDNN](https://developer.nvidia.com/cudnn)（CUDA 深层神经网络库）是 NVIDIA 提供的深层神经网络基元的 GPU 加速库。 最新深入学习框架需要 cuDNN v6。

安装 cuDNN：

- 请访问 [NVIDIA 开发人员](https://developer.nvidia.com/rdp/cudnn-download)，下载并安装最新的包。
- 确保将包含 cuDNN 二进制文件的目录添加到 %PATH% 或 $Path 环境变量。
- 在 Windows 上，可以将 cudnn64_6.dll 复制到“C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v8.0\bin”。

> [!NOTE]
> 以前的深入学习框架（如 CNTK 2.0 和 TensorFlow 1.2.1）需要 cuDNN v5.1。 但是，可以一起安装多个 cuDNN 版本。

### <a name="python"></a>Python

Python 已成为用于深入学习应用程序的主要编程语言。 需要 **64 位** Python 分发版，推荐使用 [Python 3.5.4](https://www.python.org/downloads/release/python-354/) 以实现最佳兼容性。

### <a name="to-install-python-on-windows"></a>在 Windows 上安装 Python

- 建议只为你安装 Python 启动器，并将 Python 添加到 %PATH% 环境变量。
- 确保安装 pip，这是用于安装和管理采用 Python 编写的软件程序包的程序包管理系统。

深入学习框架依靠 pip 进行自己的安装。

![在 Windows 上安装 Python](media/installation/install_python_win.png)

随后需要验证是否正确安装了 Python 3.5 并将 pip 升级到最新版本，具体方法是在终端中执行以下命令：

- **Windows**

  ```cmd
  C:\Users\test>python -V
  Python 3.5.4

  C:\Users\test>pip3.5 -V
  pip 9.0.1 from c:\users\test\appdata\local\programs\python\python35\lib\site-packages (python 3.5)

  C:\Users\test>python -m pip install -U pip
  ```

- **macOS**

  ```bash
  MyMac:~ test$ python3.5 -V
  Python 3.5.4

  MyMac:~ test$ pip3.5 -V
  pip 9.0.1 from /Library/Frameworks/Python.framework/Versions/3.5/lib/python3.5/site-packages (python 3.5)

  MyMac:~ test$ python3.5 -m pip install -U pip
  ```

### <a name="python-on-visual-studio"></a>Visual Studio 中的 Python

在 Visual Studio 中通过扩展完全支持 Python。
详细了解如何安装 [Python for Visual Studio Tools](../python/installing-python-support-in-visual-studio.md) 以获得详细信息。

### <a name="numpy-and-scipy"></a>NumPy 和 SciPy

- **NumPy** 是一种通用数组处理程序包，旨在高效地操作任意记录的大型多维数组，而不会对小型多维数组降低太多速度。

- **SciPy**（发音为“Sigh Pie”）是用于数学、科学和工程（具体取决于 NumPy）的开放源代码软件。 从版本 1.0.0 开始，SciPy 现在具有适用于 Windows 的官方预生成滚轮软件包。

若要安装 NumPy 和 SciPy，请在终端中运行以下命令：

```bash
pip3.5 install -U numpy scipy
```

> [!NOTE]
> 上面的命令会将现有旧的或非官方（例如适用于 Windows 的来自 http://www.lfd.uci.edu/~gohlke/pythonlibs/ 的第三方程序包）NumPy 和 SciPy 升级到最新官方版本。

### <a name="microsoft-cognitive-toolkit-cntk"></a>Microsoft 认知工具包 (CNTK)

[Microsoft 认知工具包](https://cntk.ai)是一种统一深入学习工具包，可通过定向关系图将神经网络描述为一系列计算步骤。 CNTK 支持 Python 和 BrainScript 编程语言。

> [!NOTE]
> CNTK 当前不支持 macOS。

若要安装 CNTK Python 包，请参阅[如何安装 CNTK](/cognitive-toolkit/Setup-CNTK-on-your-machine)。

### <a name="tensorflow"></a>TensorFlow

[TensorFlow](https://www.tensorflow.org/) 是使用数据流关系图的数值计算的开放源代码软件库。 有关详细安装，请参阅[此处](https://www.tensorflow.org/install/)。

> [!NOTE]
> 从版本 1.2 开始，TensorFlow 不再为 macOS 提供 GPU 支持。

### <a name="caffe2"></a>Caffe2

[Caffe2](https://caffe2.ai/) 是轻型模块化的可缩放深入学习框架。 Caffe2 在原始 Caffe 的基础上构建，在设计时考虑了表达式、速度和模块性。

当前没有预生成的 Caffe2 python 滚轮程序包可用。

访问[此处](https://caffe2.ai/docs/getting-started.html)可通过源代码进行生成。

### <a name="mxnet"></a>MXNet

[Apache MXNet（孵化中）](https://mxnet.incubator.apache.org/)是旨在提高效率和灵活性的深入学习框架。 通过它，你可混用[符号和命令式编程](http://mxnet.io/architecture/index.html#deep-learning-system-design-concepts)，从而最大程度地提高效率和生产力  。

若要安装 MXNet，请在终端中运行以下命令：

- 具有 GPU

  ```bash
  pip3.5 install mxnet-cu80==0.12.0
  ```

- 没有 GPU

  ```bash
  pip3.5 install mxnet==0.12.0
  ```

### <a name="keras"></a>Keras

[Keras](https://keras.io/) 是一种高级神经网络 API，采用 Python 编写，能够在 CNTK、TensorFlow 或 Theano 上运行。 它在开发时侧重于实现快速实验。 能够在延迟尽可能少的情况下从想法到获得结果是做好研究的关键。

若要安装 Keras，请在终端中运行以下命令：

```bash
pip3.5 install Keras==2.0.9
```

### <a name="theano"></a>Theano

[Theano](http://deeplearning.net/software/theano/) 是一种 Python 库，可用于高效地定义、优化和计算涉及多维数组的数学表达式。

若要安装 Theano，请在终端中运行以下命令：

```bash
pip3.5 install Theano==0.9.0
```

### <a name="pytorch"></a>PyTorch

[PyTorch](https://pytorch.org/) 是一种 python 程序包，提供两个高级功能：

- 具有强 GPU 加速的 Tensor 计算（如 numpy）
- 在基于磁带的自动梯度系统上构建的深层神经网络

若要安装 PyTorch，请在终端中运行以下命令：

- **Windows**

  尚没有官方滚轮程序包。 从 [Anaconda](https://anaconda.org/pytorch/repo?type=all) 或[加利福尼亚大学](https://www.lfd.uci.edu/~gohlke/pythonlibs/#pytorch)可以下载第三方程序包。

  - 将它解压缩到主目录，例如 C:\Users\test\pytorch  。
  - 将 C:\Users\test\pytorch\Lib\site-packages 添加到 %PYTHONPATH% 环境变量  。

    ```bash
    pip3 install http://download.pytorch.org/whl/cu80/torch-0.4.0-cp36-cp36m-win_amd64.whl
    pip3 install torchvision
    ```

- **macOS**

  ```bash
  pip3.5 install http://download.pytorch.org/whl/torch-0.2.0.post3-cp35-cp35m-macosx_10_7_x86_64.whl
  ```

  > [!NOTE]
  > macOS 二进制文件不支持 CUDA，如果需要 CUDA，请从源提供程序进行安装

- **Linux**

  ```bash
  pip3.5 install http://download.pytorch.org/whl/cu80/torch-0.2.0.post3-cp35-cp35m-manylinux1_x86_64.whl
  ```

  > [!NOTE]
  > 此单个程序包支持 GPU 和 CPU。

最后，在非 Windows 上安装 torchvision：

```bash
pip3.5 install torchvision
```

### <a name="chainer"></a>Chainer

[Chainer](https://chainer.org/) 是旨在提高灵活性的基于 Python 的深入学习框架。 它提供基于通过运行定义方法（也称为动态计算图）的自动差异化 API 以及面向对象的高级 API 来构建和训练神经网络。

若要启用 CUDA 支持，请安装 [CuPy](https://github.com/cupy/cupy)：

```bash
pip3.5 install cupy
```

> [!NOTE]
> 在 Windows 上，需要 2015 版本的 [Visual Studio](https://visualstudio.microsoft.com/) 或 [Microsoft Visual C++ 生成工具](https://visualstudio.microsoft.com/visual-cpp-build-tools/)来使用 CUDA 8.0 编译 CuPy。

若要安装 Chainer，请在终端中运行以下命令：

```bash
pip3.5 install chainer==3.0.0
```
