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
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 74b9047ef6df1e6bf20a5b5a95e40e27ed1b1926
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66329211"
---
# <a name="sdk-helpers-for-debugging"></a>用于调试的 SDK 帮助程序
这些函数和声明是全局的 helper 函数，用于实现的调试引擎中，表达式计算器和符号中的提供程序C++。

> [!NOTE]
> 此时没有上述函数和声明的托管的版本。

## <a name="overview"></a>概述
 为了使用由 Visual Studio 的调试引擎中，表达式计算器和符号提供程序，必须在注册它们。 这是通过设置注册表子项和注册表项，也称为"度量值设置。" 以下全局函数旨在简化更新这些度量值的过程。 在注册表位置来找出这些函数更新每个注册表子项的布局，请参阅部分。

## <a name="general-metric-functions"></a>通用指标函数
 这些是使用的调试引擎的常规函数。 表达式计算器的专用函数和符号提供程序后面详细说明。

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

|参数|描述|
|---------------|-----------------|
|pszMachine|[in]将写入其注册的可能是远程计算机的名称 (`NULL`表示本地计算机)。|
|pszType|[in]指标类型之一。|
|guidSection|[in]特定的引擎、 计算器、 异常等的 GUID。这会指定一个子节下的特定元素的指标类型。|
|pszMetric|[in]若要获取度量值。 这对应于一个特定值名称。|
|pdwValue|[in]该度量值中的值的存储位置。 有几种 GetMetric 可以返回一个 dword 值 （如本例所示）、 BSTR、 GUID 或 Guid 的数组。|
|pszAltRoot|[in]若要使用备用的注册表根。 设置为`NULL`若要使用默认值。|

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

|参数|描述|
|---------------|-----------------|
|pszType|[in]指标类型之一。|
|guidSection|[in]特定的引擎、 计算器、 异常等的 GUID。这会指定一个子节下的特定元素的指标类型。|
|pszMetric|[in]若要获取度量值。 这对应于一个特定值名称。|
|dwValue|[in]该度量值中的值的存储位置。 有几种 SetMetric 可以存储一个 dword 值，（在此示例中）、 BSTR、 GUID 或 Guid 的数组。|
|fUserSpecific|[in]如果该度量值是特定于用户的并且应写入而不是本地计算机单元的用户的配置单元，则为 TRUE。|
|pszAltRoot|[in]若要使用备用的注册表根。 设置为`NULL`若要使用默认值。|

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

|参数|描述|
|---------------|-----------------|
|pszType|[in]指标类型之一。|
|guidSection|[in]特定的引擎、 计算器、 异常等的 GUID。这会指定一个子节下的特定元素的指标类型。|
|pszMetric|[in]要删除度量值。 这对应于一个特定值名称。|
|pszAltRoot|[in]若要使用备用的注册表根。 设置为`NULL`若要使用默认值。|

### <a name="enummetricsections-method"></a>EnumMetricSections 方法
 枚举注册表中的各个指标部分。

```cpp
HRESULT EnumMetricSections(
   LPCWSTR pszMachine,
   LPCWSTR pszType,
   GUID *  rgguidSections,
   DWORD * pdwSize,
   LPCWSTR pszAltRoot
);
```

|参数|描述|
|---------------|-----------------|
|pszMachine|[in]将写入其注册的可能是远程计算机的名称 (`NULL`表示本地计算机)。|
|pszType|[in]指标类型之一。|
|rgguidSections|[in、 out]预先分配的 Guid 的数组填充。|
|pdwSize|[in]可以存储在 Guid 的最大数目`rgguidSections`数组。|
|pszAltRoot|[in]若要使用备用的注册表根。 设置为`NULL`若要使用默认值。|

## <a name="expression-evaluator-functions"></a>表达式计算器函数

|函数|描述|
|--------------|-----------------|
|GetEEMetric|从注册表检索指标值。|
|SetEEMetric|在注册表中设置指定的指标值。|
|RemoveEEMetric|从注册表中删除指定的指标。|
|GetEEMetricFile|获取文件名称从指定的指标并将数据加载，以字符串形式返回文件内容。|

## <a name="exception-functions"></a>异常函数

|函数|描述|
|--------------|-----------------|
|GetExceptionMetric|从注册表检索指标值。|
|SetExceptionMetric|在注册表中设置指定的指标值。|
|RemoveExceptionMetric|从注册表中删除指定的指标。|
|RemoveAllExceptionMetrics|从注册表中删除所有异常指标。|

## <a name="symbol-provider-functions"></a>符号提供程序函数

|函数|描述|
|--------------|-----------------|
|GetSPMetric|从注册表检索指标值。|
|SetSPMetric|在注册表中设置指定的指标值。|
|RemoveSPMetric|从注册表中删除指定的指标。|

## <a name="enumeration-functions"></a>枚举函数

|函数|描述|
|--------------|-----------------|
|EnumMetricSections|枚举用于指定的指标类型的所有度量值。|
|EnumDebugEngine|枚举已注册的调试引擎。|
|EnumEEs|枚举已注册的表达式计算器。|
|EnumExceptionMetrics|枚举所有异常指标。|

## <a name="metric-definitions"></a>指标定义
 这些定义可用于预定义的指标名称。 名称对应于各种注册表项和值的名称和这些都是定义为宽字符字符串： 例如， `extern LPCWSTR metrictypeEngine`。

|预定义的指标类型|描述：有关基项...|
|-----------------------------|---------------------------------------|
|metrictypeEngine|所有调试引擎指标。|
|metrictypePortSupplier|所有端口供应商指标。|
|metrictypeException|所有异常指标。|
|metricttypeEEExtension|所有表达式计算器扩展。|

|调试引擎属性|描述|
|-----------------------------|-----------------|
|metricAddressBP|设置为非零值，指示支持地址断点。|
|metricAlwaysLoadLocal|设置为非零值，以便始终加载本地调试引擎。|
|metricLoadInDebuggeeSession|不使用|
|metricLoadedByDebuggee|设置为非零值，指示使用或由正在调试的程序，将始终加载调试引擎。|
|metricAttach|设置为非零值，指示为附加到的现有程序的支持。|
|metricCallStackBP|设置为非零值，指示对调用堆栈断点的支持。|
|metricConditionalBP|设置为非零值，指示对条件断点的设置的支持。|
|metricDataBP|设置为非零值，指示对数据中的更改上的断点的设置的支持。|
|metricDisassembly|设置为非零值，指示对反汇编列表的生产环境的支持。|
|metricDumpWriting|设置为非零值，指示对转储写入 （转储到输出设备的内存） 的支持。|
|metricENC|设置为非零值来表明支持编辑并继续。 **注意：** 自定义调试引擎应永远不会将此设置，或应始终将其设置为 0。|
|metricExceptions|设置为非零值，指示对异常的支持。|
|metricFunctionBP|设置为非零值，指示对命名断点 （中断调用特定函数名称时的断点） 的支持。|
|metricHitCountBP|设置为非零值，指示对"射击点"断点 （仅在命中一定次数后触发断点） 的设置的支持。|
|metricJITDebug|设置为非零值，指示用于在实时调试 （当正在运行的进程中发生异常时，将启动调试器） 的支持。|
|metricMemory|不使用|
|metricPortSupplier|设置为端口提供程序的 CLSID 如果实现了一个。|
|metricRegisters|不使用|
|metricSetNextStatement|设置为非零值，指示对设置的下一个语句 （它将跳过中间语句的执行） 的支持。|
|metricSuspendThread|设置为非零值，指示对挂起线程执行的支持。|
|metricWarnIfNoSymbols|设置为非零值，指示没有符号是否应通知用户。|
|metricProgramProvider|将此设置为程序提供程序的 CLSID。|
|metricAlwaysLoadProgramProviderLocal|将此设置为非零值，表明程序提供程序应始终将加载本地。|
|metricEngineCanWatchProcess|将此设置为非零值，指示调试引擎将处理事件而不是程序提供程序的监视。|
|metricRemoteDebugging|将此设置为非零值，指示对远程调试的支持。|
|metricEncUseNativeBuilder|将此设置为非零值，指示编辑并继续管理器应使用调试引擎 encbuild.dll 编辑并继续生成。 **注意：** 自定义调试引擎应永远不会将此设置，或应始终将其设置为 0。|
|metricLoadUnderWOW64|将此设置为非零值，指示当调试 64 位进程; 调试引擎，应在 WOW 下调试对象进程中加载否则，将在 Visual Studio 过程 （这在 WOW64 下运行的） 加载调试引擎。|
|metricLoadProgramProviderUnderWOW64|将此设置为非零值，指示程序提供程序应在调试对象进程中加载时调试 64 位进程在 WOW;否则，它将在 Visual Studio 进程中加载。|
|metricStopOnExceptionCrossingManagedBoundary|将此设置为非零值，指示跨托管/非托管代码边界引发未处理的异常，应停止该过程。|
|metricAutoSelectPriority|将此设置为自动选择调试引擎 （优先级更高的值等于更高版本） 的优先级。|
|metricAutoSelectIncompatibleList|其中包含指定 Guid 的调试引擎忽略中自动选择的项的注册表项。 这些条目是一个数字 （0、 1、 2，依此类推） 使用 GUID 表示为字符串。|
|metricIncompatibleList|其中包含指定的 Guid 与此调试引擎不兼容的调试引擎的项的注册表项。|
|metricDisableJITOptimization|将此设置为非零值，指示应在调试期间禁用 （适用于托管代码） 中实时优化。|

|表达式计算器属性|描述|
|-------------------------------------|-----------------|
|metricEngine|它将保存的调试引擎支持指定的表达式计算器的数量。|
|metricPreloadModules|将此设置为非零值，指示模块应预加载，针对程序启动后的表达式计算器。|
|metricThisObjectName|将此设置为"this"对象名称。|

|表达式计算器的扩展属性|描述|
| - |-----------------|
|metricExtensionDll|支持此扩展 dll 的名称。|
|metricExtensionRegistersSupported|支持的寄存器列表。|
|metricExtensionRegistersEntryPoint|用于访问寄存器的入口点。|
|metricExtensionTypesSupported|支持的类型的列表。|
|metricExtensionTypesEntryPoint|访问类型的入口点。|

|端口供应商属性|描述|
|------------------------------|-----------------|
|metricPortPickerCLSID|（一个对话框，用户可以使用选择的端口，并添加要用于调试的端口） 端口选取器的 CLSID。|
|metricDisallowUserEnteredPorts|如果用户输入的端口不能添加到端口提供程序，非零值 （实质上是只读的这使得端口选取器对话框）。|
|metricPidBase|基本进程 ID 分配进程 Id 时使用的端口提供程序。|

|预定义的 SP 存储类型|描述|
|-------------------------------|-----------------|
|storetypeFile|符号存储在一个单独的文件中。|
|storetypeMetadata|符号存储为程序集中的元数据。|

|其他属性|描述|
|------------------------------|-----------------|
|metricShowNonUserCode|将此设置为非零值，显示非代码。|
|metricJustMyCodeStepping|将此设置为非零值，指示单步执行，可以仅在用户代码中。|
|metricCLSID|特定的指标类型的对象的的 CLSID。|
|metricName|特定的指标类型的对象的用户友好名称。|
|metricLanguage|语言名称。|

## <a name="registry-locations"></a>注册表位置
 指标是从读取和写入到注册表中，特别是在`VisualStudio`子项。

> [!NOTE]
> 大多数情况下，度量值将写入到 HKEY_LOCAL_MACHINE 项。 但是，有时 HKEY_CURRENT_USER 将是目标项。 Dbgmetric.lib 处理这两个密钥。 度量值时，它将搜索 HKEY_CURRENT_USER 中，然后 HKEY_LOCAL_MACHINE。 它会将设置度量值，当参数指定要使用哪个顶级密钥。

 *[registry key]* \

 `Software`\

 `Microsoft`\

 `VisualStudio`\

 *[版本根]* \

 *[指标根]* \

 *[metric type]* \

 *[metric] = [metric value]*

 *[metric] = [metric value]*

 *[metric] = [metric value]*

|占位符|描述|
|-----------------|-----------------|
|*[registry key]*|`HKEY_CURRENT_USER` 或 `HKEY_LOCAL_MACHINE`。|
|*[版本根]*|Visual Studio 的版本 (例如， `7.0`， `7.1`，或`8.0`)。 但是，此根目录还可以修改使用 **/rootsuffix**切换到**devenv.exe**。 VSIP，对于此修饰符通常是**Exp**，因此，则版本根将是，例如，8.0Exp。|
|*[指标根]*|这可以是`AD7Metrics`或`AD7Metrics(Debug)`，取决于是否使用 dbgmetric.lib 的调试版本。 **注意：** 指示是否使用 dbgmetric.lib 时，此命名约定应遵守如果必须调试和发布之间的差异必须反映在注册表中的版本。|
|*[metric type]*|要写入的度量值的类型： `Engine`， `ExpressionEvaluator`， `SymbolProvider`，等等。这些都被定义为如下所示为 dbgmetric.h `metricTypeXXXX`，其中`XXXX`是特定类型名称。|
|*[metric]*|要将分配一个值，以便将跃点设置的项的名称。 度量值的实际组织取决于指标类型。|
|*[metric value]*|分配给该度量值的值。 应具有的值 （字符串、 数字等） 的类型取决于该度量值。|

> [!NOTE]
> 格式存储所有 Guid `{GUID}`。 例如 `{123D150B-FA18-461C-B218-45B3E4589F9B}`。

### <a name="debug-engines"></a>调试引擎
 以下是在注册表中的调试引擎指标的组织。 `Engine` 调试引擎的指标类型名称和对应于 *[指标类型]* 上述注册表子树中。

 `Engine`\

 *[引擎 guid]* \

 `CLSID` =  *[类 guid]*

 *[metric] = [metric value]*

 *[metric] = [metric value]*

 *[metric] = [metric value]*

 `PortSupplier`\

 `0` =  *[端口供应商 guid]*

 `1` =  *[端口供应商 guid]*

|占位符|描述|
|-----------------|-----------------|
|*[引擎 guid]*|调试引擎的 GUID。|
|*[class guid]*|实现此调试引擎的类的 GUID。|
|*[端口供应商 guid]*|端口提供程序，如果有的 GUID。 许多的调试引擎使用默认端口提供程序，并因此不指定其自己的供应商。 在此情况下，该子项`PortSupplier`将不会出现。|

### <a name="port-suppliers"></a>端口提供程序
 以下是在注册表中的端口供应商指标的组织。 `PortSupplier` 是端口提供程序的指标类型名称，对应于 *[指标类型]* 。

 `PortSupplier`\

 *[端口供应商 guid]* \

 `CLSID` =  *[类 guid]*

 *[metric] = [metric value]*

 *[metric] = [metric value]*

|占位符|描述|
|-----------------|-----------------|
|*[端口供应商 guid]*|端口提供程序的 GUID|
|*[class guid]*|实现此端口提供程序的类的 GUID|

### <a name="symbol-providers"></a>符号提供程序
 以下是在注册表中的符号供应商指标的组织。 `SymbolProvider` 是符号提供程序的指标类型名称，对应于 *[指标类型]* 。

 `SymbolProvider`\

 *[符号提供程序 guid]* \

 `file`\

 `CLSID` =  *[类 guid]*

 *[metric] = [metric value]*

 *[metric] = [metric value]*

 `metadata`\

 `CLSID` =  *[类 guid]*

 *[metric] = [metric value]*

 *[metric] = [metric value]*

|占位符|描述|
|-----------------|-----------------|
|*[符号提供程序 guid]*|符号提供程序的 GUID|
|*[class guid]*|实现此符号提供程序的类的 GUID|

### <a name="expression-evaluators"></a>表达式计算器
 以下是在注册表中的表达式计算器指标的组织。 `ExpressionEvaluator` 表达式计算器的指标类型名称和对应于 *[指标类型]* 。

> [!NOTE]
> 指标类型`ExpressionEvaluator`未定义在 dbgmetric.h，因为它假定所有度量值更改为表达式计算器将经过适当的表达式计算器指标函数 (的布局`ExpressionEvaluator`子项是某种程度上很复杂，因此详细信息隐藏在 dbgmetric.lib）。

 `ExpressionEvaluator`\

 *[语言 guid]* \

 *[vendor guid]* \

 `CLSID` =  *[类 guid]*

 *[metric] = [metric value]*

 *[metric] = [metric value]*

 `Engine`\

 `0` =  *[调试引擎 guid]*

 `1` =  *[调试引擎 guid]*

|占位符|描述|
|-----------------|-----------------|
|*[language guid]*|一种语言的 GUID|
|*[vendor guid]*|供应商的 GUID|
|*[class guid]*|实现此表达式计算器的类的 GUID|
|*[调试引擎 guid]*|此表达式计算器适用于调试引擎的 GUID|

### <a name="expression-evaluator-extensions"></a>表达式计算器扩展
 以下是在注册表中的表达式计算器扩展指标的组织。 `EEExtensions` 是计算器扩展的表达式的度量值的类型名称，对应于 *[指标类型]* 。

 `EEExtensions`\

 *[扩展 guid]* \

 *[metric] = [metric value]*

 *[metric] = [metric value]*

|占位符|描述|
|-----------------|-----------------|
|*[扩展 guid]*|表达式计算器扩展的 GUID|

### <a name="exceptions"></a>Exceptions
 以下是在注册表中的异常度量值的组织。 `Exception` 是异常的指标类型名称，对应于 *[指标类型]* 。

 `Exception`\

 *[调试引擎 guid]* \

 *[异常类型]* \

 *[exception]* \

 *[metric] = [metric value]*

 *[metric] = [metric value]*

 *[exception]* \

 *[metric] = [metric value]*

 *[metric] = [metric value]*

|占位符|描述|
|-----------------|-----------------|
|*[调试引擎 guid]*|支持异常的调试引擎的 GUID。|
|*[exception types]*|子项标识可以处理的异常的类的一个常规标题。 典型的名称是**C++异常**， **Win32 异常**，**公共语言运行时异常**，并**本机运行时检查**. 这些名称也用于标识特定类别的用户的例外。|
|*[exception]*|异常的名称： 例如， **_com_error**或**控制中断**。 这些名称还用于确定向用户特定异常。|

## <a name="requirements"></a>要求
 这些文件位于[!INCLUDE[vs_dev10_ext](../../../extensibility/debugger/reference/includes/vs_dev10_ext_md.md)]SDK 安装目录 (默认情况下 *[驱动器]* \Program Files\Microsoft Visual Studio 2010 SDK\\)。

 标头： includes\dbgmetric.h

 库： libs\ad2de.lib、 libs\dbgmetric.lib

## <a name="see-also"></a>请参阅
- [API 参考](../../../extensibility/debugger/reference/api-reference-visual-studio-debugging.md)