---
title: 示例 R 项目
description: R 和 Visual Studio 入门示例集合的索引。
ms.date: 01/24/2018
ms.topic: conceptual
author: kraigb
ms.author: kraigb
manager: jillfra
ms.workload:
- data-science
ms.openlocfilehash: ef3316d929b00203815918a656568f75571e954e
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "75843826"
---
# <a name="r-tools-for-visual-studio-sample-projects"></a>针对 Visual Studio 的 R 工具示例项目

此示例集合可助你开始使用 R、针对 Visual Studio 的 R 工具 (RTVS) 以及 Microsoft Machine Learning Server：

1. 下载[示例 zip 文件](https://github.com/Microsoft/RTVS-docs/archive/master.zip)并将其解压到选择的文件夹。
1. 打开 `examples/Examples.sln`，可看到项目中的两个文件夹：

    - “初探 R”  为 R 新用户提供简要介绍。
    - “MRS 和机器学习”举例说明如何将 R 和 Microsoft Machine Learning Server 用于机器学习  。

## <a name="a-first-look-at-r"></a>初探 R

此示例通过两个源文件中的大量注释深入介绍 R。 为获得最佳体验，请将光标置于文件顶部，然后按 Ctrl+Enter 将代码逐行发送到“R 交互”窗口  。 （用于安装包的行可能需要一两分钟来完成。）

- `1-Getting Started with R.R` 介绍了许多 R 基础知识，包括使用包、加载和分析数据以及绘图等。

    ![1-Getting Started with R.R 示例的示例输出](media/samples-getting-started-output.png)

- `2-Introduction to ggplot2.R` 引入了 ggplot2 图形包，该图形包以其极具视觉吸引力的绘图和简单的语法而著称。 此示例直观的展示斐济的地震数据。

    ![2-Introduction to ggplot2.R 示例的示例输出](media/samples-ggplot-output.png)

## <a name="microsoft-machine-learning-server-and-machine-learning"></a>Microsoft Machine Learning Server 和机器学习

此示例集合演示如何使用 R 创建机器学习模型，以及如何利用 [Microsoft Machine Learning Server](/machine-learning-server/what-is-machine-learning-server)。

与所有示例一样，请打开文件、将光标置于顶部，然后按 Ctrl+Enter 逐行单步执行代码。 每个文件夹中的 Markdown 文件还包含其他详细信息。

- `Benchmarks` 运行大量密集型的并行线性代数计算，显示使用 Microsoft R Open 和 Intel Math Kernel Library (MKL) 可能提升的性能。 通过模拟数据，基准专门将一个线程和其他两个线程上的矩阵计算进行比较。

    ![基准绘图示例](media/samples-mro-benchmark-plot.png)

- `Bike_Rental_Estimation_with_MRS` 使用 Microsoft ML Server 基于历史数据集创建单车租赁需求预测模型。

- `Data_Exploration` 包含三个脚本：

  - `Import Data from URL.R` 演示如何将 URL 标识的数据文件加载到 R 中。
  - `Import Data from URL to xdf.R` 演示如何将 URL 标识的数据文件以 xdf 的形式加载到 Microsoft ML Server。
  - `Using ggplot2.R` 是`A First Look at R/2-Introduction to ggplot2.R` 示例的扩展，它更深入地介绍了 ggplot2 的功能，包括交互式 3D 绘图。

      ![使用 ggplot2.R 示例的输出](media/samples-3d-interactive.png)

- `Datasets` 包含其他示例使用的三个 .csv 文件 
- `Flight_Delays_Prediction_with_R` 和 `Flight_Delays_Prediction_with_MRS` 演示如何使用 R 机器学习、历史实时性能和天气数据预测航班延误。
- `Machine learning` 包含三个示例，用于学习如何预测航班延迟、住房价格和自行车租金。 总体而言，这些示例演示了 R 和 Microsoft ML Server 在实际问题中的应用。 它们还演示如何使用多个热门机器学习模型，以及如何使用 [Azure 机器学习](https://azure.microsoft.com/services/machine-learning/)工作区将这些模型部署为 Azure Web 服务。

- `R_MRO_MRS_Comparison` 是一个由六部分构成的比较，展示了 R、Microsoft R Open 和 Microsoft ML Server 在命令、语法、构造和性能方面的异同。

## <a name="whats-special-about-microsoft-r-open-and-microsoft-ml-server"></a>Microsoft R Open 和 Microsoft ML Server 有什么特别之处？

[Microsoft R Open](https://mran.revolutionanalytics.com/download/) 是 Microsoft R 的分发，与 [CRAN R](https://cran.r-project.org/) 相比有两个重大差异：

1. 如果与 [Intel Math Kernel Libraries](https://software.intel.com/intel-mkl) 配合使用，可获得[更好的计算性能](https://mran.revolutionanalytics.com/rro/#intelmkl1)。 可从 Microsoft 免费下载这些库，以便与 Microsoft R Open 配合使用。

1. [可重现 R 工具包](https://mran.revolutionanalytics.com/rro/#reproducibility)，可确保用于生成 R 程序的库始终都可供想要重现操作的其他人员使用。

[Microsoft ML Server (MLS)](/machine-learning-server/what-is-machine-learning-server) 是 R 的扩展，可用于更快处理更多数据。 它为 R 赋予了两项强大的功能：

1. 数据集更大，且无 RAM 限制。 ML Server 可处理各种来源（包括 Hadoop 群集、数据库和数据仓库）中的内存不足数据。

1. 并行多核处理。 MLS 能够在可用的所有计算资源中高效分发计算。 在个人工作站或远程群集上，MLS 可更快获得答案。

以下比较显示，进行某些矩阵计算时，使用 MKL 的 MLS 和 MRO 可实现的性能明显优于不使用 MKL 的 R 和 MRO。 此计算中使用模拟数据：

![比较使用 MKL 的 MLS 和 MRO 与不使用 MKL 的 R 和 MRO](media/samples-speed-comparison.png)

有关 R 与 MRO 和 MLS 的技术比较，请参阅关于该主题的 [Lixun Zhang 详细讨论](http://htmlpreview.github.io/?https://github.com/lixzhang/R-MRO-MRS/blob/master/Introduction_to_MRO_and_MRS.html)。

下图比较生成逻辑回归模型所用的运行时间（秒），从而预测航班延误是否将超过 15 分钟。  行数的微小增加会导致 CRAN R 中的运行时间显著增加，而 MLS 的增加量仅约为行数的两倍。 有关此基准的详细信息，请参阅 Benchmarks/rxGlm_benchmark.R 示例  。

![rxGlm 基准](media/samples-rxGLM-benchmark.png)
