---
title: 用于调试的 SDK 帮助程序 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- dbgmetric.lib
- registry, Debugging SDK
- Debugging SDK, registry locations
- dbgmetric.h
- metrics [Debugging SDK]
ms.assetid: 80a52e93-4a04-4ab2-8adc-a7847c2dc20b
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 9edb7c508fdea6736a71c0f70c0d2ff305d4a399
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80713652"
---
# <a name="sdk-helpers-for-debugging"></a>用于调试的 SDK 帮助程序
这些函数和声明是用于实现 c + + 中的调试引擎、表达式计算器和符号提供程序的全局帮助器函数。

> [!NOTE]
> 目前没有这些函数和声明的托管版本。

## <a name="overview"></a>概述
 为了使调试引擎、表达式计算器和 Visual Studio 使用的符号提供程序，必须进行注册。 这是通过设置注册表子项和条目来完成的，也称为 "设置度量值"。 以下全局函数旨在简化更新这些度量值的过程。 请参阅注册表位置部分，以了解这些函数更新的每个注册表子项的布局。

## <a name="general-metric-functions"></a>常规度量函数
 这些是调试引擎使用的常规功能。 稍后详细介绍了表达式计算器和符号提供程序的专用函数。

### <a name="getmetric-method"></a>GetMetric 方法
 从注册表检索指标值。

```cpp
HRESULT GetMetric(
   LPCWSTR pszMachine,
   LPCWSTR pszType,
   REFGUID guidSection,
   LPCWSTR pszMetric,
   DWORD * pdwValue,
   LPCWSTR pszAltRoot
);
```

|参数|说明|
|---------------|-----------------|
|pszMachine|中可能远程计算机的名称，其寄存器将写入 (`NULL` 表示本地计算机) 。|
|pszType|中度量值类型之一。|
|guidSection|中特定引擎、计算器、异常等的 GUID。这会为特定元素指定指标类型下的子节。|
|pszMetric|中要获取的指标。 这对应于特定的值名称。|
|pdwValue|中指标中值的存储位置。 有多种类型的 GetMetric 可以返回 DWORD (，如本示例所示) 、BSTR、GUID 或 Guid 数组。|
|pszAltRoot|中要使用的备用注册表根目录。 将设置为 `NULL` 以使用默认值。|

### <a name="setmetric-method"></a>SetMetric 方法
 在注册表中设置指定的指标值。

```cpp
HRESULT SetMetric(
         LPCWSTR pszType,
         REFGUID guidSection,
         LPCWSTR pszMetric,
   const DWORD   dwValue,
         bool    fUserSpecific,
         LPCWSTR pszAltRoot
);
```

|参数|说明|
|---------------|-----------------|
|pszType|中度量值类型之一。|
|guidSection|中特定引擎、计算器、异常等的 GUID。这会为特定元素指定指标类型下的子节。|
|pszMetric|中要获取的指标。 这对应于特定的值名称。|
|dwValue|中度量值中值的存储位置。 在此示例中，有几种类型的 SetMetric 可存储 DWORD () 、BSTR、GUID 或 Guid 数组。|
|fUserSpecific|中如果度量值是用户特定的，并且应该写入用户的 hive 而不是本地计算机 hive，则为 TRUE。|
|pszAltRoot|中要使用的备用注册表根目录。 将设置为 `NULL` 以使用默认值。|

### <a name="removemetric-method"></a>RemoveMetric 方法
 从注册表中删除指定的指标。

```cpp
HRESULT RemoveMetric(
   LPCWSTR pszType,
   REFGUID guidSection,
   LPCWSTR pszMetric,
   LPCWSTR pszAltRoot
);
```

|参数|说明|
|---------------|-----------------|
|pszType|中度量值类型之一。|
|guidSection|中特定引擎、计算器、异常等的 GUID。这会为特定元素指定指标类型下的子节。|
|pszMetric|中要删除的度量值。 这对应于特定的值名称。|
|pszAltRoot|中要使用的备用注册表根目录。 将设置为 `NULL` 以使用默认值。|

### <a name="enummetricsections-method"></a>EnumMetricSections 方法
 枚举注册表中的各种指标部分。

```cpp
HRESULT EnumMetricSections(
   LPCWSTR pszMachine,
   LPCWSTR pszType,
   GUID *  rgguidSections,
   DWORD * pdwSize,
   LPCWSTR pszAltRoot
);
```

|参数|说明|
|---------------|-----------------|
|pszMachine|中可能远程计算机的名称，其寄存器将写入 (`NULL` 表示本地计算机) 。|
|pszType|中度量值类型之一。|
|rgguidSections|[in，out]要填充的预先分配的 Guid 数组。|
|pdwSize|中可在数组中存储的最大 Guid 数目 `rgguidSections` 。|
|pszAltRoot|中要使用的备用注册表根目录。 将设置为 `NULL` 以使用默认值。|

## <a name="expression-evaluator-functions"></a>表达式计算器函数

|函数|说明|
|--------------|-----------------|
|GetEEMetric|从注册表检索指标值。|
|SetEEMetric|在注册表中设置指定的指标值。|
|RemoveEEMetric|从注册表中删除指定的指标。|
|GetEEMetricFile|获取指定指标中的文件名，并将其加载，并将文件内容作为字符串返回。|

## <a name="exception-functions"></a>异常函数

|函数|说明|
|--------------|-----------------|
|GetExceptionMetric|从注册表检索指标值。|
|SetExceptionMetric|在注册表中设置指定的指标值。|
|RemoveExceptionMetric|从注册表中删除指定的指标。|
|RemoveAllExceptionMetrics|从注册表中删除所有异常指标。|

## <a name="symbol-provider-functions"></a>符号提供程序函数

|函数|说明|
|--------------|-----------------|
|GetSPMetric|从注册表检索指标值。|
|SetSPMetric|在注册表中设置指定的指标值。|
|RemoveSPMetric|从注册表中删除指定的指标。|

## <a name="enumeration-functions"></a>枚举函数

|函数|说明|
|--------------|-----------------|
|EnumMetricSections|枚举指定指标类型的所有指标。|
|EnumDebugEngine|枚举已注册的调试引擎。|
|EnumEEs|枚举已注册的表达式计算器。|
|EnumExceptionMetrics|枚举所有异常指标。|

## <a name="metric-definitions"></a>指标定义
 这些定义可用于预定义的指标名称。 名称对应于各种注册表项和值名称，并且都定义为宽字符字符串：例如 `extern LPCWSTR metrictypeEngine` 。

|预定义指标类型|说明：的基本键 ...。|
|-----------------------------|---------------------------------------|
|metrictypeEngine|所有调试引擎指标。|
|metrictypePortSupplier|所有端口供应商指标。|
|metrictypeException|所有异常指标。|
|metricttypeEEExtension|所有表达式计算器扩展。|

|调试引擎属性|说明|
|-----------------------------|-----------------|
|metricAddressBP|设置为非零值表示支持地址断点。|
|metricAlwaysLoadLocal|设置为非零值，以便始终在本地加载调试引擎。|
|metricLoadInDebuggeeSession|未使用|
|metricLoadedByDebuggee|设置为非零值表示将始终使用或正在调试的程序加载调试引擎。|
|metricAttach|如果设置为非零，则表示支持对现有程序的附件。|
|metricCallStackBP|设置为非零值表示支持调用堆栈断点。|
|metricConditionalBP|设置为非零值表示支持条件断点的设置。|
|metricDataBP|设置为非零值，表示支持对数据更改进行断点设置。|
|metricDisassembly|设置为非零值表示支持拆装列表。|
|metricDumpWriting|设置为非零值，表示支持转储写入 (将内存转储到输出设备) 。|
|metricENC|设置为非零值表示支持 "编辑并继续"。 **注意：**  自定义调试引擎绝不应设置此设置，否则应始终将其设置为0。|
|metricExceptions|设置为非零值表示支持异常。|
|metricFunctionBP|如果设置为非零，则表示支持已命名的断点 (在) 指定某个函数名称时中断的断点。|
|metricHitCountBP|设置为非零值，以指示支持 "点击点" 断点 (仅在达到特定次数) 时触发的断点。|
|metricJITDebug|如果设置为非零，则表示支持实时调试 (调试程序在运行的进程) 中发生异常时启动。|
|metricMemory|未使用|
|metricPortSupplier|如果实现，则将此项设置为端口供应商的 CLSID。|
|metricRegisters|未使用|
|metricSetNextStatement|如果设置为非零，则表示支持设置下一个语句 (这将跳过中间语句的执行) 。|
|metricSuspendThread|设置为非零值以指示支持挂起线程执行。|
|metricWarnIfNoSymbols|如果设置为非零，则指示在没有符号时应通知用户。|
|metricProgramProvider|将此设置为程序提供程序的 CLSID。|
|metricAlwaysLoadProgramProviderLocal|将此值设置为非零值，以指示应始终在本地加载程序提供程序。|
|metricEngineCanWatchProcess|将此值设置为非零值，以指示调试引擎将监视进程事件而不是程序提供程序。|
|metricRemoteDebugging|将此值设置为非零表示支持远程调试。|
|metricEncUseNativeBuilder|将此值设置为非零值，表示 "编辑并继续" 管理器应该使用调试引擎的 encbuild.dll 来生成以进行 "编辑并继续"。 **注意：**  自定义调试引擎绝不应设置此设置，否则应始终将其设置为0。|
|metricLoadUnderWOW64|将此项设置为非零值，指示调试引擎应在调试64位进程时在 WOW 下的调试对象进程中加载;否则，将在 (在 WOW64) 下运行的 Visual Studio 进程中加载调试引擎。|
|metricLoadProgramProviderUnderWOW64|将此项设置为非零值，表示当调试 WOW 下的64位进程时，应在调试对象进程中加载程序提供程序。否则，它将加载到 Visual Studio 进程中。|
|metricStopOnExceptionCrossingManagedBoundary|将此值设置为非零值，以指示当跨托管/非托管代码边界引发未经处理的异常时，进程应停止。|
|metricAutoSelectPriority|将此项设置为自动选择调试引擎的优先级 (较高的值等于较高的优先级) 。|
|metricAutoSelectIncompatibleList|包含一些项的注册表项，这些项指定要在自动选择中忽略的调试引擎的 Guid。 这些项是 (0、1、2等) ，并以字符串形式表示的 GUID。|
|metricIncompatibleList|包含一些项的注册表项，这些项指定与此调试引擎不兼容的调试引擎的 Guid。|
|metricDisableJITOptimization|将此项设置为非零值，以指示应在调试过程中禁用托管代码) 的实时优化 (。|

|表达式计算器属性|说明|
|-------------------------------------|-----------------|
|metricEngine|这会保留支持指定表达式计算器的调试引擎的数量。|
|metricPreloadModules|将此值设置为非零值，指示在对程序启动表达式计算器时应预加载模块。|
|metricThisObjectName|将此设置为 "this" 对象名称。|

|表达式计算器扩展属性|说明|
| - |-----------------|
|metricExtensionDll|支持此扩展的 dll 的名称。|
|metricExtensionRegistersSupported|支持的寄存器列表。|
|metricExtensionRegistersEntryPoint|用于访问寄存器的入口点。|
|metricExtensionTypesSupported|支持的类型列表。|
|metricExtensionTypesEntryPoint|用于访问类型的入口点。|

|端口供应商属性|说明|
|------------------------------|-----------------|
|metricPortPickerCLSID|端口选取器的 CLSID (一个对话框，用户可以使用该对话框选择端口并添加用于调试) 的端口。|
|metricDisallowUserEnteredPorts|如果无法将用户输入的端口添加到端口供应商，则为非零值 (这会使端口选取器对话框本质上是只读的) 。|
|metricPidBase|分配进程 Id 时端口提供程序使用的基本进程 ID。|

|预定义的 SP 存储类型|说明|
|-------------------------------|-----------------|
|storetypeFile|符号存储在单独的文件中。|
|storetypeMetadata|符号作为元数据存储在程序集中。|

|其他属性|说明|
|------------------------------|-----------------|
|metricShowNonUserCode|将此值设置为非零值将显示 nonuser 代码。|
|metricJustMyCodeStepping|将此项设置为非零值，以指示单步执行只能在用户代码中进行。|
|metricCLSID|特定指标类型的对象的 CLSID。|
|metricName|特定指标类型的对象的用户友好名称。|
|metricLanguage|语言名称。|

## <a name="registry-locations"></a>注册表位置
 将从注册表中读取并写入到注册表中，特别是在 `VisualStudio` 子项中。

> [!NOTE]
> 大多数情况下，度量值将写入 HKEY_LOCAL_MACHINE 键。 但是，有时 HKEY_CURRENT_USER 将是目标键。 Dbgmetric 处理这两个键。 获取度量值时，将先搜索 HKEY_CURRENT_USER，然后 HKEY_LOCAL_MACHINE。 设置度量值时，参数指定要使用的顶级键。

 *[注册表项]*\

 `Software`\

 `Microsoft`\

 `VisualStudio`\

 *[版本根目录]*\

 *[指标根]*\

 *[指标类型]*\

 *[指标] = [指标值]*

 *[指标] = [指标值]*

 *[指标] = [指标值]*

|占位符|说明|
|-----------------|-----------------|
|*[注册表项]*|`HKEY_CURRENT_USER` 或 `HKEY_LOCAL_MACHINE`。|
|*[版本根目录]*|Visual Studio 的版本 (例如，、 `7.0` `7.1` 或 `8.0`) 。 不过，还可以使用 **/rootsuffix** 开关来修改此根 **devenv.exe**。 对于 VSIP，此修饰符通常为 **Exp**，因此版本 root 为，例如 8.0 Exp。|
|*[指标根]*|此为 `AD7Metrics` 或 `AD7Metrics(Debug)` ，具体取决于是否使用 dbgmetric 的调试版本。 **注意：**  无论是否使用 dbgmetric，如果必须在注册表中反映的调试版本和发布版本之间存在差异，则应遵守此命名约定。|
|*[指标类型]*|要写入的度量类型： `Engine` 、 `ExpressionEvaluator` 、 `SymbolProvider` 等。这些都是在 dbgmetric 中定义为 `metricTypeXXXX` ，其中 `XXXX` 是特定的类型名称。|
|*跃*|要为其分配值以便设置指标的项的名称。 指标的实际组织取决于指标类型。|
|*[指标值]*|分配给度量值的值。 值应具有 (字符串、数字等 ) 取决于指标。|

> [!NOTE]
> 所有 Guid 都以的格式存储 `{GUID}` 。 例如，`{123D150B-FA18-461C-B218-45B3E4589F9B}`。

### <a name="debug-engines"></a>调试引擎
 下面是注册表中调试引擎指标的组织。 `Engine` 是调试引擎的度量类型名称，并且对应于上述注册表子树中的 *[指标类型]* 。

 `Engine`\

 *[引擎 guid]*\

 `CLSID` = *[类 guid]*

 *[指标] = [指标值]*

 *[指标] = [指标值]*

 *[指标] = [指标值]*

 `PortSupplier`\

 `0` = *[端口供应商 guid]*

 `1` = *[端口供应商 guid]*

|占位符|说明|
|-----------------|-----------------|
|*[引擎 guid]*|调试引擎的 GUID。|
|*[类 guid]*|实现此调试引擎的类的 GUID。|
|*[端口供应商 guid]*|端口供应商的 GUID （如果有）。 许多调试引擎使用默认端口供应商，因此不指定其自己的供应商。 在这种情况下，子项 `PortSupplier` 将不存在。|

### <a name="port-suppliers"></a>端口提供程序
 下面是注册表中端口供应商指标的组织。 `PortSupplier` 端口供应商的度量类型名称，并且对应于 *[指标类型]*。

 `PortSupplier`\

 *[端口供应商 guid]*\

 `CLSID` = *[类 guid]*

 *[指标] = [指标值]*

 *[指标] = [指标值]*

|占位符|说明|
|-----------------|-----------------|
|*[端口供应商 guid]*|端口供应商的 GUID|
|*[类 guid]*|实现此端口提供程序的类的 GUID|

### <a name="symbol-providers"></a>符号提供程序
 下面是注册表中符号供应商指标的组织。 `SymbolProvider` 符号提供程序的度量类型名称，并且对应于 *[度量值类型]*。

 `SymbolProvider`\

 *[符号提供程序 guid]*\

 `file`\

 `CLSID` = *[类 guid]*

 *[指标] = [指标值]*

 *[指标] = [指标值]*

 `metadata`\

 `CLSID` = *[类 guid]*

 *[指标] = [指标值]*

 *[指标] = [指标值]*

|占位符|说明|
|-----------------|-----------------|
|*[符号提供程序 guid]*|符号提供程序的 GUID|
|*[类 guid]*|实现此符号提供程序的类的 GUID|

### <a name="expression-evaluators"></a>表达式计算器
 下面是注册表中表达式计算器度量值的组织。 `ExpressionEvaluator` 表达式计算器的度量类型名称并对应于 *[度量值类型]*。

> [!NOTE]
> `ExpressionEvaluator`Dbgmetric 中未定义的度量值类型，因为假定表达式计算器的所有指标更改都将通过相应的表达式计算器度量函数 `ExpressionEvaluator` （ (子项布局有点复杂，因此详细信息隐藏在 dbgmetric) 内。

 `ExpressionEvaluator`\

 *[language guid]*\

 *[供应商 guid]*\

 `CLSID` = *[类 guid]*

 *[指标] = [指标值]*

 *[指标] = [指标值]*

 `Engine`\

 `0` = *[调试引擎 guid]*

 `1` = *[调试引擎 guid]*

|占位符|说明|
|-----------------|-----------------|
|*[language guid]*|语言的 GUID|
|*[供应商 guid]*|供应商的 GUID|
|*[类 guid]*|实现此表达式计算器的类的 GUID|
|*[调试引擎 guid]*|此表达式计算器使用的调试引擎的 GUID|

### <a name="expression-evaluator-extensions"></a>表达式计算器扩展
 下面是注册表中表达式计算器扩展指标的组织。 `EEExtensions` 表达式计算器扩展的度量类型名称，并且对应于 *[指标类型]*。

 `EEExtensions`\

 *[extension guid]*\

 *[指标] = [指标值]*

 *[指标] = [指标值]*

|占位符|说明|
|-----------------|-----------------|
|*[extension guid]*|表达式计算器扩展的 GUID|

### <a name="exceptions"></a>例外
 下面是注册表中例外指标的组织。 `Exception` 异常的度量类型名称，并且对应于 *[指标类型]*。

 `Exception`\

 *[调试引擎 guid]*\

 *[异常类型]*\

 *异常*\

 *[指标] = [指标值]*

 *[指标] = [指标值]*

 *异常*\

 *[指标] = [指标值]*

 *[指标] = [指标值]*

|占位符|说明|
|-----------------|-----------------|
|*[调试引擎 guid]*|支持异常的调试引擎的 GUID。|
|*[异常类型]*|子项的一般标题，用于标识可处理的异常类。 典型名称为 **c + + 异常**、 **Win32 异常**、 **公共语言运行时异常**和 **本机运行时检查**。 这些名称还用于向用户标识特定的异常类。|
|*异常*|异常的名称：例如， **_com_error** 或 **控制中断**。 这些名称还用于向用户标识特定异常。|

## <a name="requirements"></a>要求
 [!INCLUDE[vs_dev10_ext](../../../extensibility/debugger/reference/includes/vs_dev10_ext_md.md)]默认情况下，这些文件位于 SDK 安装目录中 (*[drive]* \Program Files\Microsoft VISUAL Studio 2010 SDK \\) 。

 标头： includes\dbgmetric。h

 库： libs\ad2de.lib、libs\dbgmetric.lib

## <a name="see-also"></a>另请参阅
- [API 参考](../../../extensibility/debugger/reference/api-reference-visual-studio-debugging.md)
