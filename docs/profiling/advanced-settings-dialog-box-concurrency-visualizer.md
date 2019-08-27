---
title: “高级设置”对话框（并发可视化工具）| Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.cv.settings
ms.assetid: bb3d90aa-5f08-4953-9be0-be6cea11633d
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ae0507e75a84f18350817a33abe25d3e59fa9aa2
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68926326"
---
# <a name="advanced-settings-dialog-box-concurrency-visualizer"></a>“高级设置”对话框（并发可视化工具）
通过使用并发可视化工具中的“高级设置”  对话框，可以控制如何收集跟踪。  对话框中有符号、仅我的代码、缓冲、筛选、CLR 事件、标记、提供程序和文件的选项卡。

## <a name="symbols"></a>符号
 并发可视化工具使用与 Visual Studio 调试器相同的符号设置。 并发可视化工具使用这些设置来解析与性能数据相关的调用堆栈。  当处理跟踪时，并发可视化工具将访问在设置页中指定的符号服务器。  当通过网络访问此数据时，跟踪处理速度将会下降。  若要减少解析符号所需的时间，可以在本地缓存符号。 如果已下载符号，则 Visual Studio 将从本地缓存加载它们。

## <a name="just-my-code"></a>仅我的代码
 默认情况下，“仅我的代码”是一组与 Visual Studio 中的当前解决方案相关联的 .exe 和 .dll 文件   。 在使用“仅我的代码”功能筛选调用堆栈时，并发可视化工具将评估此文件组。 在“仅我的代码”选项卡上，可以将包含 .exe 和 .dll 文件的目录添加到并发可视化工具用于“仅我代码”的位置   。

 在收集跟踪时，.exe 和 .dll 文件的路径存储在跟踪文件中   。  更改此设置不会影响任何之前收集的跟踪。

## <a name="buffering"></a>缓冲
 收集跟踪时，并发可视化工具使用 Windows 事件跟踪 (ETW)。  在存储事件时，ETW 会使用各种缓冲区。  默认 ETW 缓冲区设置可能不是在所有情况下都最优，在某些情况下，可能会导致诸如丢失事件等问题。  可以使用“缓冲”选项卡来配置 ETW 缓冲区设置。 有关详细信息，请参阅 [Event Tracing](http://go.microsoft.com/fwlink/?LinkId=234579)（事件跟踪）和 [EVENT_TRACE_PROPERTIES structure](http://go.microsoft.com/fwlink/?LinkId=234580)（EVENT_TRACE_PROPERTIES 结构）。

## <a name="filter"></a>筛选器
 在“筛选器”选项卡上，可以选择并发可视化工具收集的一组事件。 选择一部分事件会限制报告中显示的数据类型，减少每个跟踪的大小，并缩减处理跟踪所需的时间。

### <a name="clr-events"></a>CLR 事件
 利用公共语言运行时 (CLR) 生成的事件，并发可视化工具能够解析托管调用堆栈。  如果禁止收集 CLR 事件，将减少跟踪大小，但某些调用堆栈将无法解析。  因此，一些 CPU 线程活动可能会错误地分类。

### <a name="collect-for-native-processes"></a>为本机进程收集
 默认情况下，仅在分析托管进程时才会收集 CLR 事件，因为它们对本机进程来说通常不是必需的。  在某些情况下（例如，本机进程正托管 CLR）时，您可能需要收集本机进程的 CLR 事件。  如果是这样，请选中“为本机进程收集”  复选框。

### <a name="disable-rundown-events"></a>禁用断开事件
 CLR 会从两个提供程序生成事件：运行时和断开。  如果要收集 CLR 运行时事件，但要避免收集断开事件，请选中“禁用断开事件”  复选框。  这会减少由集合生成的跟踪文件的大小，但有些堆栈可能无法解析。 有关详细信息，请参阅 [CLR ETW 提供程序](/dotnet/framework/performance/clr-etw-providers)。

### <a name="sample-events"></a>样本事件
 您可以使用样本事件来收集与线程执行有关的调用堆栈。 对于在当前进程中执行的线程，这些事件大约 1 毫秒收集一次。 如果禁止收集样本事件，则会减少所收集跟踪的大小，但无法查看与线程执行有关的任何调用堆栈。

### <a name="gpu-events"></a>GPU 事件
 GPU 事件是 DirectX 生成的事件。 如果禁止收集 GPU 事件，则会减少所收集跟踪的大小，但无法查看“使用率”视图中的任何 GPU 活动或“线程”视图中的 DirectX 引擎活动。

### <a name="file-io-events"></a>文件 I/O 事件
 文件 I/O 事件表示代表当前进程访问磁盘。  如果禁用文件 I/O 事件，则会减少跟踪的大小，但“线程”视图不会报告与磁盘通道或磁盘操作有关的任何信息。

## <a name="markers"></a>标记
 在“标记”选项卡上，可以配置在并发可视化工具中显示为“标记”的 ETW 提供程序组  。  还可以根据重要性级别和 ETW 类别来筛选“标记”集合。  如果使用[并发可视化工具 SDK](../profiling/concurrency-visualizer-sdk.md) 并使用自己的标记提供程序，则可以在此处注册，以便其显示在“线程”视图中。

### <a name="add-a-new-provider"></a>添加新提供程序
 如果代码使用[并发可视化工具 SDK](../profiling/concurrency-visualizer-sdk.md) 或生成符合 <xref:System.Diagnostics.Tracing.EventSource> 约定的 ETW 事件，则可以通过在此对话框中注册这些事件，在并发可视化工具中查看它们。

 在“名称”字段中，输入一个名称，用以描述由提供程序生成的事件  。  在“GUID”字段中，输入与此提供程序关联的 GUID  。 （GUID 与每个 ETW 提供程序相关联。）

 或者，您可以根据类别或重要性级别，指定是否从此提供程序中筛选出事件。  您可以使用类别字段，以便根据并发可视化工具 SDK 类别进行筛选。  为此，请输入逗号分隔的类别或类别范围字符串。  这会指定当前提供程序中要显示的事件类别。  如果要添加 <xref:System.Diagnostics.Tracing.EventSource> 提供程序，则可以使用类别字段按 ETW 关键字进行筛选。  因为关键字是位掩码，所以可以使用逗号分隔的整数字符串指定要设置掩码中的哪些位。 例如，“1,2”会设置第一个和第二个位，而这会转换为十进制的 6。

 可以使用重要性级别列表筛选出重要性或 ETW 级别小于指定值的事件。

### <a name="configure-an-existing-provider"></a>配置现有的提供程序
 若要编辑与现有提供程序相关联的设置，请在列表中将其选中，然后选择“编辑提供程序”  按钮。  可以更改名称、GUID 和筛选设置。

### <a name="filter-marker-data-out-of-concurrency-visualizer-reports"></a>从并发可视化工具报告中筛选出标记数据
 如果不希望未来的跟踪中出现特定提供程序的数据，请清除要移除的提供程序旁的复选框。

## <a name="files"></a>文件
 在“文件”  选项卡上，可以指定每次收集跟踪时用来存储跟踪文件的目录。  并发可视化工具会为每个所收集的跟踪生成四个文件：

- 内核模式事件跟踪日志 (ETL) 文件 (.kernel.etl*)

- 用户模式事件跟踪日志文件 (.user.etl*)

- 并发可视化工具数据文件 (.CVData*)

- 并发可视化工具跟踪文件 (.CVTrace*)

  两个 ETL 文件用于存储原始跟踪数据，而两个并发可视化工具文件用于存储处理后的数据。  处理跟踪后，通常不使用原始 ETL 文件。  选择“在分析后删除事件跟踪日志(ETL)文件”复选框后，将减少磁盘上存储的跟踪数据量  。

## <a name="see-also"></a>请参阅
- [仅我的代码](../profiling/just-my-code-threads-view.md)
- [并发可视化工具标记](../profiling/concurrency-visualizer-markers.md)