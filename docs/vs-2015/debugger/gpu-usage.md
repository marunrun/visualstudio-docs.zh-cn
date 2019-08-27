---
title: GPU 使用情况 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: 957fed3c-4ded-4e05-87c6-ccc33de65349
caps.latest.revision: 7
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: b7dee579f726a1edfc81e1f3e1ec62bf7d8beba4
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63437959"
---
# <a name="gpu-usage"></a>GPU 使用情况
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在 Visual Studio 性能和诊断中心使用 GPU 使用情况工具，更好地了解你 Direct3D 应用的高级硬件利用率。 你可以使用该工具来确定应用的性能是与 CPU 绑定还是与 GPU 绑定，并深入了解如何更有效地使用平台的硬件。 GPU 使用情况工具支持使用 Direct3D 12、Direct3D 11 和 Direct3D 10 的应用，但不支持其他图形 API（如 Direct2D 或 OpenGL）。  
  
 以下是“GPU 使用情况报告”窗口：  
  
 ![GPU 使用情况报告，提供 CPU 和 GPU 时间线](../debugger/media/gfx-diag-gpu-usage-report.png "gfx_diag_gpu_usage_report")  
  
## <a name="requirements"></a>要求  
 以下是除图形诊断要求之外使用 GPU 使用情况工具的要求。  
  
- 支持必要计时规范的 GPU 和驱动程序。  
  
  > [!NOTE]
  > 有关支持的硬件和驱动程序的详细信息，请参阅本文档末尾的[硬件和驱动程序支持](#hwsupport)。  
  
  有关图形诊断要求的详细信息，请参阅[入门](../debugger/getting-started-with-visual-studio-graphics-diagnostics.md)。  
  
## <a name="using-the-gpu-usage-tool"></a>使用 GPU 使用情况工具  
 在 GPU 使用情况工具下运行应用时，Visual Studio 将创建一个诊断会话，以图形方式实时显示有关应用的呈现性能和 GPU 利用率的高级信息。  
  
#### <a name="to-start-the-gpu-usage-tool"></a>启动 GPU 使用情况工具：  
  
1. 在菜单按钮中，选择“调试”，然后选择“性能和诊断”（键盘：按 Alt+F2）。  
  
2. 在“性能和诊断”中心，选中“GPU 使用情况”旁的复选框。 （可选）选中你希望使用的其他工具旁的复选框。 你可以同时运行几个性能和诊断工具，以便对应用的性能有一个更全面的了解。  
  
    ![选择要使用的诊断工具。](../debugger/media/gfx-diag-diagsession-tools.png "gfx_diag_diagsession_tools")  
  
   > [!NOTE]
   > 并非所有性能和诊断工具都可以同时使用。  
  
3. 选择“性能和诊断”中心底部的蓝色“启动”按钮，以便在所选工具下运行应用。  
  
   实时显示的高级信息包括帧时间、帧速率和 GPU 利用率。 每条信息都显示在独立的图形中，但使用公共的时间刻度，因此你可以轻松将它们联系在一起。  
  
   “帧时间(毫秒)”和“每秒帧数(FPS)”图形包含两条红色水平线，用于表示每秒 60 帧和 30 帧的性能目标。 在“帧时间”图形中，图形低于红线表示应用超过性能目标，高于红线表示未达到性能目标。 在“每秒帧数”图形中则相反，图形高于红线表示你的应用超过性能目标，低于红线表示未达到性能目标。 这些图形主要用于对你应用的性能有一个大致的了解，并确定你可能希望调查的减速情况，例如帧速率突降或 GPU 利用率陡升。  
  
   当你的应用在 GPU 使用情况工具下运行时，诊断会话还会收集有关在 GPU 上执行的图形事件的详细信息。 此信息用于生成有关应用如何利用硬件的更精细报告。 由于从收集的信息生成此报告需要一些时间，因此仅当诊断会话完成信息收集之后此报告才可用。  
  
   如果希望进一步了解性能或利用率问题，请停止收集性能信息，以便生成报告。  
  
#### <a name="to-generate-and-view-the-gpu-usage-report"></a>生成和查看 GPU 使用情况报告：  
  
1. 在诊断会话窗口底部，选择“停止收集”链接，或按左上角的“停止”。  
  
    ![收集 GPU 和 CPU 计时信息。](../debugger/media/gfx-diag-gpu-usage-collect.png "gfx_diag_gpu_usage_collect")  
  
2. 在报告的顶部，从显示要调查问题的图形中选择一个。 所选内容最长可达 3 秒，较长部分将被截尾。  
  
    ![收集之后，选择范围以查看详细信息](../debugger/media/gfx-diag-gpu-usage-select1.png "gfx_diag_gpu_usage_select1")  
  
3. 在报告底部的“...单击此处查看该范围内的 GPU 使用情况详细信息”消息中，选择“查看详细信息”链接，以查看所选内容的详细时间线。  
  
    ![收集之后，选定范围](../debugger/media/gfx-diag-gpu-usage-select2.png "gfx_diag_gpu_usage_select2")  
  
   这将打开一个新的标签页式文档，文档中包含报告。 GPU 使用情况报告可帮助你了解图形事件在 CPU 上的启动时间、到达 GPU 的时间以及 GPU 执行该事件所花费的时间。 此信息可以帮助你确定瓶颈和机遇，以提高代码的并行度。  
  
## <a name="using-the-gpu-usage-report"></a>使用 GPU 使用情况报告  
 GPU 使用情况报告的上半部分显示 CPU 处理活动、GPU 呈现活动以及 GPU 复制活动的时间线。 这些时间线由浅灰色的竖线分隔，竖线表示显示器的垂直同步。竖线的频率与从中收集 GPU 使用情况数据的其中一个显示器（使用“显示”下拉列表选择）的刷新率一致。 由于显示器的刷新率可能高于应用的性能目标，因此垂直同步与你希望达到的帧速率不一定具有一一对应关系。 若要达到其性能目标，应用必须完成所有处理、执行呈现，并对目标帧速率进行 Present() 调用，但在调用 Present() 后的下一个垂直同步之前，将不会显示呈现的帧。  
  
 下半部分显示报告期间发生的图形事件列表。  
  
 以下是“GPU 使用情况报告”窗口：  
  
 ![GPU 使用情况报告，提供 CPU 和 GPU 时间线](../debugger/media/gfx-diag-gpu-usage-report.png "gfx_diag_gpu_usage_report")  
  
 选择报告下半部分的其中一个事件会在相关时间线中的相应事件处放置一个标记，通常一个事件在 CPU 线程上，表示 API 调用；另一个事件在 GPU 时间线上，表示 GPU 完成任务的时间。 同样，选择时间线中的一个事件将在报告的下半部分突出显示相应事件。当缩小显示报告上半部分的时间线时，仅最耗时的事件可见。 若要查看持续时间更短的事件，可通过对你的指针设备使用 Ctrl + 滚轮或使用顶部面板左下角的缩放控件来放大时间线。 还可以拖动时间线面板中的内容，以浏览记录的事件。  
  
 为了帮助你找到要寻找的内容，可以基于进程名、线程 ID 和事件名筛选 GPU 使用情况报告。此外，还可以选择决定垂直同步线的显示器刷新率，如果你的应用使用 ID3DUserDefinedAnnotation 接口分组呈现命令，你还可以按层次结构排列事件。  
  
 以下是更多详细信息：  
  
|筛选器控件|描述|  
|--------------------|-----------------|  
|**Process**|你感兴趣的进程的名称。 诊断会话期间使用 GPU 的所有进程都包括在此下拉列表中。 与此下拉列表中的进程相关联的颜色是以下时间线中线程活动的颜色。|  
|**线程**|你感兴趣的线程 ID。 在多线程应用中，这有助于隔离属于你感兴趣的进程的特定线程。 与所选线程关联的事件在每条时间线中突出显示。|  
|**显示**|显示其刷新率的显示器编号**注意：** 可以配置某些驱动程序，以便将多个物理显示器显示为单个较大的虚拟显示器。 即使计算机连接了多个显示器，也可能仅列出一个。|  
|**筛选器**|你感兴趣的关键字。 报告的下半部分将仅包括与关键字完全匹配或部分匹配的事件。 你可以指定多个关键字并用分号 (;) 隔开。|  
|**层次结构排序**|指示是保留还是忽略事件层次结构（通过用户标记定义）的复选框。|  
  
 GPU 使用情况报告下半部分中的事件列表显示每个事件的详细信息。  
  
|列|描述|  
|------------|-----------------|  
|**事件名称**|图形事件的名称。 事件通常对应于 CPU 线程时间线中的一个事件和 GPU 时间线上的一个事件。<br /><br /> 如果 GPU 使用情况无法确定事件的名称，则事件名称可能“无归属”。 有关详细信息，请参阅此表下面的说明。|  
|**CPU 启动(纳秒)**|通过调用 Direct3D API 在 CPU 上启动事件的时间。 时间以纳秒计，与应用的启动时间相关。|  
|**GPU 启动(纳秒)**|在 GPU 上启动事件的时间。 时间以纳秒计，与应用的启动时间相关。|  
|**GPU 持续时间(纳秒)**|在 GPU 上完成事件所用的时间，以纳秒计。|  
|**进程名**|事件源于的应用的名称。|  
|**线程 ID**|事件源于的线程 ID。|  
  
> [!IMPORTANT]
> Windows 8.1 是事件归属所必需的。 此外，如果你的 GPU 或驱动程序不支持必要的检测功能，则所有事件将都显示为“无归属”。 如果遇到此问题，请确保更新 GPU 驱动程序，然后重试。 有关详细信息，请参阅下面的[硬件和驱动程序支持](#hwsupport)。  
  
## <a name="gpu-usage-settings"></a>GPU 使用情况设置  
 你可以将 GPU 使用情况工具配置为推迟收集分析信息，而不在应用启动后立即开始收集信息。 由于分析信息可能非常大，因此当你知道应用性能暂时不会降速时，这将很有用。  
  
#### <a name="to-postpone-profiling-from-the-start-of-the-app"></a>从应用的开头推迟分析：  
  
1. 在菜单按钮中，选择“调试”，然后选择“性能和诊断”（键盘：按 Alt+F2）。  
  
2. 在“性能和诊断”中心，按照“GPU 使用情况”旁的“设置”链接进行操作。  
  
3. 在“常规”属性页上的“GPU 分析配置”下，取消选中“在应用启动时开始分析”复选框以推迟分析。  
  
     ![配置 GPU 使用情况收集何时开始](../debugger/media/gfx-diag-gpu-usage-config.png "gfx_diag_gpu_usage_config")  
  
> [!IMPORTANT]
> Direct3D 12 当前不支持推迟分析。  
  
 如果使用此设置推迟分析信息的收集，当你在 GPU 使用情况工具下运行应用时，GPU 使用情况工具窗口底部的一个附加链接将变为可用。 若要开始收集分析信息，请选择“开始收集更多详细 GPU 使用情况数据”消息中的“启动”链接。  
  
## <a name="hwsupport"></a>硬件和驱动程序支持  
 支持以下 GPU 硬件和驱动程序：  
  
|Vendor|GPU 说明|要求的驱动程序版本|  
|------------|---------------------|-----------------------------|  
|Intel®|第四代 Intel® 芯处理器（“Haswell”）<br /><br /> -   Intel® HD Graphics (GT1)<br />-   Intel® HD Graphics 4200 (GT2)<br />-   Intel® HD Graphics 4400 (GT2)<br />-   Intel® HD Graphics 4600 (GT2)<br />-   Intel® HD Graphics P4600 (GT2)<br />-   Intel® HD Graphics P4700 (GT2)<br />-   Intel® HD Graphics 5000 (GT3)<br />-   Intel® Iris™ Graphics 5100 (GT3)<br />-   Intel® Iris™ Pro Graphics 5200 (GT3e)|--（使用最新驱动程序）|  
|AMD®|AMD Radeon™ HD 7000 系列之后的大多数产品（AMD Radeon™ HD 7350-7670 除外）<br /><br /> 具有 Graphics Core Next (GCN) 体系结构的 AMD Radeon™ GPU、AMD FirePro™ GPU 和 AMD FirePro GPU 加速器<br /><br /> 具有 Graphics Core Next (GCN) 体系结构的 MD® E 系列和 AMD A 系列加速处理单元 (APU)（“Kaveri”、“Kabini”、“Temash”、“Beema”、“Mullins”）|14.7 RC3 或更高版本|  
|NVIDIA®|NVIDIA GeForce® 400 系列之后的大多数产品<br /><br /> 具有 Fermi™、Kepler™ 或 Maxwell™ 体系结构的 NVIDIA® GeForce® GPU、NVIDIA Quadro® GPU 和 NVIDIA® Tesla™ GPU 加速器|343.37 或更高版本|  
  
 暂不支持 VIDIA® SLI™ 和 AMD Crossfire™ 等多 GPU 配置。 支持 VIDIA® Optimus™ 和 AMD Enduro™ 等混合图形设置。  
  
## <a name="see-also"></a>请参阅  
  
- [使用 DirectX 工具解决游戏中的复杂图形问题（视频）](http://channel9.msdn.com/Events/GDC/GDC-2015/Solve-the-Tough-Graphics-Problems-with-your-Game-Using-DirectX-Tools)  
  
- [Visual Studio 中的 GPU 使用情况工具（视频）](http://channel9.msdn.com/Events/Visual-Studio/Connect-event-2014/715)  
  
- [Visual Studio 2013 Update 4 CTP1 中的 GPU 使用情况工具（博客）](http://blogs.msdn.com/b/vcblog/archive/2014/09/05/gpu-usage-tool-in-visual-studio-2013-update-4-ctp1.aspx)  
  
- [Visual Studio 中 DirectX 的 GPU 使用情况](http://blogs.msdn.com/b/ianhu/archive/2014/12/16/gpu-usage-for-directx-in-visual-studio.aspx)
