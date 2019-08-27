---
title: 图形诊断概述 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: ddd429d9-ac70-4ac4-9e69-299c6ea2df09
caps.latest.revision: 32
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 2dc0d0bf4efd8c30d874a24e94d3933d2eef713a
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68186540"
---
# <a name="overview-of-visual-studio-graphics-diagnostics"></a>Visual Studio 图形诊断概述
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio“图形诊断”是一套工具，用于记录、然后分析 Direct3D 应用中的呈现问题和性能问题  。 可对在 Windows PC 上、在 Windows 设备模拟器中或在远程 PC 或设备上本地运行的应用使用图形诊断。

## <a name="using-graphics-diagnostics-to-debug-rendering-problems"></a>使用图形诊断调试呈现问题
 对于图形丰富的应用程序，调试其中的呈现问题并不如启动调试器并逐句通过某些代码的方式直接。 在每个帧中，将生成数十万个唯一像素，每个像素都是根据一组复杂的状态、数据、参数和代码生成的，其中，可能只有少量像素会展示出你尝试诊断的问题。 生成每个像素的代码在并行处理数百个像素的专用硬件上执行，这使问题更加复杂。 传统调试工具和技术难以在包含少量线程的代码中使用，在处理大量数据时较为低效。

 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 中的图形诊断工具旨在通过启动指示问题的视觉效果，然后仅关注应用程序自有源代码中的相关着色器代码、管道阶段、绘图调用、资源和设备状态来进行反向跟踪，帮助你找到呈现问题。

## <a name="directx-version-compatibility"></a>DirectX 版本兼容性
 图形诊断支持使用 Direct3D 12、Direct3D 11 和 Direct3D 10 的应用，并对使用 Direct2D 的应用提供有限支持。 它不支持使用 Direct3D、DirectDraw 或其他图形 API 的更早版本的应用。

### <a name="windows-10-and-direct3d-12"></a>Windows 10 和 Direct3D 12
 Windows 10 引入了下一版本的 Direct3D: *Direct3D 12*，这是与 Direct3D 10 和 Direct3D 11 差别很大。 这些差异使 DirectX 重新符合现代图形硬件要求，并充分发挥其最大潜力，但是它们也导致对 API 的较大更改，并使程序员在管理资源生存期和争用方面具有更大的责任。 拥有卓越的调试工具对帮助图形程序员实现这一转换至关重要，所以 Visual Studio 2015 中的图形诊断从一开始就支持 Direct3D12。 尽管存在差异，支持 Direct3D 12 的图形诊断保持了与支持 Direct3D 11.2 的图形诊断同等的功能，除了帧分析功能以外。 很快，Direct3D 12 中将增加帧分析功能，随后将增加新的诊断工具，以帮助你解决可能会在 Direct3D 12 中遇到的新类型的 bug。

 Windows 10 还保持对以前版本的 Direct3D 及依赖于它的游戏和应用程序的支持。 Visual Studio 2015 中的图形诊断程序将在 Windows 10 上继续支持 Direct3D 10 和 Direct3D 11，在 Windows 8.1 上也是如此。

### <a name="windows-81-and-direct3d-112"></a>Windows 8.1 和 Direct3D 11.2
 在 [!INCLUDE[win81](../includes/win81-md.md)] 中，DirectX 11.2 介绍了一些新功能，包括对在其运行时期间捕获图形信息的支持。 [!INCLUDE[win81](../includes/win81-md.md)] 使用新的基于运行时捕获，称为*可靠捕获*— 专用于所有版本的 DirectX 的[!INCLUDE[win81](../includes/win81-md.md)]支持。 可靠捕获还支持 Direct3D 11.2 的新功能。

### <a name="limited-direct2d-support"></a>有限的 Direct2D 支持
 Direct2D 是以 Direct3D 为基础构建的用户模式 API，因此可以使用图形诊断帮助调试使用 Direct2D 的应用中的呈现问题。 不过，由于只记录基础 Direct3D 事件而非更高级别的 Direct2D 事件，Direct2D 事件不会显示在图形事件列表中。 此外，Direct2D 事件和生成的 Direct3D 事件之间的关系并非始终明确，因此使用图形诊断来调试使用 Direct2D 的应用中的呈现问题并不是直接方式。 但是，你仍可使用图形诊断来获取有关使用 Direct2D 的应用中低级别呈现问题的信息。

## <a name="graphics-diagnostics-features-in-visual-studio"></a>Visual Studio 中的图形诊断功能
 图形诊断具有一个专用界面：图形分析工具窗口，用于诊断呈现问题，但它还将一些工具添加到了 Visual Studio 界面。

### <a name="the-graphics-toolbar-visual-studio"></a>图形工具栏 (Visual Studio)
 通过“图形”工具栏，可以快速访问图形诊断命令。

 选择“启动诊断”按钮可在图形诊断下运行应用  。 在图形诊断下运行应用时，“捕获下一个呈现的帧”按钮处于启用状态  。

### <a name="diagnostics-capture-interface"></a>诊断捕获接口
 当你在图形诊断下运行应用时，Visual Studio 将显示一个诊断会话接口，可用于捕获帧，并且它还会显示当前的 CPU 和 GPU 负载。 显示 CPU 和 GPU 负载能帮助你识别可能因其性能特征（而不是呈现错误）而想要捕获的帧。

 但这不是唯一捕获帧的方法。 你还可以通过使用编程捕获界面或使用命令行捕获程序 dxcap.exe 来捕获帧。

 有关详细信息，请参阅[捕获图形信息](../debugger/capturing-graphics-information.md)。

### <a name="gpu-usage"></a>GPU 使用情况
 图形诊断还可以分析你的 Direct3D 应用的性能。 由于录制图形事件的详细信息会扭曲分析数据，所以这是独立于帧捕获的，将通过图形分析器进行检查来使用。

 有关详细信息，请参阅 [GPU 使用情况](../debugger/gpu-usage.md)。

### <a name="directx-control-panel"></a>DirectX 控制面板
 DirectX 控制面板是 DirectX 的一个组件，你可以使用此控制面板更改 DirectX 的行为方式，例如，可以启用 DirectX 运行时组件的调试版本、选择报告的调试消息类型，以及不允许使用某些图形硬件功能以模拟功能较少的硬件。 对 DirectX 的这一控制级别可帮助你调试和测试 DirectX 应用程序。 可以从 Visual Studio 访问 DirectX 控制面板。

##### <a name="to-open-the-directx-control-panel"></a>打开 DirectX 控制面板

- 在菜单栏上，依次选择“调试”、“图形”、“DirectX 控制面板”    。

## <a name="graphics-analyzer"></a>图形分析器
 Visual Studio 图形分析器是一个专用接口，用于检查你已捕获的帧中的呈现和性能问题。 在图形分析器中，你将发现多种工具，可帮助你浏览和理解应用的呈现行为。 每个工具会公开一种不同的有关正在检查的帧的信息，这些工具旨在协同使用以直观缩小呈现问题的源范畴，从其在帧缓冲区中的外观开始。

 此图示显示了图形分析器中工具的典型布局。

 ![所有图形调试器窗口](../debugger/media/graphicsdebuggerwindows.png "GraphicsDebuggerWindows")

### <a name="the-graphics-toolbar-graphics-analyzer"></a>图形工具栏（图形分析器）
 通过“图形”工具栏可以快速访问“图形分析器”工具窗口。

 ![图形诊断模式中的图形工具栏](../debugger/media/vsg-toolbar.png "vsg_toolbar")

### <a name="graphics-log-document"></a>图形日志文档
 在图形分析器中，“图形日志文档”是最醒目的工具窗口。 此窗口表示通过在图形诊断下运行你的应用所捕获的所有帧。 从这里，你可以选择不同的帧，以检查或选择你想要使用“像素历史记录”工具检查的特定像素。 此文档中显示的帧缓冲区图像会更改以反映当前选择的事件，这样你就能看到随着时间推移帧缓冲区会如何受到影响。

 [图形日志文档](../debugger/graphics-log-document.md)还是“帧分析”工具的入口点，它通过改变呈现的某些方面的配置方式并提供与原始结果进行比较的基准校验结果，可帮助你了解帧的性能。

### <a name="event-list"></a>事件列表
 图形事件标记每个 Direct3D API 调用和用户定义的事件。

 [事件列表](../debugger/graphics-event-list.md)显示所有已在你检查的帧期间记录的图形事件。 为了帮助你找出重要的内容，事件列表可以按层次结构查看 — 后续绘图调用下方有最新状态更改 — 或作为时间线查看。 此外，事件会基于它们所属的队列进行颜色编码，并且你可以筛选该列表使其仅包含你关注的事件。

 在列表中选择一个事件时，图形分析工具的其余部分反映事件发生时帧的状态。 以这种方式，你可以查看任意事件对 GPU 的影响。 例如，你可以查看帧缓冲区上任意绘图调动的直接影响，即使后续绘图调用使其变得模糊。 某些事件还具有超链接，你可以进行访问以查看有关其参数或相关资源对象的更多信息。

### <a name="pipeline-stages"></a>管道阶段
 你的应用中的每个绘图调用都要通过由 Direct3D 提供的图形管道。 在管道中的每个阶段，上一阶段的输出通过一个名为着色器的小程序进行转换，然后传递到下一个阶段，直到最后将其呈现到屏幕。 当输出格式与下一阶段的预期不同或任一阶段产生不正确的结果时，许多呈现错误会在管道阶段之间的边界发生。 通常情况下，你会得到将在屏幕上看到的最终结果，而并不能轻松地判断管道中发生错误的位置。

 [管道阶段](../debugger/graphics-pipeline-stages.md)窗口会单独可视化每个阶段的结果，在中，以便可以更轻松地确定哪个阶段先出现呈现问题。 一旦已确定是哪个阶段，就可以开始从“管道阶段”窗口调试其着色器。

### <a name="graphics-state"></a>图形状态
 呈现操作取决于通常分布在多个对象的大量状态。 很多种类的呈现问题都是由于配置错误的状态而引起的。

 [状态](../debugger/graphics-state.md)窗口会将与每个绘图调用相关的状态信息收集到一个地方，以便能更轻松地查找，并突出显示自上一个绘图调用以来发生的状态更改。

### <a name="pixel-history"></a>像素历史记录
 在复杂场景中，一个像素在单一帧中被多次着色的情况并不常见。 早期颜色有时只是被覆盖，但其他时候会合并颜色以实现透明度等效果。 当将它们组合起来而得不到正确的外观效果时，你无法轻松地判断是否这是因为其中一种颜色不正确，或者是否是它们组合的方式出现问题。 其他时候，可能看上去像是缺少对象，因为它对像素的贡献出于某种原因而被拒绝。

 [像素历史记录](../debugger/graphics-pixel-history.md)窗口直观显示在框架中，其中包括被拒绝的贡献的每个像素的完整着色器历史记录。 对于没有被拒绝的贡献，它将显示原始的着色器结果以及每个新的颜色与前一个颜色组合的方式。 在混合了着色器结果的像素中或者当呈现的对象因其对像素的贡献被错误地拒绝而缺少时，使用此信息能更轻松地找到错误的源。

### <a name="event-call-stack"></a>事件调用堆栈
 着色器代码不是 Direct3D 应用中的呈现问题的唯一根源，有时你的应用的源代码传递了错误的参数或没有完全正确地配置 Direct3D。 前面讨论的功能像素（历史记录）的一种错误，能帮助你发现什么时候呈现的对象因其所有像素被拒绝而丢失。 这种错误通常会在你错误配置了设置时发生，如控制深度测试方式的设置，你通常可以在缺少的对象的绘图调用中的某处找到错误。

 [事件调用堆栈](../debugger/graphics-event-call-stack.md)窗口将显示在事件列表中，每个图形事件的整个调用堆栈和甚至可以让您跳转到应用的源代码的调试信息是否可用。 这是一个强大的工具，能从 GPU 上错误最初出现的位置回溯到它在应用的源代码中产生的位置对错误进行跟踪。

### <a name="object-table"></a>对象表
 你的应用呈现的每一帧都可能是由数百甚至数千个资源对象所支持的。 其中可能包括后台缓冲区和呈现目标、纹理、顶点缓冲区、索引缓冲区、常规缓冲区 — Direct3D 记住的所有内容几乎都是一个对象。

 [对象表](../debugger/graphics-object-table.md)显示所有在事件列表中选择的图形事件时存在的对象。 由于典型应用中的大多数对象都是纹理，则会优化事件列表以一目了然地显示与映像相关的详细信息。 “类型”列告诉你每行中的对象的种类，“格式”列进一步显示对象的子类型或版本。 还显示了其他详细信息。 某些对象还具有超链接，你可以跟随它使用更专业的查看器查看对象（如纹理，你可以将纹理看作图像），或缓冲区（你可以选择缓冲区查看器的分析方式，并通过定义缓冲区格式显示原始缓冲区字节）。

### <a name="frame-analysis"></a>帧分析
 你的应用的图形不仅需要是正确的 — 它们也需要能快速显示。 即便是在性能较差的设备上（如使用集成图像的便携式计算机或移动电话）。 并且，它们仍需外观精美。

 [帧分析](../debugger/graphics-frame-analysis.md)工具通过自动改变应用使用 Direct3D 的方式并提供用于比较的基准校验结果，探索潜在的性能优化。 例如，帧分析可以在每个纹理上启用 mip 映射，可能会显示能够利用 mip 映射但当前尚未启用该映射的纹理。 在支持它的硬件上，帧分析还会显示从 GPU 的性能计数器收集的信息 — 此级别的信息可以确定硬件级别的性能问题，如大量的纹理提取暂停或缓存缺失。

 但帧分析并不只在于速度快 – 它还能让你在最小程度地影响视觉质量的情况下就能获得最优的性能。 有时在大显示屏上看起来很棒而造价昂贵的效果在电话的小显示屏上却起不到相同的作用，而在小屏幕上，更简单的效果看上也不错，同时还不会那么耗费电量。 图形分析提供的自动更改和基准检验可以帮助你跨各种设备找到适合你应用的平衡点。

## <a name="see-also"></a>请参阅
 [命令行捕获工具](../debugger/command-line-capture-tool.md) [HLSL 调试器](../debugger/hlsl-shader-debugger.md)
