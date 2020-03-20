---
title: 在本地训练 tensorflow 模型
description: 在 AI Tools for Visual Studio 中以本地方式运行 tensorflow 模型
keywords: ai, visual studio, tensorflow, 本地
author: lisawong19
ms.author: liwong
manager: routlaw
ms.date: 11/13/2017
ms.topic: quickstart
ms.devlang: python
ms.workload:
- multiple
ms.openlocfilehash: 43ce126baeb96efcaab3c40bac912274ee1cd8c7
ms.sourcegitcommit: 2975d722a6d6e45f7887b05e9b526e91cffb0bcf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/20/2020
ms.locfileid: "72777435"
---
# <a name="train-a-tensorflow-model-locally"></a>在本地训练 TensorFlow 模型

在本快速入门中，我们会在 Visual Studio Tools for AI 中以本地方式使用 [MNIST](http://yann.lecun.com/exdb/mnist/) 数据集训练 TensorFlow 模型。

MNIST 数据库具有包含 60,000 个示例的训练集，以及包含 10,000 个手写数字示例的测试集。

## <a name="prerequisites"></a>系统必备

开始之前，确保安装了以下各项：

### <a name="google-tensorflow"></a>Google TensorFlow

在终端中运行以下命令：

```cmd
C:\>pip.exe install tensorflow
```

### <a name="numpy-and-scipy"></a>NumPy 和 SciPy
安装 [NumPy](https://www.lfd.uci.edu/~gohlke/pythonlibs/#numpy) 和 [SciPy](https://www.lfd.uci.edu/~gohlke/pythonlibs/#scipy)。

### <a name="download-sample-code"></a>下载示例代码
下载包含示例的此 [GitHub 存储库](https://github.com/Microsoft/samples-for-ai)，以便开始在 TensorFlow、CNTK、Theano 等工具中进行深入学习。

## <a name="open-solution-and-train-model"></a>打开解决方案并训练模型

- 启动 Visual Studio，选择“文件”>“打开”>“项目/解决方案”。

- 在下载的示例存储库中选择 Tensorflow Examples 文件夹，然后打开 TensorflowExamples.sln 文件。

   ![打开项目](media/tensorflow-local/open-project.png)

   ![打开解决方案](media/tensorflow-local/open-solution.png)

- 在“解决方案资源管理器”中找到 MNIST 项目，右键单击并选择“设为启动项目”。

- 单击“开始” 。

- 输出会在控制台中进行打印。

   ![控制台的示例输出](media/tensorflow-local/console-output.png)

> [!div class="nextstepaction"]
> [在云中训练 TensorFlow 模型](tensorflow-vm.md)
