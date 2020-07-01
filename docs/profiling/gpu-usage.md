---
title: GPU 使用情况 | Microsoft Docs
ms.date: 11/01/2018
ms.topic: conceptual
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 6aa4cce032a5eb80a11568a83c1166b5690bd688
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/23/2020
ms.locfileid: "85279870"
---
# <a name="gpu-usage"></a>GPU 使用情况

使用 Visual Studio 性能和诊断中心内的 GPU 使用情况工具，更好地概览 Direct3D 应用的硬件使用情况。 它有助于查看应用的性能是受限于 CPU 还是 GPU，并深入了解如何更有效地使用平台的硬件。 GPU 使用情况工具支持使用 Direct3D 12、Direct3D 11 和 Direct3D 10 的应用。 它不支持其他图形 API（如 Direct2D 或 OpenGL）。

“GPU 使用情况报告”窗口如下所示：

![内含 CPU 和 GPU 时间线的“GPU 使用情况报告”屏幕截图](media/gfx_diag_gpu_usage_report.png "gfx_diag_gpu_usage_report")

## <a name="requirements"></a>要求

除了图形诊断要求外，使用 GPU 使用情况工具还必须满足以下要求：

- 支持必要计时规范的 GPU 和驱动程序。

  > [!NOTE]
  > 有关支持的硬件和驱动程序的详细信息，请参阅本文档末尾的[硬件和驱动程序支持](#hwsupport)。

若要详细了解图形诊断要求，请参阅[入门](../debugger/graphics/getting-started-with-visual-studio-graphics-diagnostics.md)。

## <a name="use-the-gpu-usage-tool"></a>使用 GPU 使用情况工具

当你在 GPU 使用情况工具下运行应用时，Visual Studio 会创建一个诊断会话。 此会话以图形方式实时提供有关应用的呈现性能和 GPU 使用情况的概览信息。

启动 GPU 使用情况工具：

1. 在主菜单上，依次选择“调试” > “性能和诊断”（或者，在键盘上按 Alt+F2）。

2. 在“性能和诊断”中心内，选中“GPU 使用情况”旁边的复选框。 （可选）选中你希望使用的其他工具旁的复选框。 可同时运行多个性能和诊断工具，以更全面地了解应用性能。

    ![“性能和诊断”中心的屏幕截图（已选中“GPU 使用情况”）](media/gpuusageselected.png "已选中“GPU 使用情况”")

   > [!NOTE]
   > 并非所有性能和诊断工具都可以同时使用。

3. 选择“性能和诊断”中心底部的“启动”，以在所选工具下运行应用。

实时显示的概览信息包括帧时间、帧速率和 GPU 使用情况。 每条信息都是独立绘制的，但它们都使用一个通用的时间范围，因此你可以很容易地理解它们之间的关系。

“帧时间(毫秒)”和“每秒帧数(FPS)”图都有两条红色水平线，表示每秒 60 帧和 30 帧的性能目标。 在“帧时间”图中，图低于红线表示应用超过性能目标，高于红线表示未达到性能目标。 对于“每秒帧数”图，情况正好相反：图高于红线表示应用超过性能目标，低于红线表示未达到性能目标。 使用这些图主要是为了对应用性能有一个大概的了解，并发现可能需要调查的减速情况。 例如，如果看到帧速率突然下降或 GPU 利用率突然上升，进一步调查可能是必要的。

当应用在 GPU 使用情况工具下运行时，诊断会话还收集关于在 GPU 上运行的图形事件的详细信息。 此信息用于生成有关应用如何利用硬件的更细致报告。 由于从收集的信息生成此报告需要一些时间，因此仅当诊断会话完成信息收集之后此报告才可用。

若要进一步了解性能或利用率问题，请停止收集性能信息，以便能够生成报告。

若要生成和查看 GPU 使用情况报告，请执行以下操作：

1. 选择“诊断会话”窗口底部的“停止收集”链接，或选择左上角的“停止”。

   ![“诊断会话”窗口的屏幕截图](media/gfx_diag_gpu_usage_collect.png "gfx_diag_gpu_usage_collect")

2. 在报告的顶部，从显示要调查问题的图形中选择一个。 最长可选择 3 秒。 如果选择的部分较长，则会在开头处截断。

   ![“诊断会话”窗口的屏幕截图](media/gfx_diag_gpu_usage_select1.png "gfx_diag_gpu_usage_select1")

3. 若要查看所选部分的详细时间线，请选择报告底部“...单击此处查看此范围内的 GPU 使用情况详细信息”消息中的“查看详细信息”。

   ![“诊断会话”窗口的屏幕截图（已选择范围）](media/gfx_diag_gpu_usage_select2.png "gfx_diag_gpu_usage_select2")

此选择会打开一个包含该报表的新标签页式文档。 GPU 使用情况报告有助于了解图形事件何时在 CPU 上启动、何时到达 GPU，以及 GPU 运行它需要多长时间。 此信息可以帮助你确定瓶颈和机遇，以提高代码的并行度。

<!-- VERSIONLESS -->
## <a name="export-to-gpuview-or-windows-performance-analyzer"></a>导出到 GPUView 或 Windows Performance Analyzer

自 Visual Studio 2017 起，你可以使用 [GPUView](/windows-hardware/drivers/display/using-gpuview) 和 [Windows Performance Analyzer](/windows-hardware/test/wpt/windows-performance-analyzer) 来打开此数据。 只需选择“诊断会话”窗口右下角的“在 GpuView 中打开”或“在 WPA 中打开”链接即可。

![“诊断会话”窗口的屏幕截图（突出显示了链接）](media/gfx_diag_open_in.png)
<!-- /VERSIONLESS -->

## <a name="use-the-gpu-usage-report"></a>使用 GPU 使用情况报告

GPU 使用情况报告的上半部分显示了 CPU 处理活动、GPU 呈现活动和 GPU 复制活动的时间线。 这些时间线由表示显示器垂直同步的浅灰色竖线分隔。 竖线的频率与从中收集 GPU 使用情况数据的显示器之一（使用“显示器”下拉列表选择）的刷新频率一致。

由于显示器的刷新率可能高于应用的性能目标，因此垂直同步与你希望达到的帧速率不一定具有一一对应关系。 为了达到性能目标，应用必须完成所有处理、执行呈现，并以目标帧速率执行 `Present()` 调用。 不过，已呈现的帧直到 `Present()` 后的下一次垂直同步才会显示。

GPU 使用情况报告的下半部分列出了在报告期间发生的图形事件。 当你选择事件时，标记会出现在相关时间线中的相应事件上。 通常，CPU 线程上的一个事件显示 API 调用，某个 GPU 时间线上的另一个事件显示 GPU 何时完成了任务。 同样，当你在时间线中选择事件时，报告会在报告的下半部分突出显示相应的图形事件。

当你在报告的上半部分缩小时间线时，只有最耗时的事件才可见。 若要查看持续时间更短的事件，请放大时间线，具体方法为使用指针设备上的 Ctrl+滚轮，或使用上半部分面板左下角的缩放控件。 还可以拖动时间线面板中的内容，浏览记录的事件。

为了有助于查找所需的内容，请根据进程名称、线程 ID 和事件名称来筛选 GPU 使用情况报告。 此外，可以选择确定垂直同步线的显示器刷新率。 如果应用使用 [ ID3DUserDefinedAnnotation](/windows/desktop/api/d3d11_1/nn-d3d11_1-id3duserdefinedannotation) 接口对呈现命令进行分组，则可以分层次地对事件进行排序。

 以下是更多详细信息：

|筛选器控件|描述|
|--------------------|-----------------|
|**Process**|关注的进程的名称。 所有在诊断会话期间使用 GPU 的进程都包括在此下拉列表中。 与此进程相关联的颜色是时间线中线程活动的颜色。|
|**线程**|关注的线程 ID。 在多线程应用中，此信息有助于隔离属于你感兴趣的进程的特定线程。 与所选线程关联的事件在每条时间线中突出显示。|
|**显示**|显示其刷新频率的显示器的编号。 可以配置某些驱动程序，以便将多个物理显示器显示为单个较大的虚拟显示器。 即使计算机连接了多个显示器，也可能仅列出一个。|
|**筛选器**|关注的关键字。 报告的下半部分中只包括与关键字完全匹配或部分匹配的事件。 你可以指定多个关键字并用分号 (;) 隔开。|
|**层次结构排序**|复选框，指明是保留还是忽略通过用户标记定义的事件层次结构。|

GPU 使用情况报告下半部分中的事件列表显示了每个事件的详细信息。

|列|描述|
|------------|-----------------|
|**事件名称**|图形事件的名称。 事件通常对应于 CPU 线程时间线中的事件和 GPU 时间线事件。 如果 GPU 使用情况工具无法确定事件名称，则事件名称可能为“未归因”。 有关详细信息，请参阅此表后面的备注。|
|**CPU 启动(纳秒)**|通过调用 Direct3D API 在 CPU 上启动事件的时间。 时间以纳秒计，与应用的启动时间相关。|
|**GPU 启动(纳秒)**|在 GPU 上启动事件的时间。 时间以纳秒计，与应用的启动时间相关。|
|**GPU 持续时间(纳秒)**|在 GPU 上完成事件所用的时间（以纳秒为单位）。|
|**进程名**|事件源于的应用的名称。|
|**线程 ID**|事件源于的线程 ID。|

> [!IMPORTANT]
> 如果 GPU 或驱动程序不支持必要的检测功能，则所有事件都显示为“未归因”。 如果遇到此问题，请更新 GPU 驱动程序，然后重试。 有关详细信息，请参阅本文档末尾的[硬件和驱动程序支持](#hwsupport)。

## <a name="gpu-usage-settings"></a>GPU 使用情况设置

你可以将 GPU 使用情况工具配置为推迟收集分析信息，而不在应用启动后立即开始收集信息。 由于分析信息可能非常大，因此当你知道应用性能暂时不会降速时，此操作将很有用。

从应用的开头推迟分析：

1. 在主菜单上，依次选择“调试” > “性能和诊断”（或者，在键盘上按 Alt+F2）。

2. 在“性能和诊断”中心内，选择“GPU 使用情况”旁边的“设置”链接。

3. 在“常规”属性页上的“GPU 分析配置”下，取消选中“在应用启动时开始分析”复选框，以推迟分析。

   ![显示收集选项的“对象属性页”的屏幕截图](media/gfx_diag_gpu_usage_config.png "gfx_diag_gpu_usage_config")

> [!IMPORTANT]
> 暂无法推迟对 Direct3D 12 应用的分析。

在 GPU 使用情况工具下运行应用后，GPU 使用情况工具窗口底部会出现一个可用的额外链接。 若要开始收集分析信息，请选择“开始收集更多详细 GPU 使用情况数据”消息中的“启动”链接。

## <a name="hardware-and-driver-support"></a><a name="hwsupport"></a>硬件和驱动程序支持

支持以下 GPU 硬件和驱动程序：

|Vendor|GPU 说明|要求的驱动程序版本|
|------------|---------------------|-----------------------------|
|Intel®|第四代 Intel® 酷睿处理器（“Haswell”）<br /><br /> -   Intel® HD Graphics (GT1)<br />-   Intel® HD Graphics 4200 (GT2)<br />-   Intel® HD Graphics 4400 (GT2)<br />-   Intel® HD Graphics 4600 (GT2)<br />-   Intel® HD Graphics P4600 (GT2)<br />-   Intel® HD Graphics P4700 (GT2)<br />-   Intel® HD Graphics 5000 (GT3)<br />-   Intel® Iris™ Graphics 5100 (GT3)<br />-   Intel® Iris™ Pro Graphics 5200 (GT3e)|（使用最新驱动程序）|
|AMD®|AMD Radeon™ HD 7000 系列之后的大多数产品（AMD Radeon™ HD 7350-7670 除外）<br /><br /> 具有 Graphics Core Next (GCN) 体系结构的 AMD Radeon™ GPU、AMD FirePro™ GPU 和 AMD FirePro GPU 加速器<br /><br /> 具有 Graphics Core Next (GCN) 体系结构的 AMD® E 系列和 AMD A 系列加速处理单元 (APU)（“Kaveri”、“Kabini”、“Temash”、“Beema”、“Mullins”）|14.7 RC3 或更高版本|
|NVIDIA®|NVIDIA® GeForce® 400 系列之后的大多数产品<br /><br /> 具有 Fermi™、Kepler™ 或 Maxwell™ 体系结构的 NVIDIA® GeForce® GPU、NVIDIA Quadro® GPU 和 NVIDIA® Tesla™ GPU 加速器|343.37 或更高版本|

 暂不支持 NVIDIA® SLI™ 和 AMD Crossfire™ 等多 GPU 配置。 支持 VIDIA® Optimus™ 和 AMD Enduro™ 等混合图形设置。
