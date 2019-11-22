---
title: Graphics Frame Analysis | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.graphics.frameanalysis
ms.assetid: 336c48ba-a1c4-4db9-b2a4-3de4a129cdd6
caps.latest.revision: 12
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 331722df4749ca59241259e13c3b387d8303b69f
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74300513"
---
# <a name="graphics-frame-analysis"></a>图形帧分析
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

使用 Visual Studio 图形分析器中的图形帧分析可分析并优化你的 Direct3D 游戏或应用的呈现性能。  
  
> [!IMPORTANT]
> 图形分析器对于在支持的平台（包括 Windows 10）上使用 Direct3D 11 的应用支持帧分析。 对于使用 Direct3D 12 的应用，当前不支持帧分析。  
  
## <a name="frame-analysis"></a>帧分析  
 帧分析使用的信息与在图形日志文件中捕获的用于诊断的信息相同，但是使用它可汇总呈现性能。 在捕获期间，性能信息未记录到日志中；相反，性能信息稍后可通过计时事件和在播放帧时收集统计信息，在帧分析期间生成。 通过在捕获期间记录性能信息，此方法具有以下几个优点：  
  
- 帧分析可以求取同一帧的多次播放的结果的平均值，以确保性能摘要在统计学上是可靠的。  
  
- 帧分析可以生成硬件配置和设备的性能信息，而非捕获信息的硬件配置和设备的性能信息。  
  
- 帧分析可以从之前捕获的信息中生成新的性能摘要，例如，在 GPU 驱动程序已优化或公开附加调试功能时。  
  
  除了这些优点以外，帧分析还可以对播放期间帧得以呈现的方式作出更改，以便它可以显示这些更改可能如何影响应用的呈现性能的相关信息。 你可以使用这些信息在可能的优化策略中进行决策，而无需实施所有策略，然后捕获并比较所有结果。  
  
  虽然帧分析主要用于帮助你获得更快的呈现性能，但是它同样可以帮助你使给定的性能目标获得更好的视觉质量，或者减少 GPU 耗电量。  
  
  To see a demonstration of what Frame Analysis can do for your app, you can watch the [Visual Studio Graphics Frame Analysis](https://channel9.msdn.com/Shows/C9-GoingNative/GoingNative-25-Offline-Analysis-Graphics-Tool) video on Channel 9.  
  
## <a name="using-frame-analysis"></a>使用帧分析  
 在可以使用帧分析之前，你必须在应用运行时从应用中捕获图形信息，正如你在使用任何其他图形分析器工具时进行的操作。 然后，在图形日志文档 (.vsglog) 窗口中，选择“帧分析”选项卡。  
  
 ![Select the Frame Analysis tab.](../debugger/media/pix-frame-analysis-select-tab.png "pix_frame_analysis_select_tab")  
  
 在分析完成之后，将显示结果。 帧分析选项卡顶部将显示时间线和摘要表。 选项卡底部将显示详细信息表。 如果在播放期间产生错误或警告，则将在时间线上对它们进行汇总；你可以遵循此处的链接以了解错误和警告的详细信息。  
  
### <a name="interpreting-results"></a>解释结果  
 通过解释每个变体的结果，可推断有关你的应用的呈现性能和行为的有用信息。 有关呈现变体的详细信息，请参阅本文后面的[变体](#Variants)。  
  
 有些结果直接指示变体如何影响呈现性能：  
  
- 如果“双线性纹理筛选”变体显示性能提升，则在你的应用中使用双线性纹理筛选将显示类似的性能提升。  
  
- 如果“1x1 视口”变体显示性能提升，则减小你的应用中的呈现器目标的大小将提升其呈现性能。  
  
- 如果“BC 纹理压缩”变体显示性能提升，则在你的应用中使用 BC 纹理压缩将显示类似的性能提升。  
  
- 如果 2xMSAA 变体与 0xMSAA 变体具有几乎相同的性能，则你可以在你的应用中启用 2xMSAA 以提高其呈现质量，而无需性能开销。  
  
  其他结果可能会更隐晦、更微妙地暗示应用的性能：  
  
- 如果“1x1 视口”变体显示显著的性能提升，则很可能你的应用的可用填充率不足。 如果此变体未显示任何性能提升，则应用很可能处理了太多顶点。  
  
- 如果“16bpp 呈现器目标格式”变体显示显著的性能提升，则很可能你的应用占用了太多内存带宽。  
  
- 如果“一半/四分之一纹理尺寸”变体显示显著的性能提升，则很可能你的纹理占用了太多内存、消耗了太多带宽，或使用了效率低下的纹理缓存。 如果此变体显示性能中没有更改，则你很可能可以使用更大、细节更多的纹理，而无需性能开销。  
  
  当硬件计数器可用时，你可以使用它们收集有关应用可能会遭遇呈现性能问题原因的非常详细的信息。 所有功能级别 9.2 和更高设备支持深度封闭查询（“封闭的像素”计数器）以及时间戳。 其他硬件计数器也可能可用，这取决于 GPU 制造商是否实施了硬件计数器并在驱动程序中公开了这些计数器。 你可以使用这些计数器来确认摘要表中显示的结果的确切成因，例如，你可以通过检查深度测试封闭的像素的百分比，确定过度绘制是否是一个因素。  
  
### <a name="timeline-and-summary-table"></a>时间线和摘要表  
 默认情况下，显示时间线和摘要表，并且折叠其他部分。  
  
#### <a name="timeline"></a>时间线  
 时间线显示彼此相关的绘图调用计时的概述。 因为较大的直条对应于较长的绘图时间，所以你可以使用它快速地定位帧中能耗最高的绘图调用。 当捕获的帧包含大量绘图调用时，多个绘图调用将合并到一个直条中，其长度为这些绘图调用的总和。  
  
 ![The timeline shows draw&#45;call costs.](../debugger/media/pix-frame-analysis-timeline.png "pix_frame_analysis_timeline")  
  
 你可以释放直条上的指针，以查看该直条对应于哪个绘图调用事件。 选择该直条会使事件列表同步到该事件。  
  
#### <a name="table"></a>表  
 时间线下的数字表显示了与应用的默认呈现有关的每个绘图调用的每个呈现变体的相对性能。 每一列都显示一个不同的呈现变体，每一行都表示一个在最左边的列中标识的不同的绘图调用；你可以从此处遵循指向“图形事件列表”窗口中的事件的链接。  
  
 ![The summary table shows different varients.](../debugger/media/pix-frame-analysis-summary.png "pix_frame_analysis_summary")  
  
 摘要表左起第二列显示应用的基线呈现时间，即应用用以完成绘图调用所需的默认呈现时长。 其余各列将每个呈现变体的相对性能显示为基线的百分比，以便更容易看出性能是否有所提升。 大于 100% 的百分比花费的时间比基线长（即降低了性能），小于 100% 的百分比花费的时间比基线短（即提升了性能）。  
  
 实际上，基线的绝对计时和呈现变体的相对计时的值都是指多次运行的平均值（默认为 5）。 此平均计算有助于确保计时数据可靠且一致。 你可以将鼠标指针放在每个单元格上，以检查这个绘图调用和呈现变体的结果生成时所观察到的最小、最大、平均和中间计时值。 还会显示基线计时。  
  
#### <a name="hot-draw-calls"></a>“热点”绘图调用  
 为了引起对消耗了较大部分的整体呈现时间或由于无法避免的原因而可能速度异常缓慢的绘图调用的注意，当其本身的基线计时大于一个标准偏差，长于帧中所有绘图调用的平均基线计时时，会将包含这些“热点”绘图调用的行着色为红色。  
  
 ![This DrawIndexed call has hot and cold varients.](../debugger/media/pix-frame-analysis-hot-calls.png "pix_frame_analysis_hot_calls")  
  
#### <a name="statistical-significance"></a>统计意义  
 为了引起对具有最高相关性的呈现变体的注意，帧分析将确定每个呈现变体的统计意义，并将有意义的变体显示为黑体字。 它将提升性能的变体显示为绿色，将降低性能的变体显示为红色。 它还将不具有统计学意义的结果显示为正常字体。  
  
 ![The statistical relevance of the draw call variant](../debugger/media/pix-frame-analysis-summary-stats.png "pix_frame_analysis_summary_stats")  
  
 To determine statistical relevance, Frame Analysis uses the [Student's t-test](https://en.wikipedia.org/wiki/Student's_t-test).  
  
### <a name="details-table"></a>详细信息表  
 “摘要”表下面是默认为折叠状态的“详细信息”表。 “详细信息”表的内容取决于播放计算机的硬件平台。 有关支持的硬件平台的信息，请参阅[硬件支持](#HardwareSupport)。  
  
#### <a name="platforms-that-do-not-support-hardware-counters"></a>不支持硬件计数器的平台  
 大多数平台不完全支持硬件 GPU 计数器，其中包括当前由 Intel、AMD 和 nVidia 提供的所有 GPU。 当不存在要收集的硬件计数器时，将仅显示一张“详细信息”表，它包含所有变体的平均绝对计时。  
  
 ![The details table and some playback varients.](../debugger/media/pix-frame-analysis-details.png "pix_frame_analysis_details")  
  
#### <a name="platforms-that-support-hardware-counters"></a>支持硬件计数器的平台  
 对于支持硬件 GPU 计数器的平台（例如，nVidia T40 SOC 和所有 Qualcomm SOC），将显示几张“详细信息”表，每张表对应一个变体。 为每个呈现变体收集每个可用的硬件计数器，它们显示在其本身的“详细信息”表中。  
  
 ![Hardware counters are displayed when supported.](../debugger/media/pix-frame.png "pix_frame")  
  
 硬件计数器信息为每个绘图调用都提供了一个特定硬件平台行为的非常详细的视图，可帮助你非常准确地标识出现性能瓶颈的原因。  
  
> [!NOTE]
> 不同的硬件平台支持不同的计数器；不存在任何标准。 计数器及其表示的内容由每个 GPU 制造商单独确定。  
  
### <a name="marker-regions-and-events"></a>标记区域和事件  
 帧分析支持用户定义的事件标记和事件组。 它们将显示在摘要表和详细信息表中。  
  
 你可以使用 ID3DUserDefinedAnnotation API 或旧版 D3DPERF_ 系列的 API 来创建标记和组。 使用 D3DPERF_ API 系列时，你可以为每个标记和组分配一种颜色；在包含事件标记或事件组开始/结束标记及其内容的行中，帧分析将该颜色显示为彩色带的颜色。 此功能可以帮助你快速标识重要的呈现事件或事件组。  
  
### <a name="warnings-and-errors"></a>警告和错误  
 帧分析完成时，偶尔会伴随警告或错误，警告或错误信息将汇总在“时间线”上方，“帧分析”选项卡底部将显示对它们的详细描述。  
  
 通常情况下，警告和错误仅用于提供信息，且不要求任何干预。  
  
 警告通常指示缺少硬件支持但是可以得到解决、无法收集硬件计数器或某些性能数据可能不可靠（例如，当解决方法对它造成负面影响时）。  
  
 错误通常指示帧分析实现包含 Bug、驱动程序包含 Bbug、缺少硬件支持且无法得到解决，或应用尝试播放不支持的某些内容。  
  
### <a name="retries"></a>重试  
 如果 GPU 在帧分析期间进行了电源状态转换，必须再次尝试受影响的分析传递，因为 GPU 时钟速度发生了更改，所以会使相关的计时结果无效。  
  
 帧分析将重试次数限制为 10。 如果你的平台包含积极的电源管理或门控时钟，它可能会导致帧分析失败并报告错误，因为它已经超过了重试限制。 你也许可以通过将平台的电源管理和时钟速度重置以降低积极性来缓解此问题（如果平台启用了它）。  
  
## <a name="HardwareSupport"></a> 硬件支持  
  
### <a name="timestamps-and-occlusion-queries"></a>时间戳和封闭查询  
 在支持帧分析的所有平台上都受支持的时间戳。 深度封闭查询（对于“封闭的像素”计数器是必需的）在支持功能级别 9.2 或更高级别的平台上均受支持。  
  
> [!NOTE]
> 虽然所有支持帧分析的平台都支持时间戳，但是时间戳的准确性和一致性因平台而异。  
  
### <a name="gpu-counters"></a>GPU 计数器  
 对 GPU 硬件计数器的支持与硬件相关。  
  
 因为当前由 Intel、AMD 或 nVidia 提供的计算机 GPU 都无法可靠地支持 GPU 硬件计数器，所以帧分析不会从中收集计数器。 但是，帧分析会从以下能够可靠地支持它们的 GPU 中收集硬件计数器：  
  
- Qualcomm SOC（全部支持 Windows Phone）  
  
- nVidia T40 (Tegra4)。  
  
  任何其他支持帧分析的平台都不会收集 GPU 硬件计数器。  
  
> [!NOTE]
> 由于 GPU 硬件计数器为硬件资源，因此要收集每个呈现变体的完整硬件计数器整集可能要采取多个传递。 因此，收集计数器 GPU 应采取的顺序未指定。  
  
### <a name="windows-phone"></a>Windows phone  
 时间戳、封闭查询和 GPU 硬件计数器仅在最初随 Windows Phone 8.1 提供的 Windows Phone 手机上受支持。 帧分析需要它们以播放图形日志文件。 最初随 Windows Phone 8 提供的 Windows Phone 手机不支持帧分析，即使手机已更新到 Windows Phone 8.1 也是如此。  
  
## <a name="unsupported-scenarios"></a>不支持的方案  
 不支持以某些方式使用帧分析，或者说它们是糟糕的方案。  
  
### <a name="warp"></a>WARP  
 帧分析旨在用于配置和提升真实硬件上的呈现性能。 不阻止在 WARP 设备上运行帧分析（在 WARP 上运行 Windows Phone 模拟器），但是通常这么做不值得，因为在高端 CPU 上运行的 WARP 的运行速度甚至比功能最少的现代 GPU 还慢，而且根据其运行的特定 CPU，WARP 的性能可能差别很大。  
  
### <a name="playback-of-high-feature-level-captures-on-down-level-devices"></a>低级别设备上高功能级别捕获的播放  
 在图形分析器中，当你播放使用比播放计算机支持的功能级别更高的图形日志文件时，它将自动回退到 WARP。 在帧分析中，它显然不会回退到 WARP，而且它会生成一个错误，因为 WARP 对于检查 Direct3D 应用的正确性（而非其性能）很有用。  
  
> [!NOTE]
> 虽然记住功能级别的问题很重要，但是你可以在不同的硬件配置和设备上捕获并播放图形日志文件。 例如，你可以在 Windows Phone 上捕获图形信息，然后在台式计算机上播放它，反之亦然。 在这两种情况下，只要日志文件不包含 API 或使用在播放计算机上不受支持的功能级别，就可以播放图形日志。  
  
### <a name="direct3d-10-and-lower"></a>Direct3D 10 及更低版本  
 帧分析仅在 Direct3D 11 API 中受支持。 如果你的应用调用 Direct3D 10 API，则即使图形分析器工具已识别并使用它们，帧分析也不会识别或配置它们。 如果你的应用同时使用 Direct3D11 API 和 Direct3D 10 API，则仅配置 Direct3D 11 调用。  
  
> [!NOTE]
> 这仅适用于你正在使用的 Direct3D API 调用，不适用于功能级别。 只要你使用的是 Direct3D 11、Direct3D 11.1 或 Direct3D 11.2 API，你就可以随意使用所需的功能级别，帧分析还会正常工作。  
  
## <a name="Variants"></a> 变量  
 播放期间，帧分析对呈现帧的方式所做出的每个更改称为“变体”。 帧分析检查的变体对应于你为了提升应用的呈现性能或视觉质量可能做出的相对容易的常见更改，例如，减小纹理大小、使用纹理压缩或启用不同种类的抗锯齿。 这些变体将重写应用的常用呈现上下文和参数。 摘要如下：  
  
|变体|描述|  
|-------------|-----------------|  
|**1x1 视区大小**|将所有呈现器目标上的视口尺寸缩小为 1x1 像素。<br /><br /> 有关详细信息，请参阅 [1x1 视区大小变体](../debugger/1x1-viewport-size-variant.md)|  
|**0x MSAA**|在所有呈现器目标上禁用多重采样抗锯齿 (MSAA)。<br /><br /> 有关详细信息，请参阅 [0x/2x/4x MSAA 变体](../debugger/0x-2x-4x-msaa-variants.md)|  
|**2x MSAA**|在所有呈现器目标上启用 2x 多重采样抗锯齿 (MSAA)。<br /><br /> 有关详细信息，请参阅 [0x/2x/4x MSAA 变体](../debugger/0x-2x-4x-msaa-variants.md)|  
|**4x MSAA**|在所有呈现器目标上启用 4x 多重采样抗锯齿 (MSAA)。<br /><br /> 有关详细信息，请参阅 [0x/2x/4x MSAA 变体](../debugger/0x-2x-4x-msaa-variants.md)|  
|**点纹理筛选**|针对所有相应的纹理采样，将筛选模式设置为 `DXD11_FILTER_MIN_MAG_MIP_POINT`（点纹理筛选）。<br /><br /> For more information, see [Point, Bilinear, Trilinear, and Anisotropic Texture Filtering Variants](../debugger/point-bilinear-trilinear-and-anisotropic-texture-filtering-variants.md).|  
|**双线性纹理筛选**|针对所有相应的纹理采样，将筛选模式设置为 `DXD11_FILTER_MIN_MAG_LINEAR_MIP_POINT`（双线性纹理筛选）。<br /><br /> For more information, see [Point, Bilinear, Trilinear, and Anisotropic Texture Filtering Variants](../debugger/point-bilinear-trilinear-and-anisotropic-texture-filtering-variants.md).|  
|**三双线性纹理筛选**|针对所有相应的纹理采样，将筛选模式设置为 `DXD11_FILTER_MIN_MAG_MIP_LINEAR`（三线性纹理筛选）。<br /><br /> For more information, see [Point, Bilinear, Trilinear, and Anisotropic Texture Filtering Variants](../debugger/point-bilinear-trilinear-and-anisotropic-texture-filtering-variants.md).|  
|**各向异性纹理筛选**|针对所有相应的纹理采用，将筛选模式设置为 `DXD11_FILTER_ANISOTROPIC`，并将 `MaxAnisotropy` 设置为 `16`（16x 各向异性纹理筛选）。<br /><br /> For more information, see [Point, Bilinear, Trilinear, and Anisotropic Texture Filtering Variants](../debugger/point-bilinear-trilinear-and-anisotropic-texture-filtering-variants.md).|  
|**16bpp 呈现器目标格式**|针对所有呈现器目标和后台缓冲区，将像素格式设置为 `DXGI_FORMAT_B5G6R5_UNORM`（16bpp，565 格式）。<br /><br /> 有关详细信息，请参阅 [16bpp 呈现目标格式变体](../debugger/16bpp-render-target-format-variant.md)|  
|**Mip 贴图生成**|对非呈现器目标的所有纹理启用 Mip 贴图。<br /><br /> 有关详细信息，请参阅 [Mip 贴图生成变体](../debugger/mip-map-generation-variant.md)。|  
|**一半纹理尺寸**|将非呈现器目标的所有纹理上的纹理尺寸减小为其每种尺寸的原始大小的一半。 例如，256x128 纹理将减小为 128x64 纹素。<br /><br /> 有关详细信息，请参阅 [Half/Quarter 纹理维度变体](../debugger/half-quarter-texture-dimensions-variant.md)。|  
|**四分之一纹理尺寸**|将非呈现器目标的所有纹理上的纹理尺寸减小为其每种尺寸的原始大小的四分之一。 例如，256x128 纹理将减小为 64x32 纹素。<br /><br /> 有关详细信息，请参阅 [Half/Quarter 纹理维度变体](../debugger/half-quarter-texture-dimensions-variant.md)。|  
|**BC 纹理压缩**|对所有包含 B8G8R8X8、B8G8R8A8 或 R8G8B8A8 像素格式变体的纹理启用块压缩。 通过使用 BC1 压缩 B8G8R8X8 格式变体；通过使用 BC3 压缩 B8G8R8A8 和 R8G8B8A8 格式变体。<br /><br /> 有关详细信息，请参阅 [BC 纹理压缩变体](../debugger/bc-texture-compression-variant.md)。|  
  
 大多数变体的结果是强制性规定：“将纹理大小减小一半速度会快 25%”或“启用 2x MSAA 速度仅慢 2%”。 其他变体可能会需要更多解释，例如，如果将视口尺寸更改为 1x1 的变体显示较大的性能提升，则可能指示呈现遇到低填充率瓶颈；或者，如果性能未出现显著变化，则可能指示呈现遇到顶点处理瓶颈。
