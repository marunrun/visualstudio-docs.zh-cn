---
title: 核心接口 |微软文档
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- debugging [Debugging SDK], core interfaces
ms.assetid: 666b9116-8550-4bdd-bc15-55fc57de87df
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 8bf01ffceb122ad99d5ecca8fabfaa102a8fc505
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80737577"
---
# <a name="core-interfaces"></a>核心接口
以下接口是使用 扩展调试器的核心接口[!INCLUDE[vsipsdk](../../../extensibility/includes/vsipsdk_md.md)]。

## <a name="discussion"></a>讨论区
 这些接口主要用于创建调试引擎 （DE）。 它们按类别组织在这里：

- [断点](#Breakpoints)

- [上下文](#Contexts)

- [核心服务器](#CoreServer)

- [调试引擎](#DebugEngines)

- [文档](#Documents)

- [事件](#Events)

- [表达式](#Expressions)

- [内存](#Memory)

- [模块](#Modules)

- [港口](#Ports)

- [过程](#Processes)

- [程序](#Programs)

- [属性](#Properties)

- [堆栈帧](#StackFrames)

- [线程](#Threads)

- [类型可视化器](#TypeVisualizers)

  可以实现接口的实体是：

- 调试引擎 （DE）

- 港口供应商 （PS）

- 表达式赋值器 （EE）

- 视觉工作室 （VS）

## <a name="breakpoints"></a><a name="Breakpoints"></a>断点
 这些接口与断点的实现和跟踪相关。

|接口|实施者|描述|
|---------------|--------------------|-----------------|
|[IDebugBoundBreakpoint2](../../../extensibility/debugger/reference/idebugboundbreakpoint2.md)|DE|表示绑定到内存位置的断点。|
|[IDebugBreakpointBoundEvent2](../../../extensibility/debugger/reference/idebugbreakpointboundevent2.md)|DE|当断点绑定到内存位置时，DE 发送。|
|[IDebugBreakpointChecksumRequest2](../../../extensibility/debugger/reference/idebugbreakpointchecksumrequest2.md)|VS|表示断点请求的文档校验和。|
|[IDebugBreakpointErrorEvent2](../../../extensibility/debugger/reference/idebugbreakpointerrorevent2.md)|DE|当断点无法绑定到内存位置时，DE 发送。|
|[IDebugBreakpointEvent2](../../../extensibility/debugger/reference/idebugbreakpointevent2.md)|DE|到达断点时由 DE 发送。|
|[IDebugBreakpointRequest2](../../../extensibility/debugger/reference/idebugbreakpointrequest2.md)|VS|表示断点请求;用于创建挂起的断点。|
|[IDebugBreakpointRequest3](../../../extensibility/debugger/reference/idebugbreakpointrequest3.md)|VS|表示断点请求;用于创建挂起的断点。|
|[IDebugBreakpointResolution2](../../../extensibility/debugger/reference/idebugbreakpointresolution2.md)|DE|表示用于绑定断点的信息。|
|[IDebugBreakpointUnboundEvent2](../../../extensibility/debugger/reference/idebugbreakpointunboundevent2.md)|DE|当断点从内存位置取消绑定时，DE 发送。|
|[IDebugErrorBreakpoint2](../../../extensibility/debugger/reference/idebugerrorbreakpoint2.md)|DE|表示无效的断点（由`IDebugBreakpointErrorEvent2`返回）。|
|[IDebugErrorBreakpointResolution2](../../../extensibility/debugger/reference/idebugerrorbreakpointresolution2.md)|DE|表示有关无效断点的解析信息。|
|[IDebugFunctionPosition2](../../../extensibility/debugger/reference/idebugfunctionposition2.md)|DE|表示设置断点的函数中的位置。|
|[IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)|DE|表示要绑定的断点;用于创建绑定断点。|
|[IEnumDebugBoundBreakpoints2](../../../extensibility/debugger/reference/ienumdebugboundbreakpoints2.md)|DE|表示对一组绑定断点的枚举。|
|[IEnumDebugErrorBreakpoints2](../../../extensibility/debugger/reference/ienumdebugerrorbreakpoints2.md)|DE|表示对一组无法绑定到内存位置的断点进行枚举。|

## <a name="contexts"></a><a name="Contexts"></a>上下文
 这些接口表示正在调试的程序中的各种上下文。

|接口|实施者|描述|
|---------------|--------------------|-----------------|
|[IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)|DE|表示代码指令的起始位置。|
|[IDebugCodeContext3](../../../extensibility/debugger/reference/idebugcodecontext3.md)|DE|扩展[IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)接口，以便检索模块和进程接口。|
|[IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)|VS， 德|表示文档中的位置。|
|[IDebugExpressionContext2](../../../extensibility/debugger/reference/idebugexpressioncontext2.md)|DE|表示在其中计算表达式的上下文。|
|[IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)|DE|表示字节集合内存中的起始位置。|
|[IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)|DE|表示断点或异常处的堆栈帧上下文。|
|[IDebugStackFrame3](../../../extensibility/debugger/reference/idebugstackframe3.md)|DE|表示断点或异常处的堆栈帧上下文。|
|[IEnumDebugCodeContexts2](../../../extensibility/debugger/reference/ienumdebugcodecontexts2.md)|DE|表示对一组代码上下文的枚举。|

## <a name="core-server"></a><a name="CoreServer"></a>核心服务器
 这些接口表示正在调试程序的计算机。 这些由[!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)]调试引擎实现，但可以通过调试引擎调用。

|接口|实施者|描述|
|---------------|--------------------|-----------------|
|[IDebugCoreServer2](../../../extensibility/debugger/reference/idebugcoreserver2.md)|VS|提供对端口和端口供应商的访问以及有关计算机的信息。|
|[IDebugCoreServer3](../../../extensibility/debugger/reference/idebugcoreserver3.md)|VS|表示支持远程调试的[IDebugCoreServer2。](../../../extensibility/debugger/reference/idebugcoreserver2.md)|

## <a name="debug-engines"></a><a name="DebugEngines"></a>调试引擎
 这些接口表示调试引擎及其关联的事件。

|接口|实施者|描述|
|---------------|--------------------|-----------------|
|[IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)|DE|表示自定义调试引擎。|
|[IDebugEngine3](../../../extensibility/debugger/reference/idebugengine3.md)|DE|表示支持加载符号、JustMyCode 和异常的自定义调试引擎。|
|[IDebugEngineCreateEvent2](../../../extensibility/debugger/reference/idebugenginecreateevent2.md)|DE|DE 的每个新实例发送，以指示它已准备好处理调试任务。|
|[IDebugEngineLaunch2](../../../extensibility/debugger/reference/idebugenginelaunch2.md)|DE|表示支持启动程序的自定义调试引擎。|
|[IDebugProgramEngines2](../../../extensibility/debugger/reference/idebugprogramengines2.md)|DE， PS|表示处理多个调试引擎的程序节点。|
|[IDebugQueryEngine2](../../../extensibility/debugger/reference/idebugqueryengine2.md)|DE|为 SDM 提供了一种从线程、程序或堆栈帧获取调试引擎接口的方法。|

## <a name="documents"></a><a name="Documents"></a>文件
 这些接口表示文档（源文件）及其关联元素。

|接口|实施者|描述|
|---------------|--------------------|-----------------|
|[IDebugActivateDocumentEvent2](../../../extensibility/debugger/reference/idebugactivatedocumentevent2.md)|DE|DE 发送以请求打开文档。|
|[IDebugDisassemblyStream2](../../../extensibility/debugger/reference/idebugdisassemblystream2.md)|DE|表示文档中拆解的说明流。|
|[IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md)|VS， 德|表示 DE 提供的文档，指定名称和类 ID （CLSID）。|
|[IDebugDocumentChecksum2](../../../extensibility/debugger/reference/idebugdocumentchecksum2.md)|DE， EE|表示调试文档的校验和，并启用在组件之间传递校验和。|
|[IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)|VS， 德|表示文档上下文，即文档中对应于特定语句和代码上下文的位置。|
|[IDebugDocumentPosition2](../../../extensibility/debugger/reference/idebugdocumentposition2.md)|VS， 德|表示文档中的一般位置。|
|[IDebugDocumentPositionOffset2](../../../extensibility/debugger/reference/idebugdocumentpositionoffset2.md)|VS|将源文件中的位置表示为字符偏移量。|
|[IDebugDocumentText2](../../../extensibility/debugger/reference/idebugdocumenttext2.md)|VS， 德|表示 DE 提供的文本文档（派生自[IDebugDocument2），](../../../extensibility/debugger/reference/idebugdocument2.md)提供实际文本。|
|[IDebugDocumentTextEvents2](../../../extensibility/debugger/reference/idebugdocumenttextevents2.md)|DE|DE 发送以指定对内存中的源文件的更改。|

## <a name="events"></a><a name="Events"></a>事件
 这些接口表示 DE 和会话调试管理器 （SDM） 之间发送的所有事件。

| 接口 | 实施者 | 描述 |
| - |----------------| - |
| [IDebugActivateDocumentEvent2](../../../extensibility/debugger/reference/idebugactivatedocumentevent2.md) | DE | DE 发送以请求打开文档。 |
| [IDebugBeforeSymbolSearchEvent2](../../../extensibility/debugger/reference/idebugbeforesymbolsearchevent2.md) | DE | 调试引擎 （DE） 将此接口发送到会话调试管理器 （SDM）， 以在符号加载期间设置状态栏消息。 |
| [IDebugBreakEvent2](../../../extensibility/debugger/reference/idebugbreakevent2.md) | DE | 当程序中断完成后，DE 发送。 |
| [IDebugBreakpointBoundEvent2](../../../extensibility/debugger/reference/idebugbreakpointboundevent2.md) | DE | 绑定断点时由 DE 发送。 |
| [IDebugBreakpointErrorEvent2](../../../extensibility/debugger/reference/idebugbreakpointerrorevent2.md) | DE | 当断点未绑定时，DE 发送。 |
| [IDebugBreakpointEvent2](../../../extensibility/debugger/reference/idebugbreakpointevent2.md) | DE | 到达断点时由 DE 发送。 |
| [IDebugBreakpointUnboundEvent2](../../../extensibility/debugger/reference/idebugbreakpointunboundevent2.md) | DE | 当断点未绑定时由 DE 发送。 |
| [IDebugCanStopEvent2](../../../extensibility/debugger/reference/idebugcanstopevent2.md) | DE | DE 发送以确定是否应在特定位置停止。 |
| [IDebugDocumentTextEvents2](../../../extensibility/debugger/reference/idebugdocumenttextevents2.md) | DE | DE 发送以指定对内存中的源文件的更改。 |
| [IDebugEngineCreateEvent2](../../../extensibility/debugger/reference/idebugenginecreateevent2.md) | DE | DE 的每个新实例发送，以指示它已准备好处理调试任务。 |
| [IDebugEntryPointEvent2](../../../extensibility/debugger/reference/idebugentrypointevent2.md) | DE | DE 发送以指示正在调试的程序已准备好执行第一个指令。 |
| [IDebugErrorEvent2](../../../extensibility/debugger/reference/idebugerrorevent2.md) | DE | 其他事件接口使用的接口（可能会返回错误）来提供人类可读的错误消息。 |
| [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md) | DE， PS | 从中派生所有其他事件接口的基本接口。 |
| [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) | VS | 表示 SDM 实现的接口，其中事件（表示为实现特定事件接口的对象）发送。 |
| [IDebugExceptionEvent2](../../../extensibility/debugger/reference/idebugexceptionevent2.md) | DE | 当正在调试的程序中出现异常时，DE 发送。 |
| [IDebugExpressionEvaluationCompleteEvent2](../../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2.md) | DE | 当异步表达式计算完成时由 DE 发送。 |
| IDebugFind符号事件2 | | 已过时。 请勿使用。 |
| [IDebugInterceptExceptionCompleteEvent2](../../../extensibility/debugger/reference/idebuginterceptexceptioncompleteevent2.md) | DE | DE 在处理截获的异常时发送。 |
| [IDebugLoadCompleteEvent2](../../../extensibility/debugger/reference/idebugloadcompleteevent2.md) | DE | 当程序完成加载时由 DE 发送。 |
| [IDebugMessageEvent2](../../../extensibility/debugger/reference/idebugmessageevent2.md) | DE | DE 发送给 IDE 向用户显示信息性消息。 |
| [IDebugModuleLoadEvent2](../../../extensibility/debugger/reference/idebugmoduleloadevent2.md) | DE | 当模块加载或卸载时由 DE 发送。 |
| [IDebugNoSymbolsEvent2](../../../extensibility/debugger/reference/idebugnosymbolsevent2.md) | DE | 向[!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)]调试器 UI 发出信号，警告用户无法为启动的可执行文件找到符号。 |
| [IDebugOutputStringEvent2](../../../extensibility/debugger/reference/idebugoutputstringevent2.md) | DE | DE 发送以让 IDE 显示任意字符串。 |
| [IDebugPortEvents2](../../../extensibility/debugger/reference/idebugportevents2.md) | VS， 德 | 由端口发送，用于将端口事件传达给任何侦听器。 |
| [IDebugProcessCreateEvent2](../../../extensibility/debugger/reference/idebugprocesscreateevent2.md) | DE， PS | 创建进程时由 DE 或端口发送。 |
| [IDebugProcessDestroyEvent2](../../../extensibility/debugger/reference/idebugprocessdestroyevent2.md) | DE， PS | 进程被销毁时由 DE 或端口发送。 |
| [IDebugProgramCreateEvent2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md) | DE， PS | 创建程序时由 DE 或端口发送。 |
| [IDebugProgramDestroyEvent2](../../../extensibility/debugger/reference/idebugprogramdestroyevent2.md) | DE， PS | 程序或端口在程序被销毁时发送。 |
| [IDebugProgramDestroyEventFlags2](../../../extensibility/debugger/reference/idebugprogramdestroyeventflags2.md) | DE | 使调试引擎在结束调试会话时覆盖 UI[!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)]的默认行为。 |
| [IDebugProgramNameChangedEvent2](../../../extensibility/debugger/reference/idebugprogramnamechangedevent2.md) | DE | 当程序名称更改时，从调试引擎 （DE） 发送到会话调试管理器 （SDM）。 |
| [IDebugPropertyCreateEvent2](../../../extensibility/debugger/reference/idebugpropertycreateevent2.md) | DE | 创建新属性（由`IDebugProperty2`接口表示）时由 DE 发送。 |
| [IDebugPropertyDestroyEvent2](../../../extensibility/debugger/reference/idebugpropertydestroyevent2.md) | DE | 当属性被销毁时由 DE 发送。 |
| [IDebugReturnValueEvent2](../../../extensibility/debugger/reference/idebugreturnvalueevent2.md) | DE | DE 在退出或超过函数时发送，以便可以正确显示返回值。 |
| [IDebugSettingsCallback2](../../../extensibility/debugger/reference/idebugsettingscallback2.md) | VS | 使调试引擎能够远程读取指标设置。 |
| [IDebugStepCompleteEvent2](../../../extensibility/debugger/reference/idebugstepcompleteevent2.md) | DE | 当进入、结束或退出指令时，DE 发送。 |
| [IDebugSymbolSearchEvent2](../../../extensibility/debugger/reference/idebugsymbolsearchevent2.md) | DE | DE 发送以指示模块加载符号的成败。 |
| [IDebugThreadCreateEvent2](../../../extensibility/debugger/reference/idebugthreadcreateevent2.md) | DE | 创建线程时由 DE 发送。 |
| [IDebugThreadDestroyEvent2](../../../extensibility/debugger/reference/idebugthreaddestroyevent2.md) | DE | 当线程被销毁时由 DE 发送。 |
| [IDebugThreadNameChangedEvent2](../../../extensibility/debugger/reference/idebugthreadnamechangedevent2.md) | DE | 当线程更改其名称时由 DE 发送。 |

## <a name="expressions"></a><a name="Expressions"></a> 表达式
 这些接口表示要在特定上下文中计算的表达式。

|接口|实施者|描述|
|---------------|--------------------|-----------------|
|[IDebugExpression2](../../../extensibility/debugger/reference/idebugexpression2.md)|DE|表示要计算的表达式。 从[IDebugExpressionContext2](../../../extensibility/debugger/reference/idebugexpressioncontext2.md)界面获取。|
|[IDebugExpressionContext2](../../../extensibility/debugger/reference/idebugexpressioncontext2.md)|DE|表示计算表达式的上下文。 从[IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)界面获取。|
|[IDebugExpressionEvaluationCompleteEvent2](../../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2.md)|DE|当异步表达式计算完成时由 DE 发送。|

## <a name="memory"></a><a name="Memory"></a>记忆
 这些接口表示内存中的字节序列。

|接口|实施者|描述|
|---------------|--------------------|-----------------|
|[IDebugMemoryBytes2](../../../extensibility/debugger/reference/idebugmemorybytes2.md)|DE|表示内存中可以从中读取或写入的字节序列。|
|[IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)|DE|表示字节序列的内存中的位置。|

## <a name="modules"></a><a name="Modules"></a>模块
 这些接口表示一个模块，它对应于可执行文件或 。DLL 文件。

|接口|实施者|描述|
|---------------|--------------------|-----------------|
|[IDebugModule2](../../../extensibility/debugger/reference/idebugmodule2.md)|DE|表示单个可执行文件或 DLL。|
|[IDebugModule3](../../../extensibility/debugger/reference/idebugmodule3.md)|DE|表示支持符号的[IDebugModule2。](../../../extensibility/debugger/reference/idebugmodule2.md)|
|[IDebugModuleLoadEvent2](../../../extensibility/debugger/reference/idebugmoduleloadevent2.md)|DE|当模块加载或卸载时由 DE 发送。|
|[IDebugSourceServerModule](../../../extensibility/debugger/reference/idebugsourceservermodule.md)|DE|表示 PDB 文件中的源服务器信息。|
|[IEnumDebugModules2](../../../extensibility/debugger/reference/ienumdebugmodules2.md)|DE|表示[对 IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)已知的一组模块的枚举。|

## <a name="ports"></a><a name="Ports"></a>港口
 这些接口表示端口和端口供应商。

| 接口 | 实施者 | 描述 |
| - |----------------| - |
| [IDebugDefaultPort2](../../../extensibility/debugger/reference/idebugdefaultport2.md) | VS， PS | 表示本地计算机上的默认端口。 |
| [IDebugFirewallConfigurationCallback2](../../../extensibility/debugger/reference/idebugfirewallconfigurationcallback2.md) | VS | 启用使用 DCOM 要求 UI 确保[!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)]防火墙不会阻止远程调试的调试引擎。 |
| [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md) | VS， PS | 表示端口。 |
| [IDebugPortEvents2](../../../extensibility/debugger/reference/idebugportevents2.md) | PS | 由端口发送，用于将端口事件传达给任何侦听器。 |
| [IDebugPortEx2](../../../extensibility/debugger/reference/idebugportex2.md) | PS | 表示可以启动和终止进程的端口。 |
| [IDebugPortNotify2](../../../extensibility/debugger/reference/idebugportnotify2.md) | PS | 用于在端口注册和取消注册程序;允许端口跟踪当前正在调试的程序。 |
| [IDebugPortPicker](../../../extensibility/debugger/reference/idebugportpicker.md) | PS | 表示用于选择端口的自定义 UI。 |
| [IDebugPortRequest2](../../../extensibility/debugger/reference/idebugportrequest2.md) | VS | 表示将创建或定位新端口的端口的请求。 |
| [IDebugPortSupplier2](../../../extensibility/debugger/reference/idebugportsupplier2.md) | PS | 表示端口供应商。 |
| [IDebugPortSupplier3](../../../extensibility/debugger/reference/idebugportsupplier3.md) | PS | 表示可以保留（保存到磁盘）有关其创建的端口的信息的端口供应商。 |
| [IDebugPortSupplierDescription2](../../../extensibility/debugger/reference/idebugportsupplierdescription2.md) | PS | 使[!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)]UI 能够在 **"附加到流程"** 对话框的 **"传输信息**"部分内显示文本。 |
| [IDebugWindowsComputerPort2](../../../extensibility/debugger/reference/idebugwindowscomputerport2.md) | VS | 允许查询有关目标计算机的信息。 |
| [IEnumDebugPorts2](../../../extensibility/debugger/reference/ienumdebugports2.md) | VS， PS | 表示对一组端口的枚举。 |
| [IEnumDebugPortSuppliers2](../../../extensibility/debugger/reference/ienumdebugportsuppliers2.md) | VS | 表示对一组端口供应商的枚举。 |

## <a name="processes"></a><a name="Processes"></a>过程
 这些接口表示进程，一个包含一个或多个程序的可执行文件。

|接口|实施者|描述|
|---------------|--------------------|-----------------|
|[IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)|PS， DE|表示在计算机上运行的进程。|
|[IDebugProcess3](../../../extensibility/debugger/reference/idebugprocess3.md)|PS， DE|表示积极支持调试的进程（用于替换[IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)界面上的步骤、继续和执行方法）。|
|[IDebugProcessCreateEvent2](../../../extensibility/debugger/reference/idebugprocesscreateevent2.md)|DE， PS|创建进程时由 DE 或端口发送。|
|[IDebugProcessDestroyEvent2](../../../extensibility/debugger/reference/idebugprocessdestroyevent2.md)|DE， PS|进程被销毁时由 DE 或端口发送。|
|[IDebugProcessEx2](../../../extensibility/debugger/reference/idebugprocessex2.md)|PS|表示必须跟踪附加到哪个会话的进程。|
|[IEnumDebugProcesses2](../../../extensibility/debugger/reference/ienumdebugprocesses2.md)|PS|表示端口上一组进程的枚举。|

## <a name="programs"></a><a name="Programs"></a>程序
 这些接口表示程序，逻辑执行单元不一定对应于物理可执行文件或模块。

|接口|实施者|描述|
|---------------|--------------------|-----------------|
|[IDebugEngineProgram2](../../../extensibility/debugger/reference/idebugengineprogram2.md)|DE|表示[IDebugProgram2，](../../../extensibility/debugger/reference/idebugprogram2.md)它需要与同时调试的其他程序协同工作。|
|[IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)|DE， PS|表示逻辑执行单元。|
|[IDebugProgramCreateEvent2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md)|DE， PS|创建程序时由 DE 或端口发送。|
|[IDebugProgramDestroyEvent2](../../../extensibility/debugger/reference/idebugprogramdestroyevent2.md)|DE， PS|程序或端口在程序被销毁时发送。|
|[IDebugProgramEngines2](../../../extensibility/debugger/reference/idebugprogramengines2.md)|DE， PS|表示一个[IDebugProgramNode2，](../../../extensibility/debugger/reference/idebugprogramnode2.md)可以由多个调试引擎处理。|
|[IDebugProgramEx2](../../../extensibility/debugger/reference/idebugprogramex2.md)|PS|表示[IDebugProgram2，](../../../extensibility/debugger/reference/idebugprogram2.md)它必须能够跟踪附加到它的会话。|
|[IDebugProgramHost2](../../../extensibility/debugger/reference/idebugprogramhost2.md)|DE， PS|表示[IDebugProgram2，](../../../extensibility/debugger/reference/idebugprogram2.md)它可以返回有关其运行过程的信息。|
|[IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)|DE， PS|表示可以调试的程序。|
|[IDebugProgramNodeAttach2](../../../extensibility/debugger/reference/idebugprogramnodeattach2.md)|DE， PS|允许通知程序节点尝试附加到关联的程序。|
|[IDebugProgramProvider2](../../../extensibility/debugger/reference/idebugprogramprovider2.md)|DE|为 SDM 提供了一种查询 DE 有关该 DE 控制的程序的方法。|
|[IDebugProgramPublisher2](../../../extensibility/debugger/reference/idebugprogrampublisher2.md)|VS|DEs 使用 SDM 注册程序以显示正在调试程序。|
|[IDebugProviderProgramNode2](../../../extensibility/debugger/reference/idebugproviderprogramnode2.md)|DE， PS|表示[IDebugProgramNode2，](../../../extensibility/debugger/reference/idebugprogramnode2.md)它可以跨线程或进程边界封送接口。|
|[IEnumDebugPrograms2](../../../extensibility/debugger/reference/ienumdebugprograms2.md)|DE， PS|表示一组程序的枚举。|

## <a name="properties"></a><a name="Properties"></a> 属性
 这些接口表示属性，与特定上下文关联的值，通常是表达式计算的结果。

|接口|实施者|描述|
|---------------|--------------------|-----------------|
|[IDebugCustomViewer](../../../extensibility/debugger/reference/idebugcustomviewer.md)|EE|表示[IDebugProperty2，](../../../extensibility/debugger/reference/idebugproperty2.md)它可以通过自定义方式显示其值。|
|[IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)|DE|表示堆栈帧、文档或表达式计算的结果的值。|
|[IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)|DE|表示支持任意长字符串的[IDebugProperty2。](../../../extensibility/debugger/reference/idebugproperty2.md)|
|[IDebugPropertyCreateEvent2](../../../extensibility/debugger/reference/idebugpropertycreateevent2.md)|DE|创建新属性（由[IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)接口表示）时由 DE 发送。|
|[IDebugPropertyDestroyEvent2](../../../extensibility/debugger/reference/idebugpropertydestroyevent2.md)|DE|当属性被销毁时由 DE 发送。|
|[IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)|DE|表示对可以存在于任何特定堆栈帧之外的属性的引用。|
|[IEnumDebugPropertyInfo2](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2.md)|DE|表示对一组描述变量、寄存器、参数和表达式[的DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md)结构的枚举。|
|[IEnumDebugReferenceInfo2](../../../extensibility/debugger/reference/ienumdebugreferenceinfo2.md)|DE|表示对一组[DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md)结构的枚举。|

## <a name="stack-frames"></a><a name="StackFrames"></a>堆栈帧
 这些接口表示堆栈帧，其中发生了断点或异常。

|接口|实施者|描述|
|---------------|--------------------|-----------------|
|[IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)|DE|表示发生断点或异常的上下文。|
|[IDebugStackFrame3](../../../extensibility/debugger/reference/idebugstackframe3.md)|DE|表示[IDebugStackFrame2，](../../../extensibility/debugger/reference/idebugstackframe2.md)可以处理截获的异常。|
|[IEnumCodePaths2](../../../extensibility/debugger/reference/ienumcodepaths2.md)|DE|表示对[CODE_PATH](../../../extensibility/debugger/reference/code-path.md)结构集的枚举，这些结构指定用于到达特定堆栈帧的函数调用序列。|
|[IEnumDebugFrameInfo2](../../../extensibility/debugger/reference/ienumdebugframeinfo2.md)|DE|表示对一组[FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md)结构的枚举，这些结构描述堆栈帧。|

## <a name="threads"></a><a name="Threads"></a>线程
 这些接口表示线程及其关联事件。

|接口|实施者|描述|
|---------------|--------------------|-----------------|
|[IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)|DE|表示执行线程。|
|[IDebugThreadCreateEvent2](../../../extensibility/debugger/reference/idebugthreadcreateevent2.md)|DE|创建线程时由 DE 发送。|
|[IDebugThreadDestroyEvent2](../../../extensibility/debugger/reference/idebugthreaddestroyevent2.md)|DE|当线程被销毁时由 DE 发送。|
|[IDebugThreadNameChangedEvent2](../../../extensibility/debugger/reference/idebugthreadnamechangedevent2.md)|DE|当线程更改其名称时由 DE 发送。|
|[IEnumDebugThreads2](../../../extensibility/debugger/reference/ienumdebugthreads2.md)|DE|表示对一组线程的枚举。|

## <a name="type-visualizers"></a><a name="TypeVisualizers"></a>类型可视化器
 这些接口支持类型可视化器。 这些接口通常由表达式赋值器实现。

|接口|实施者|描述|
|---------------|--------------------|-----------------|
|[IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md)|EE|表示要呈现给类型可视化工具的字节数组。|
|[IPropertyProxyEESide](../../../extensibility/debugger/reference/ipropertyproxyeeside.md)|EE|提供了用于访问要传递给类型可视化工具的数据的方法。|
|[IPropertyProxyProvider](../../../extensibility/debugger/reference/ipropertyproxyprovider.md)|EE|表示提供对[IPropertyProxyEESide](../../../extensibility/debugger/reference/ipropertyproxyeeside.md)实现的访问的属性。|

## <a name="see-also"></a>请参阅
- [API 参考](../../../extensibility/debugger/reference/api-reference-visual-studio-debugging.md)
- [创建自定义调试引擎](../../../extensibility/debugger/creating-a-custom-debug-engine.md)
