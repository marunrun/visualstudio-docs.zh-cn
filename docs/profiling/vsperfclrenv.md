---
title: VSPerfCLREnv | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- command-line tools, VSPerfCLREnv
- command line, tools
- performance tools, VSPerfCLREnv
- profiling tools,VSPerfCLREnv
- VSPerfCLREnv tool
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 119aa0a710218635cca945372ba9ea6fb6d4d27b
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62822880"
---
# <a name="vsperfclrenv"></a>VSPerfCLREnv

VSPerfCLREnv 工具用于设置配置 .NET Framework 应用程序所需的环境变量。 它使用以下语法：

```cmd
VsPerfCLREnv [/option]
```

选择的选项取决于使用三种分析类型中的哪一种：采样、检测或全局。 要在分析数据中包含层交互数据需要单独的选项。 以下各表中描述了每个选项的语法。

> [!NOTE]
> 完成分析后，请将 **VSPerfCLREnv** 与 **/off** 或 **/globaloff** 选项一起运行以删除分析所需的环境变量。 有关详细信息，请参阅此处显示的删除环境设置的 VSPerfCLREnv 选项。

## <a name="vsperfclrenv-options-for-including-tier-interaction-data"></a>用于包含层交互数据的 VSPerfCLREnv 选项

> [!WARNING]
> 可以使用任何版本的 Visual Studio 收集层交互分析。 但是，层交互分析数据只能在 Visual Studio Enterprise 中查看。

层交互分析提供有关多层应用程序中的 ADO.NET 查询的其他信息。 仅针对同步函数调用收集数据。 可以向使用任何分析方法的分析运行添加交互数据。

**InteractionOn** 和 **GlobalInteractionOn** 选项启用层交互数据收集。 在设置了分析应用程序所需的 VSPerfCLREnv 环境变量后，必须设置交互选项。

以下示例在使用采样方法的分析运行中包含层交互数据：

```cmd
VSPerfCLREnv /SampleOn
VSPerfCLREnv /InteractionOn
VSPerfCmd /Start:Sample /Output:MyApp.exe.vsp /Launch:MyApp.exe
```

以下示例在 Windows 服务的分析运行中包含层交互数据：

```cmd
VSPerfCLREnv /GlobalSampleOn
VSPerfCLREnv /GlobalInteractionOn
REM Restart the computer and start the service
VSPerfCmd /Start:Sample /Output:MyService.exe.vsp
VSPerfCmd /Attach:MyService.exe
```

## <a name="vsperfclrenv-options-for-process-instrumentation-profiling"></a>用于进程检测分析的 VSPerfCLREnv 选项

下表描述了用于检测分析的 VSPerfCLREnv 选项：

|选项|说明|
|------------|-----------------|
|**TraceOn**|启用使用检测方法的分析。 不会启用内存分配分析或对象生存期数据收集。|
|**TraceGC**|启用使用检测方法的内存分配分析。 不会启用对象生存期数据收集。|
|**TraceGCLife**|启用使用检测方法的内存分配分析和对象生存期数据收集。|

## <a name="vsperfclrenv-options-for-process-sampling-profiling"></a>用于进程采样分析的 VSPerfCLREnv 选项

下表描述了用于采样分析的 VSPerfCLREnv 选项：

|选项|说明|
|------------|-----------------|
|**SampleOn**|启用使用采样方法的分析。 不会启用内存分配分析或对象生存期数据收集。|
|**SampleGC**|启用使用采样方法的内存分配分析。 不会启用对象生存期数据收集。|
|**SampleGCLife**|启用使用采样方法的内存分配分析。 还启用对象生存期数据收集。|
|**SampleLineOff**|禁用 .NET 行级别分析数据的收集。|

## <a name="vsperfclrenv-options-for-global-profiling"></a>用于全局分析的 VSPerfCLREnv 选项

若要分析由操作系统启动、而不是由用户启动的 ASP.NET Web 应用程序等托管服务，请使用用于全局分析的 VSPerfCLREnv 选项。 下表描述了 VSPerfCLREnv 选项的全局版本。 这些选项可在注册表中设置合适的环境变量。

|选项|说明|
|------------|-----------------|
|**GlobalTraceOn**|启用使用检测方法的全局分析。 不会收集内存分配事件或对象生存期数据。|
|**GlobalTraceGC**|启用使用检测方法的全局内存分配分析。 不会启用对象生存期数据收集。|
|**GlobalTraceGCLife**|启用使用检测方法的全局内存分配分析。 还启用对象生存期数据收集。|
|**GlobalSampleOn**|启用使用采样方法的全局分析。 不会启用内存分配事件或对象生存期数据收集。|
|**GlobalSampleGC**|启用使用采样方法的全局内存分配分析。 不会启用对象生存期数据收集。|
|**GlobalSampleGCLife**|启用使用采样方法的全局内存分配分析。 还启用对象生存期数据收集。|

## <a name="vsperfclrenv-options-to-delete-environment-settings"></a>删除环境设置的 VSPerfCLREnv 选项

 在分析完托管应用程序后，请使用下列选项之一删除由 VSPerfCLREnv 添加的环境变量。 下表描述了如何删除标准和全局环境变量：

|选项|说明|
|------------|-----------------|
|**Off**|删除用于标准 .NET 分析的环境变量。 在使用了非全局的 VSPerfClrEnv 选项设置探查器环境变量后，使用此选项。|
|**GlobalOff**|删除用于全局 .NET 分析的环境变量。 当应用程序由操作系统而非探查器启动时，使用此选项。|

## <a name="remarks"></a>备注

如果托管应用程序是由 IDE 中的性能资源管理器启动的，分析此应用程序则不需要这些选项。 性能资源管理器可为你设置所有必需的环境设置。

如果在分析期间未设置正确的环境，在分析期间将报告警告，并且将无法正确地解析托管函数名称。

## <a name="see-also"></a>请参阅

[通过命令行分析](../profiling/using-the-profiling-tools-from-the-command-line.md)