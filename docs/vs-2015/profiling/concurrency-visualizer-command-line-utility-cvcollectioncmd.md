---
title: 并发可视化工具命令行实用工具 (CVCollectionCmd) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.cv.performance.cvcollectioncmd
ms.assetid: 476601be-1608-4014-af15-5aba6ccbed1c
caps.latest.revision: 26
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 23c6f008050cc2695a5b86d2164093823726a7b2
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74300649"
---
# <a name="concurrency-visualizer-command-line-utility-cvcollectioncmd"></a>并发可视化工具命令行实用工具 (CVCollectionCmd)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

你可以使用并发可视化工具命令行实用程序 (CVCollectionCmd.exe) 以从命令行收集跟踪，使你可以在 Visual Studio 的并发可视化工具中查看它们。 这些工具可以在未安装 Visual Studio 的计算机上使用。  
  
> [!NOTE]
> 从 Visual Studio 2013 开始，并发可视化工具是可选扩展。 (Previously it had been included in Visual Studio.) You can download the [Concurrency Visualizer Collection Tools for Visual Studio 2015](https://www.microsoft.com/download/details.aspx?id=49103) from the Download Center.  
  
## <a name="download-the-concurrency-visualizer-command-line-utility"></a>下载并发可视化工具命令行实用程序  
 若要下载并安装命令行实用程序，请转到 [Visual Studio 2015 的并发可视化工具收集工具](https://www.microsoft.com/download/details.aspx?id=49103) ，按照说明进行操作。 默认情况下，CVCollectionCmd.exe 安装在 %ProgramFiles%\Microsoft Concurrency Visualizer Collection Tools\（在 x64 计算机上为 %ProgramFiles(x86)%\Microsoft Concurrency Visualizer Collection Tools\）。  
  
## <a name="collect-a-trace-with-cvcollectioncmd"></a>使用 CVCollectionCmd 收集跟踪  
 通过使用 CVCollectionCmd 启动应用，或通过附加到该应用，你可以收集跟踪。 对于选项，请参阅以下命令参考。 例如  
  
```  
<Path>CVCollectionCmd /launch c:\myapp\myapp.exe /outdir c:\myapp\data  
```  
  
## <a name="commands-and-parameters"></a>命令和参数  
 若要获得有关命令行实用程序中的命令和参数的帮助，请在命令提示符处键入：  
  
 **CvCollectionCmd /?**  
  
|选项|描述|参数|返回值|  
|------------|-----------------|----------------|-------------------|  
|查询|返回是否可以启动收集。|None|如果准备开始启动收集，则为 0。<br /><br /> 如果收集已在进行中，则为 1。<br /><br /> 如果收集未在进行，但是已经启用一个或多个必需的 [ETW](https://msdn.microsoft.com/library/ac99a063-e2d2-40cc-b659-d23c2f783f92) 会话，则为 2。|  
|启动|在并发可视化工具下运行指定的进程。|可执行文件的路径。|如果运行已成功，则为 0。<br /><br /> 如果因为目标应用程序无法启动而运行失败，则为 1。<br /><br /> 如果因为 CVCollectionCmd 没有足够的权限写入指定的输出目录而运行失败，则为 13。|  
|Attach|开始收集系统级跟踪，否则如果指定了一个进程，则附加到该进程。|无。|如果附加成功，则为 0。<br /><br /> 如果因为指定的进程无效或不明确而附加失败，则为 1。<br /><br /> 如果因为 CVCollectionCmd 没有足够的权限写入指定的输出目录而附加失败，则为 13。|  
|Detach|停止收集。|无。|如果分离成功，则为 0。<br /><br /> 如果因为收集当前没有进行而分离失败，则为 1。<br /><br /> 如果因为无法停止收集而分离失败，则为 2。|  
|分析|分析指定的跟踪。|CVTrace 文件的完整路径。|如果分析成功，则为 0。<br /><br /> 如果因为指定的跟踪为系统级但是未指定目标进程而无法启动分析，则为 1。<br /><br /> 如果因为跟踪并非系统级并且已指定进程而无法启动分析，则为 2。<br /><br /> 如果因为指定的进程无效而分析失败，则为 3。<br /><br /> 如果因为指定的 CVTrace 文件无效而分析失败，则为 4。|  
|LaunchArgs|指定目标可执行文件参数。 此选项仅适用于“启动”命令。|应用程序的命令行参数。|无。|  
|Outdir|指定用于保存跟踪文件的目录。 适用于“启动”和“附加”命令。|目录路径或相对路径。|无。|  
|过程|当执行“附加”命令时，指定要附加到的进程，或者当执行“分析”命令时，指定要分析的跟踪中的进程。 适用于“附加”和“分析”命令。|PID 或进程的名称。|无。|  
|配置|如果你想要收集设置而非默认值，则指定配置文件的路径。   适用于“启动”、“附加”和“分析”命令。|XML 配置文件的目录路径或相对路径。|无。|  
  
## <a name="customizing-configuration-settings"></a>自定义配置设置  
 如果你使用 CVCollectionCmd 来收集跟踪并且希望自定义收集设置，则使用配置文件来指定它们。  
  
> [!NOTE]
> 当你使用 Visual Studio 收集跟踪时，请不要直接修改配置文件。  而是使用 [高级设置](../profiling/advanced-settings-dialog-box-concurrency-visualizer.md) 对话框来修改设置。  
  
 若要修改收集设置，则在你将运行 CVCollectionCmd 实用工具的计算机上创建配置文件。 你可以从头开始创建配置文件，或者可以在安装了 Visual Studio 的计算机上复制配置文件并修改该文件。 该文件名为 `UserConfig.xml` 并且位于“本地 AppData” 文件夹中。 当你运行实用工具时，与“启动”、“附加”或“分析”命令结合使用 Config 选项。  在与 Config 选项相关联的参数中，指定配置文件的路径。  
  
### <a name="configuration-file-tags"></a>配置文件标记  
 此配置文件基于 XML 文件。 以下是有效的标记和值：  
  
|Tag|描述|值|  
|---------|-----------------|------------|  
|配置|划分整体配置文件。|必须包含以下元素：<br /><br /> -   MinorVersion<br />-   MajorVersion|  
|MajorVersion|指定配置文件的主要版本。|对于 [!INCLUDE[vs_dev11_long](../includes/vs-dev11-long-md.md)] 项目，必须为 1。 如果不是 1，则实用工具不起作用。|  
|MinorVersion|指定配置文件的次要版本。|对于 [!INCLUDE[vs_dev11_long](../includes/vs-dev11-long-md.md)] 项目，必须为 0。 如果不是 0，则实用工具不起作用。|  
|IncludeEnvSymbolPath|设置一个值，该值确定是否使用环境符号路径 (_NT_SYMBOL_PATH)。|-   True<br />-   False|  
|DeleteEtlsAfterAnalysis|设置一个值，该值确定是否在分析完成时，删除 ETL 文件。|-   True<br />-   False|  
|SymbolPath|指定符号服务器的路径。 有关详细信息，请参阅 [使用 Microsoft 符号服务器获取调试符号文件](https://go.microsoft.com/fwlink/?LinkID=149389)。|目录名或 URL。|  
|标记|包含标记提供程序的列表。|可能不包含也可能包含多个 MarkerProvider 元素。|  
|MarkerProvider|指定单个标记提供程序。|必须包含以下元素：<br /><br /> -   Level<br />-   GUID<br />-   Name<br /><br /> 可以包含以下元素：<br /><br /> -   Categories<br />-   IsEnabled|  
|层次|设置 MarkerProvider 的重要性级别。|-   低<br />-   普通<br />-   高<br />-   严重<br />-   全部|  
|GUID|ETW 标记提供程序的全局唯一标识符。|一个 GUID。|  
|“属性”|指定标记提供程序的说明。|一个字符串。|  
|类别|指定为标记提供程序收集的类别。|一个以逗号分隔的数字或数字范围的字符串。|  
|IsEnabled|设置一个值，该值确定是否针对收集启用标记提供程序。|-   True<br />-   False|  
|FilterConfig|指定 ETW 事件的配置选项的列表，这些事件筛选自收集。|可能包含以下元素：<br /><br /> -   CollectClrEvents<br />-   ClrCollectionOptions<br />-   CollectSampleEvents<br />-   CollectGpuEvents<br />-   CollectFileIO|  
|CollectClrEvents|设置一个值，该值确定是否收集 CLR 事件。|-   True<br />-   False|  
|ClrCollectionOptions|指定是否针对本机应用收集 CLR 事件，并且是否收集 NGEN 断开事件。|可能包含下列值中的一个值、两个值或都不包含：<br /><br /> -   CollectForNative<br />-   DisableNGenRundown|  
|CollectSampleEvents|设置一个值，该值确定是否收集样本事件。|-   True<br />-   False|  
|CollectGpuEvents|设置一个值，该值确定是否收集由 DX 生成的事件。|-   True<br />-   False|  
|CollectFileIO|设置一个值，该值确定是否收集文件 I/O 事件。|-   True<br />-   False|  
|UserBufferSettings|指定用户缓冲区设置参数的列表。|必须包含以下元素：<br /><br /> -   BufferFlushTimer<br />-   BufferSize<br />-   MinimumBuffers<br />-   MaximumBuffers|  
|KernelBufferSettings|指定内核缓冲区设置参数的列表。|必须包含以下元素：<br /><br /> -   BufferFlushTimer<br />-   BufferSize<br />-   MinimumBuffers<br />-   MaximumBuffers|  
|BufferFlushTimer|指定 ETW 缓冲区的刷新计时器。|正整数。|  
|BufferSize|为每个事件跟踪会话缓冲区分配的内存量（以 KB 为单位）。|介于 0 至 1024 之间的数字。|  
|MinimumBuffers|为事件跟踪会话的缓冲池分配的缓冲区最小数目。|一个大于或等于逻辑内核数两倍的正整数。|  
|MaximumBuffers|为事件跟踪会话的缓冲池分配的缓冲区的最大数目。|一个大于或等于 MinimumBuffers 的数字。|  
|JustMyCode|指定“仅我的代码”目录的列表。|零个或多个 MyCodeDirectory 元素的列表。|  
|MyCodeDirectory|指定包含代码的目录。|绝对路径。|  
  
### <a name="example"></a>示例  
 你可以复制以下示例，然后对其进行修改以满足你的要求，而不是从头开始创建配置文件。  
  
```xml  
<?xml version="1.0"?>  
<LocalConfig xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" MajorVersion="1" MinorVersion="0">  
  
  <IncludeEnvSymbolPath>true</IncludeEnvSymbolPath>  
  
  <DeleteEtlsAfterAnalysis>true</DeleteEtlsAfterAnalysis>  
  
  <TraceLocation>C:\traces</TraceLocation>  
  
  <SymbolPath>http://symweb</SymbolPath>  
  
  <Markers>  
    <MarkerProvider Name="Default" Guid="8d4925ab-505a-483b-a7e0-6f824a07a6f0" Level="Low" />  
    <MarkerProvider Name="TPL" Guid="2e5dba47-a3d2-4d16-8ee0-6671ffdcd7b5" Level="Normal" />  
    <MarkerProvider Name="TPL Dataflow" Guid="16f53577-e41d-43d4-b47e-c17025bf4025" Level="Normal" />  
    <MarkerProvider Name="TPL Synchronization" Guid="ec631d38-466b-4290-9306-834971ba0217" Level="Normal" />  
    <MarkerProvider Name="PLINQ" Guid="159eeeec-4a14-4418-a8fe-faabcd987887" Level="Normal" />  
    <MarkerProvider Name="Concurrency Runtime" Guid="f7b697a3-4db5-4d3b-be71-c4d284e6592f" Level="Normal" />  
    <MarkerProvider Name="Scenario Markers" Guid="fb9244c9-f23a-4966-8a9c-97a51f8c355b" Level="Low" />  
  
    <!-- The IsEnabled and Categories elements are optional -->  
    <MarkerProvider Name="myMarker1" Guid="d0dbb3a3-895c-4ce6-96d9-28f69d664dc3" Level="Critical" IsEnabled="false" Categories="0,1,3-5,8" />  
    <MarkerProvider Name="myMarker2" Guid="03452127-a617-4302-9e30-c0d10442e4ee" Level="Low" IsEnabled="false" Categories="0,1,3-5,8-10,11-13" />  
  </Markers>  
  
  <FilterConfig>  
    <CollectClrEvents>true</CollectClrEvents>  
    <ClrCollectionOptions>CollectForNative DisableNGenRundown</ClrCollectionOptions>  
    <CollectSampleEvents>true</CollectSampleEvents>  
    <CollectGpuEvents>true</CollectGpuEvents>  
    <CollectFileIO>true</CollectFileIO>  
  </FilterConfig>  
  
  <UserBufferSettings>  
    <BufferFlushTimer>0</BufferFlushTimer>  
    <BufferSize>256</BufferSize>  
    <MinimumBuffers>512</MinimumBuffers>  
    <MaximumBuffers>1024</MaximumBuffers>  
  </UserBufferSettings>  
  
  <KernelBufferSettings>  
    <BufferFlushTimer>0</BufferFlushTimer>  
    <BufferSize>256</BufferSize>  
    <MinimumBuffers>512</MinimumBuffers>  
    <MaximumBuffers>1024</MaximumBuffers>  
  </KernelBufferSettings>  
  
  <!-- List of MyCodeDirectory directories -->  
  <JustMyCode>  
    <MyCodeDirectory>C:\myBinaries1</MyCodeDirectory>  
    <MyCodeDirectory>C:\myBinaries2</MyCodeDirectory>  
  </JustMyCode>  
</LocalConfig>  
  
```
