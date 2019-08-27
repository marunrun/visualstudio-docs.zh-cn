---
title: “选项”页 ->“调试”节点属性 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
ms.assetid: 564cc8b2-0084-420e-b560-200cc5621a7e
caps.latest.revision: 13
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: bd02ae0c3cd9f05e817e335b942a76c849655e44
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65674733"
---
# <a name="options-page-debugging-node-properties"></a>“选项”页 ->“调试”节点属性
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

下表描述了与“选项”对话框的“调试”类别 `DTE.Properties("Debugging", <Property Page>)` 关联的页面（或属性集合）。  
  
## <a name="general"></a>常规  
 `DTE.Properties("Debugging", "General")`  
  
|属性项名称|值|说明|  
|------------------------|-----------|-----------------|  
|PromptOnBreakpointDelete|Get/Set (Boolean)|确定调试器是否在删除项目中的所有断点之前请示授权。|  
|BreakAllProcesses|Get/Set (Boolean)|确定调试器是否在单个进程中断时中断所有进程。|  
|BreakAtBoundaries|Get/Set (Boolean)|确定当异常跨越 AppDomains 之间或托管代码和本机代码之间的边框时，调试器是否中断执行。|  
|EnableAddressLevelDebugging|Get/Set (Boolean)|确定是否启用地址级调试功能。|  
|ShowDisassemblyIfNoSource|Get/Set (Boolean)|确定调试器是否在源代码不可用时显示反汇编代码。|  
|EnableBreakpointFilters|Get/Set (Boolean)|确定是否启用断点筛选。|  
|EnableExceptionAssistant|Get/Set (Boolean)|确定是否将异常情况助手用于托管的异常。|  
|UnwindCallstack|Get/Set (Boolean)|确定调试器是否为未经处理的异常展开调用堆栈。|  
|EnableJustMyCode|Get/Set (Boolean)|确定是否为 C# 和 Visual Basic 代码启用“仅我的代码”。|  
|ShowAllMembers|Get/Set (Boolean)|对于非用户对象，确定调试器是否在变量窗口中显示所有对象成员。 除非启用“仅我的代码”，否则此选项无效。|  
|WarnIfNoUserCode|Get/Set (Boolean)|确定调试器是否在用户尝试附加到没有用户代码的进程时发出警告。 除非启用“仅我的代码”，否则此选项无效。|  
|EnablePropertyEvaluation|Get/Set (Boolean)|确定调试器是否自动评估托管代码中的属性和隐式函数调用。|  
|CallStringConversion|Get/Set (Boolean)|确定调试器是否对变量窗口中的对象隐式调用字符串转换函数。 此选项仅适用于 C# 和 JScript 代码。|  
|EnableSourceServer|Get/Set (Boolean)|确定调试器是否可以从源服务器访问代码。|  
|PrintSourceServerDiagnostics|Get/Set (Boolean)|确定“输出”窗口是否显示与源服务器相关的诊断消息。 除非启用源服务器访问，否则此选项无效。|  
|HighlightEntireLine|Get/Set (Boolean)|确定调试器是否突出显示断点的整行和当前语句。|  
|RequireSourceToMatch|Get/Set (Boolean)|确定在打开文件进行调试时，调试器是否要求源文件与原始版本完全匹配。|  
|RedirectOutputToImmediate|Get/Set (Boolean)|确定是否将“输出”窗口的输出重定向到“即时”窗口。|  
|ShowRawVariableStructure|Get/Set (Boolean)|确定变量窗口中的对象是否以原始形式显示。|  
|SuppressJitOptimization|Get/Set (Boolean)|对于托管代码，确定调试器是否抑制实时优化。|  
|WarnIfNoSymbols|Get/Set (Boolean)|确定在启动进程后没有调试符号可用的情况下，调试器是否显示警告。|  
|WarnIfScriptDisabled|Get/Set (Boolean)|确定在启动进程后未启用脚本调试的情况下，调试器是否显示警告。|  
|ShowMarkersForAllThreads|Get/Set (Boolean)|确定调试器是否显示线程标记。|  
|StepOverPropertiesAndOperators|Get/Set (Boolean)|指定是否仅在托管代码中跳过属性和运算符。|  
  
## <a name="edit-and-continue"></a>编辑并继续  
 `DTE.Properties("Debugging", "EditAndContinue")`  
  
|属性项名称|值|说明|  
|------------------------|-----------|-----------------|  
|EnableEditAndContinue|Get/Set (Boolean)|确定是否启用“编辑并继续”。 此选项适用于所有支持“编辑并继续”的语言。|  
|InvokedByCommands|Get/Set (Boolean)|确定当用户选择调试命令（例如“单步执行”或“继续”）时，是否自动将“编辑并继续”应用代码更改。 此选项仅适用于本机代码。|  
|InvokedByCommandsAskFirst|Get/Set (Boolean)|确定当用户选择调试命令（例如“单步执行”或“继续”）时，“编辑并继续”是否提示用户授权以应用代码更改。 此选项仅适用于本机代码。|  
|WarnAboutStaleCode|Get/Set (Boolean)|确定当“编辑并继续”导致执行过时或陈旧的代码时，调试器是否发出警告消息。 此选项仅适用于本机代码。|  
|RelinkChangesOnStop|Get/Set (Short)|确定当停止执行应用程序时，Visual Studio 是否重新链接由“编辑并继续”应用的代码更改。 此选项仅适用于本机代码。|  
|AllowPrecompiling|Get/Set (Short)|确定是否允许“编辑并继续”在后台加载预编译标头。 此选项仅适用于本机代码。|  
  
## <a name="just-in-time"></a>实时  
 `DTE.Properties("Debugging", "JustInTime")`  
  
|属性项名称|值|说明|  
|------------------------|-----------|-----------------|  
|JitManaged|Get/Set (Boolean)|确定是否为托管代码启用实时调试。|  
|JitNative|Get/Set (Boolean)|确定是否为本机代码启用实时调试。|  
|JitScript|Get/Set (Boolean)|确定是否为脚本代码启用实时调试。|  
  
## <a name="native"></a>Native  
 `DTE.Properties("Debugging", "Native")`  
  
|属性项名称|值|说明|  
|------------------------|-----------|-----------------|  
|LoadDllExports|Get/Set (Boolean)|确定调试器是否加载 DLL 导出表。|  
|EnableRPC|Get/Set (Boolean)|确定调试器是否可以单步执行 COM 远程过程调用。|  
  
## <a name="see-also"></a>请参阅  
 [控制选项设置](https://msdn.microsoft.com/library/a09ed242-7494-4cde-bbd1-7a8ec617965d)   
 [确定“选项”页中属性项的名称](https://msdn.microsoft.com/library/d450422d-47c7-4eeb-9f9f-3286264bc5aa)   
 [“选项”页 ->“字体和颜色”节点属性](../../ide/reference/options-page-fonts-and-colors-node-properties.md)   
 [“选项”页 ->“文本编辑器”节点属性](../../ide/reference/options-page-text-editor-node-properties.md)   
 [“选项”对话框 ->“调试”->“常规”](../../debugger/general-debugging-options-dialog-box.md)   
 [“选项”对话框 ->“调试”->“编辑并继续”](https://msdn.microsoft.com/library/009d225f-ef65-463f-a146-e4c518f86103)   
 [“选项”对话框 ->“调试”->“实时”](../../debugger/just-in-time-debugging-options-dialog-box.md)
