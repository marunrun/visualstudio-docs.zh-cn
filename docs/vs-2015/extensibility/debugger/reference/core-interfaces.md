---
title: 核心接口 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- debugging [Debugging SDK], core interfaces
ms.assetid: 666b9116-8550-4bdd-bc15-55fc57de87df
caps.latest.revision: 25
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 94703f13eba0c58aad24597bc65beeea862e79e5
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68179218"
---
# <a name="core-interfaces"></a>核心接口
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

以下接口是用于通过使用扩展调试器的核心接口[!INCLUDE[vsipsdk](../../../includes/vsipsdk-md.md)]。  
  
## <a name="discussion"></a>讨论  
 这些接口主要用于创建调试引擎 (DE)。 在此处按类别进行组织：  
  
- [断点](#Breakpoints)  
  
- [上下文](#Contexts)  
  
- [核心服务器](#CoreServer)  
  
- [调试引擎](#DebugEngines)  
  
- [文档](#Documents)  
  
- [事件](#Events)  
  
- [表达式](#Expressions)  
  
- [内存](#Memory)  
  
- [模块](#Modules)  
  
- [端口](#Ports)  
  
- [进程](#Processes)  
  
- [程序](#Programs)  
  
- [属性](#Properties)  
  
- [堆栈帧](#StackFrames)  
  
- [线程](#Threads)  
  
- [类型可视化工具](#TypeVisualizers)  
  
  可以实现接口的实体是：  
  
- 调试引擎 (DE)  
  
- 端口提供程序 (PS)  
  
- 表达式计算器 (EE)  
  
- Visual Studio (VS)  
  
## <a name="Breakpoints"></a> 断点  
 有关这些接口的实现和跟踪断点。  
  
|接口|由实现|描述|  
|---------------|--------------------|-----------------|  
|[IDebugBoundBreakpoint2](../../../extensibility/debugger/reference/idebugboundbreakpoint2.md)|DE|表示绑定到一个内存位置断点。|  
|[IDebugBreakpointBoundEvent2](../../../extensibility/debugger/reference/idebugbreakpointboundevent2.md)|DE|断点绑定到的内存位置时，由 DE 发送。|  
|[IDebugBreakpointChecksumRequest2](../../../extensibility/debugger/reference/idebugbreakpointchecksumrequest2.md)|VS|表示断点请求的文档校验和。|  
|[IDebugBreakpointErrorEvent2](../../../extensibility/debugger/reference/idebugbreakpointerrorevent2.md)|DE|断点未能绑定到一个内存位置时，由 DE 发送。|  
|[IDebugBreakpointEvent2](../../../extensibility/debugger/reference/idebugbreakpointevent2.md)|DE|到达断点时由 DE 发送。|  
|[IDebugBreakpointRequest2](../../../extensibility/debugger/reference/idebugbreakpointrequest2.md)|VS|表示断点; 的请求用于创建挂起断点。|  
|[IDebugBreakpointRequest3](../../../extensibility/debugger/reference/idebugbreakpointrequest3.md)|VS|表示断点; 的请求用于创建挂起断点。|  
|[IDebugBreakpointResolution2](../../../extensibility/debugger/reference/idebugbreakpointresolution2.md)|DE|表示用于绑定断点的信息。|  
|[IDebugBreakpointUnboundEvent2](../../../extensibility/debugger/reference/idebugbreakpointunboundevent2.md)|DE|中的内存位置未绑定断点时由 DE 发送。|  
|[IDebugErrorBreakpoint2](../../../extensibility/debugger/reference/idebugerrorbreakpoint2.md)|DE|表示无效的断点 (返回`IDebugBreakpointErrorEvent2`)。|  
|[IDebugErrorBreakpointResolution2](../../../extensibility/debugger/reference/idebugerrorbreakpointresolution2.md)|DE|表示有关无效的断点解决方法信息。|  
|[IDebugFunctionPosition2](../../../extensibility/debugger/reference/idebugfunctionposition2.md)|DE|表示一个函数中设置了断点的位置。|  
|[IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)|DE|表示要绑定; 一个断点用于创建绑定的断点。|  
|[IEnumDebugBoundBreakpoints2](../../../extensibility/debugger/reference/ienumdebugboundbreakpoints2.md)|DE|表示对一组绑定断点的枚举。|  
|[IEnumDebugErrorBreakpoints2](../../../extensibility/debugger/reference/ienumdebugerrorbreakpoints2.md)|DE|表示对一组无法绑定到的内存位置的断点的枚举。|  
  
## <a name="Contexts"></a> 上下文  
 这些接口表示各种类型的上下文中正在调试的程序。  
  
|接口|由实现|描述|  
|---------------|--------------------|-----------------|  
|[IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)|DE|表示代码指令的起始位置。|  
|[IDebugCodeContext3](../../../extensibility/debugger/reference/idebugcodecontext3.md)|DE|扩展了[IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)接口以便可以检索模块并处理的接口。|  
|[IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)|VS DE|表示文档中的位置。|  
|[IDebugExpressionContext2](../../../extensibility/debugger/reference/idebugexpressioncontext2.md)|DE|表示在其中计算表达式的上下文。|  
|[IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)|DE|表示内存字节的集合中的起始位置。|  
|[IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)|DE|表示在断点或异常的堆栈帧上下文。|  
|[IDebugStackFrame3](../../../extensibility/debugger/reference/idebugstackframe3.md)|DE|表示在断点或异常的堆栈帧上下文。|  
|[IEnumDebugCodeContexts2](../../../extensibility/debugger/reference/ienumdebugcodecontexts2.md)|DE|表示一组代码上下文枚举。|  
  
## <a name="CoreServer"></a> 核心服务器  
 这些接口表示正在其调试程序的计算机。 这些功能通过实现[!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)]可以调试引擎通过调用到。  
  
|接口|由实现|描述|  
|---------------|--------------------|-----------------|  
|[IDebugCoreServer2](../../../extensibility/debugger/reference/idebugcoreserver2.md)|VS|提供对端口和端口提供程序，以及有关计算机的信息的访问。|  
|[IDebugCoreServer3](../../../extensibility/debugger/reference/idebugcoreserver3.md)|VS|表示[IDebugCoreServer2](../../../extensibility/debugger/reference/idebugcoreserver2.md)支持远程调试。|  
  
## <a name="DebugEngines"></a> 调试引擎  
 这些接口表示的调试引擎和及其关联的事件。  
  
|接口|由实现|描述|  
|---------------|--------------------|-----------------|  
|[IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)|DE|表示自定义调试引擎。|  
|[IDebugEngine3](../../../extensibility/debugger/reference/idebugengine3.md)|DE|表示一个自定义调试引擎，支持加载的符号、 JustMyCode 和异常。|  
|[IDebugEngineCreateEvent2](../../../extensibility/debugger/reference/idebugenginecreateevent2.md)|DE|每个新的实例发送的 DE 以指示它已准备好处理的调试任务。|  
|[IDebugEngineLaunch2](../../../extensibility/debugger/reference/idebugenginelaunch2.md)|DE|表示一个自定义调试引擎，支持启动的程序。|  
|[IDebugProgramEngines2](../../../extensibility/debugger/reference/idebugprogramengines2.md)|DE PS|表示处理多个调试引擎的程序节点。|  
|[IDebugQueryEngine2](../../../extensibility/debugger/reference/idebugqueryengine2.md)|DE|提供有关 SDM，获得到的调试引擎的接口，从线程、 程序或堆栈帧的方法。|  
  
## <a name="Documents"></a> 文档  
 这些接口代表对文档 （源文件） 和其关联的元素。  
  
|接口|由实现|描述|  
|---------------|--------------------|-----------------|  
|[IDebugActivateDocumentEvent2](../../../extensibility/debugger/reference/idebugactivatedocumentevent2.md)|DE|由 DE 发送，以请求要打开的文档。|  
|[IDebugDisassemblyStream2](../../../extensibility/debugger/reference/idebugdisassemblystream2.md)|DE|表示从文档的反汇编指令的流。|  
|[IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md)|VS DE|表示由 DE，指定名称和类 ID (CLSID) 提供的文档。|  
|[IDebugDocumentChecksum2](../../../extensibility/debugger/reference/idebugdocumentchecksum2.md)|DE EE|表示调试文档的校验和并可将组件之间传递校验和。|  
|[IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)|VS DE|表示文档上下文中，与特定语句和代码上下文相对应的文档中的位置。|  
|[IDebugDocumentPosition2](../../../extensibility/debugger/reference/idebugdocumentposition2.md)|VS DE|表示文档中的常规位置。|  
|[IDebugDocumentPositionOffset2](../../../extensibility/debugger/reference/idebugdocumentpositionoffset2.md)|VS|表示源文件中作为字符偏移量的位置。|  
|[IDebugDocumentText2](../../../extensibility/debugger/reference/idebugdocumenttext2.md)|VS DE|表示文本文档提供的 DE (派生自[IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md))，提供的实际文本。|  
|[IDebugDocumentTextEvents2](../../../extensibility/debugger/reference/idebugdocumenttextevents2.md)|DE|由 DE 发送，以指定对内存中的源文件的更改。|  
  
## <a name="Events"></a> 事件  
 这些接口表示 DE 和会话调试管理器 (SDM) 之间发送的所有事件。  
  
|接口|由实现|描述|  
|---------------|--------------------|-----------------|  
|[IDebugActivateDocumentEvent2](../../../extensibility/debugger/reference/idebugactivatedocumentevent2.md)|DE|由 DE 发送，以请求要打开的文档。|  
|[IDebugBeforeSymbolSearchEvent2](../../../extensibility/debugger/reference/idebugbeforesymbolsearchevent2.md)|DE|调试引擎 (DE) 期间将发送此接口到会话调试管理器 (SDM) 设置的状态消息栏符号加载。|  
|[IDebugBreakEvent2](../../../extensibility/debugger/reference/idebugbreakevent2.md)|DE|由 DE 中断程序完成后发送。|  
|[IDebugBreakpointBoundEvent2](../../../extensibility/debugger/reference/idebugbreakpointboundevent2.md)|DE|当绑定断点时由 DE 发送。|  
|[IDebugBreakpointErrorEvent2](../../../extensibility/debugger/reference/idebugbreakpointerrorevent2.md)|DE|断点未能绑定时，由 DE 发送。|  
|[IDebugBreakpointEvent2](../../../extensibility/debugger/reference/idebugbreakpointevent2.md)|DE|到达断点时由 DE 发送。|  
|[IDebugBreakpointUnboundEvent2](../../../extensibility/debugger/reference/idebugbreakpointunboundevent2.md)|DE|未绑定断点时由 DE 发送。|  
|[IDebugCanStopEvent2](../../../extensibility/debugger/reference/idebugcanstopevent2.md)|DE|由 DE 发送，以确定它是否应停止在特定位置。|  
|[IDebugDocumentTextEvents2](../../../extensibility/debugger/reference/idebugdocumenttextevents2.md)|DE|由 DE 发送，以指定对内存中的源文件的更改。|  
|[IDebugEngineCreateEvent2](../../../extensibility/debugger/reference/idebugenginecreateevent2.md)|DE|每个新的实例发送的 DE 以指示它已准备好处理的调试任务。|  
|[IDebugEntryPointEvent2](../../../extensibility/debugger/reference/idebugentrypointevent2.md)|DE|由 DE 发送，以指示正在调试的程序已准备好执行的第一个指令。|  
|[IDebugErrorEvent2](../../../extensibility/debugger/reference/idebugerrorevent2.md)|DE|一个用其他事件接口，它们可能会返回错误，来提供用户可读的错误消息的接口。|  
|[IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)|DE PS|派生的所有其他事件接口的基接口。|  
|[IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)|VS|表示由事件 （表示为作为实现特定的事件接口的对象） 发送到 SDM 实现的接口。|  
|[IDebugExceptionEvent2](../../../extensibility/debugger/reference/idebugexceptionevent2.md)|DE|当正在调试的程序中发生了异常由 DE 发送。|  
|[IDebugExpressionEvaluationCompleteEvent2](../../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2.md)|DE|由 DE 异步表达式求值完成后发送。|  
|IDebugFindSymbolEvent2||已过时。 不要使用。|  
|[IDebugInterceptExceptionCompleteEvent2](../../../extensibility/debugger/reference/idebuginterceptexceptioncompleteevent2.md)|DE|由 DE 已截获异常处理完成后发送。|  
|[IDebugLoadCompleteEvent2](../../../extensibility/debugger/reference/idebugloadcompleteevent2.md)|DE|当在程序完成加载由 DE 发送。|  
|[IDebugMessageEvent2](../../../extensibility/debugger/reference/idebugmessageevent2.md)|DE|由发送 DE 以使 IDE 显示一条信息性消息给用户。|  
|[IDebugModuleLoadEvent2](../../../extensibility/debugger/reference/idebugmoduleloadevent2.md)|DE|加载或卸载模块时，由 DE 发送。|  
|[IDebugNoSymbolsEvent2](../../../extensibility/debugger/reference/idebugnosymbolsevent2.md)|DE|信号[!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)]调试器用户界面以警告符号不找不到启动可执行文件的用户。|  
|[IDebugOutputStringEvent2](../../../extensibility/debugger/reference/idebugoutputstringevent2.md)|DE|若要使 IDE 显示 DE 由发送的任意字符串。|  
|[IDebugPortEvents2](../../../extensibility/debugger/reference/idebugportevents2.md)|VS DE|端口发送的任何侦听器与通信端口事件。|  
|[IDebugProcessCreateEvent2](../../../extensibility/debugger/reference/idebugprocesscreateevent2.md)|DE PS|DE 或发送端口时创建一个进程。|  
|[IDebugProcessDestroyEvent2](../../../extensibility/debugger/reference/idebugprocessdestroyevent2.md)|DE PS|当一个进程已被销毁时发送 DE 或端口。|  
|[IDebugProgramCreateEvent2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md)|DE PS|在创建程序时，由 DE 或端口发送。|  
|[IDebugProgramDestroyEvent2](../../../extensibility/debugger/reference/idebugprogramdestroyevent2.md)|DE PS|当程序已被销毁时发送 DE 或端口。|  
|[IDebugProgramDestroyEventFlags2](../../../extensibility/debugger/reference/idebugprogramdestroyeventflags2.md)|DE|使调试引擎能够重写的默认行为[!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)]UI 时结束调试会话。|  
|[IDebugProgramNameChangedEvent2](../../../extensibility/debugger/reference/idebugprogramnamechangedevent2.md)|DE|从调试引擎 (DE) 会话调试管理器 (SDM) 更改时发送程序的名称。|  
|[IDebugPropertyCreateEvent2](../../../extensibility/debugger/reference/idebugpropertycreateevent2.md)|DE|发送的 DE 时新属性 (由`IDebugProperty2`接口) 已创建。|  
|[IDebugPropertyDestroyEvent2](../../../extensibility/debugger/reference/idebugpropertydestroyevent2.md)|DE|由 DE 属性已销毁时发送。|  
|[IDebugReturnValueEvent2](../../../extensibility/debugger/reference/idebugreturnvalueevent2.md)|DE|由 DE 逐句共或过程执行函数，以便可以正确显示返回值时发送。|  
|[IDebugSettingsCallback2](../../../extensibility/debugger/reference/idebugsettingscallback2.md)|VS|启用调试引擎读取指标设置远程。|  
|[IDebugStepCompleteEvent2](../../../extensibility/debugger/reference/idebugstepcompleteevent2.md)|DE|由 DE 到、 逐过程或指令的步骤完成后发送。|  
|[IDebugSymbolSearchEvent2](../../../extensibility/debugger/reference/idebugsymbolsearchevent2.md)|DE|由 DE 发送以指明成功或失败的加载的模块的符号。|  
|[IDebugThreadCreateEvent2](../../../extensibility/debugger/reference/idebugthreadcreateevent2.md)|DE|当创建一个线程由 DE 发送。|  
|[IDebugThreadDestroyEvent2](../../../extensibility/debugger/reference/idebugthreaddestroyevent2.md)|DE|由 DE 线程已销毁时发送。|  
|[IDebugThreadNameChangedEvent2](../../../extensibility/debugger/reference/idebugthreadnamechangedevent2.md)|DE|当一个线程已更改其名称由 DE 发送。|  
  
## <a name="Expressions"></a> 表达式  
 这些接口表示要在特定上下文中计算表达式。  
  
|接口|由实现|描述|  
|---------------|--------------------|-----------------|  
|[IDebugExpression2](../../../extensibility/debugger/reference/idebugexpression2.md)|DE|表示要计算的表达式。 从获取[IDebugExpressionContext2](../../../extensibility/debugger/reference/idebugexpressioncontext2.md)接口。|  
|[IDebugExpressionContext2](../../../extensibility/debugger/reference/idebugexpressioncontext2.md)|DE|表示在其中计算表达式的上下文。 从获取[IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)接口。|  
|[IDebugExpressionEvaluationCompleteEvent2](../../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2.md)|DE|由 DE 异步表达式求值完成后发送。|  
  
## <a name="Memory"></a> 内存  
 这些接口表示内存中的字节的序列。  
  
|接口|由实现|描述|  
|---------------|--------------------|-----------------|  
|[IDebugMemoryBytes2](../../../extensibility/debugger/reference/idebugmemorybytes2.md)|DE|表示可以读取或写入到的内存中的字节序列。|  
|[IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)|DE|表示序列中的内存中的字节的位置。|  
  
## <a name="Modules"></a> 模块  
 这些接口表示对应于可执行文件的模块或。DLL 文件。  
  
|接口|由实现|描述|  
|---------------|--------------------|-----------------|  
|[IDebugModule2](../../../extensibility/debugger/reference/idebugmodule2.md)|DE|表示单个可执行文件或 DLL。|  
|[IDebugModule3](../../../extensibility/debugger/reference/idebugmodule3.md)|DE|表示[IDebugModule2](../../../extensibility/debugger/reference/idebugmodule2.md)支持符号。|  
|[IDebugModuleLoadEvent2](../../../extensibility/debugger/reference/idebugmoduleloadevent2.md)|DE|加载或卸载模块时，由 DE 发送。|  
|[IDebugSourceServerModule](../../../extensibility/debugger/reference/idebugsourceservermodule.md)|DE|表示包含在 PDB 文件中的源服务器信息。|  
|[IEnumDebugModules2](../../../extensibility/debugger/reference/ienumdebugmodules2.md)|DE|表示一个枚举，通过一组模块的已知[IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)。|  
  
## <a name="Ports"></a> 端口  
 这些接口表示的端口和端口提供程序。  
  
|接口|由实现|描述|  
|---------------|--------------------|-----------------|  
|[IDebugDefaultPort2](../../../extensibility/debugger/reference/idebugdefaultport2.md)|VS PS|表示本地计算机上的默认端口。|  
|[IDebugFirewallConfigurationCallback2](../../../extensibility/debugger/reference/idebugfirewallconfigurationcallback2.md)|VS|允许使用 DCOM 提出的调试引擎[!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)]UI，以确保该防火墙将阻止远程调试。|  
|[IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)|VS PS|表示的端口。|  
|[IDebugPortEvents2](../../../extensibility/debugger/reference/idebugportevents2.md)|PS|端口发送的任何侦听器与通信端口事件。|  
|[IDebugPortEx2](../../../extensibility/debugger/reference/idebugportex2.md)|PS|表示可启动和终止进程的端口。|  
|[IDebugPortNotify2](../../../extensibility/debugger/reference/idebugportnotify2.md)|PS|用于注册和注销具有端口; 的程序允许的端口，以跟踪当前正在调试的程序。|  
|[IDebugPortPicker](../../../extensibility/debugger/reference/idebugportpicker.md)|PS|表示自定义的 UI 选择相应端口。|  
|[IDebugPortRequest2](../../../extensibility/debugger/reference/idebugportrequest2.md)|VS|表示从中创建或位于一个新的端口的端口的请求。|  
|[IDebugPortSupplier2](../../../extensibility/debugger/reference/idebugportsupplier2.md)|PS|表示供应商的端口。|  
|[IDebugPortSupplier3](../../../extensibility/debugger/reference/idebugportsupplier3.md)|PS|表示可以保留的端口的供应商 （保存到磁盘） 的端口信息创建它。|  
|[IDebugPortSupplierDescription2](../../../extensibility/debugger/reference/idebugportsupplierdescription2.md)|PS|使[!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)]UI 来显示内的文本**传输信息**一部分**附加到进程**对话框。|  
|[IDebugWindowsComputerPort2](../../../extensibility/debugger/reference/idebugwindowscomputerport2.md)|VS|允许的目标计算机的信息进行查询。|  
|[IEnumDebugPorts2](../../../extensibility/debugger/reference/ienumdebugports2.md)|VS PS|表示一个枚举，通过一组的端口。|  
|[IEnumDebugPortSuppliers2](../../../extensibility/debugger/reference/ienumdebugportsuppliers2.md)|VS|通过端口供应商提供的一组表示一个枚举。|  
  
## <a name="Processes"></a> 进程  
 这些接口表示单个可执行文件，其中包含一个或多个程序的进程。  
  
|接口|由实现|描述|  
|---------------|--------------------|-----------------|  
|[IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)|PS，DE|表示在计算机运行的进程。|  
|[IDebugProcess3](../../../extensibility/debugger/reference/idebugprocess3.md)|PS，DE|表示积极支持的进程调试 (用于替换步骤，继续，并在执行方法[IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)接口)。|  
|[IDebugProcessCreateEvent2](../../../extensibility/debugger/reference/idebugprocesscreateevent2.md)|DE PS|DE 或发送端口时创建一个进程。|  
|[IDebugProcessDestroyEvent2](../../../extensibility/debugger/reference/idebugprocessdestroyevent2.md)|DE PS|当一个进程已被销毁时发送 DE 或端口。|  
|[IDebugProcessEx2](../../../extensibility/debugger/reference/idebugprocessex2.md)|PS|表示必须跟踪哪些会话附加到它的进程。|  
|[IEnumDebugProcesses2](../../../extensibility/debugger/reference/ienumdebugprocesses2.md)|PS|表示一组端口上的进程的枚举。|  
  
## <a name="Programs"></a> 程序  
 这些接口表示程序，不一定对应于物理可执行文件或模块执行的逻辑单元。  
  
|接口|由实现|描述|  
|---------------|--------------------|-----------------|  
|[IDebugEngineProgram2](../../../extensibility/debugger/reference/idebugengineprogram2.md)|DE|表示[IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)需要与其他程序正在调试在同一时间可以协同工作。|  
|[IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)|DE PS|表示执行的逻辑单元。|  
|[IDebugProgramCreateEvent2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md)|DE PS|在创建程序时，由 DE 或端口发送。|  
|[IDebugProgramDestroyEvent2](../../../extensibility/debugger/reference/idebugprogramdestroyevent2.md)|DE PS|当程序已被销毁时发送 DE 或端口。|  
|[IDebugProgramEngines2](../../../extensibility/debugger/reference/idebugprogramengines2.md)|DE PS|表示[IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md) ，可以由多个调试引擎。|  
|[IDebugProgramEx2](../../../extensibility/debugger/reference/idebugprogramex2.md)|PS|表示[IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) ，必须能够跟踪哪个会话附加到它。|  
|[IDebugProgramHost2](../../../extensibility/debugger/reference/idebugprogramhost2.md)|DE PS|表示[IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) ，可以返回有关在其中运行的进程的信息。|  
|[IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)|DE PS|表示可调试的程序。|  
|[IDebugProgramNodeAttach2](../../../extensibility/debugger/reference/idebugprogramnodeattach2.md)|DE PS|允许程序节点尝试附加到关联的程序接收通知。|  
|[IDebugProgramProvider2](../../../extensibility/debugger/reference/idebugprogramprovider2.md)|DE|提供有关 SDM 来查询有关由该 DE 控制的程序 DE 的方法。|  
|[IDebugProgramPublisher2](../../../extensibility/debugger/reference/idebugprogrampublisher2.md)|VS|由 DEs 用于注册 SDM，显示在进行调试的程序。|  
|[IDebugProviderProgramNode2](../../../extensibility/debugger/reference/idebugproviderprogramnode2.md)|DE PS|表示[IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md) ，可以跨线程或进程边界封送接口。|  
|[IEnumDebugPrograms2](../../../extensibility/debugger/reference/ienumdebugprograms2.md)|DE PS|表示的程序集的枚举。|  
  
## <a name="Properties"></a>属性  
 这些接口表示属性，与特定上下文中，通常的表达式计算结果关联的值。  
  
|接口|由实现|描述|  
|---------------|--------------------|-----------------|  
|[IDebugCustomViewer](../../../extensibility/debugger/reference/idebugcustomviewer.md)|EE|表示[IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) ，可以自定义方式显示它的值。|  
|[IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)|DE|表示一个堆栈帧、 文档或的表达式计算结果的值。|  
|[IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)|DE|表示[IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)支持任意长度的字符串。|  
|[IDebugPropertyCreateEvent2](../../../extensibility/debugger/reference/idebugpropertycreateevent2.md)|DE|发送的 DE 时新属性 (由[IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)接口) 已创建。|  
|[IDebugPropertyDestroyEvent2](../../../extensibility/debugger/reference/idebugpropertydestroyevent2.md)|DE|由 DE 属性已销毁时发送。|  
|[IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)|DE|表示一个属性，它可以存在于任何特定堆栈帧之外的引用。|  
|[IEnumDebugPropertyInfo2](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2.md)|DE|表示一个枚举，通过一系列[DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md)描述变量、 寄存器、 参数和表达式的结构。|  
|[IEnumDebugReferenceInfo2](../../../extensibility/debugger/reference/ienumdebugreferenceinfo2.md)|DE|表示一个枚举，通过一系列[DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md)结构。|  
  
## <a name="StackFrames"></a> 堆栈帧  
 这些接口表示堆栈帧，上下文中的断点或异常已发生。  
  
|接口|由实现|描述|  
|---------------|--------------------|-----------------|  
|[IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)|DE|表示上下文中的断点或异常已发生。|  
|[IDebugStackFrame3](../../../extensibility/debugger/reference/idebugstackframe3.md)|DE|表示[IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)它可以处理已截获异常。|  
|[IEnumCodePaths2](../../../extensibility/debugger/reference/ienumcodepaths2.md)|DE|表示访问集合的枚举[CODE_PATH](../../../extensibility/debugger/reference/code-path.md)结构指定的函数的调用用于到达特定堆栈帧的序列。|  
|[IEnumDebugFrameInfo2](../../../extensibility/debugger/reference/ienumdebugframeinfo2.md)|DE|表示一个枚举，通过一系列[FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md)结构，描述堆栈帧。|  
  
## <a name="Threads"></a>线程  
 这些接口表示线程和及其关联的事件。  
  
|接口|由实现|描述|  
|---------------|--------------------|-----------------|  
|[IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)|DE|表示执行的线程。|  
|[IDebugThreadCreateEvent2](../../../extensibility/debugger/reference/idebugthreadcreateevent2.md)|DE|当创建一个线程由 DE 发送。|  
|[IDebugThreadDestroyEvent2](../../../extensibility/debugger/reference/idebugthreaddestroyevent2.md)|DE|由 DE 线程已销毁时发送。|  
|[IDebugThreadNameChangedEvent2](../../../extensibility/debugger/reference/idebugthreadnamechangedevent2.md)|DE|当一个线程已更改其名称由 DE 发送。|  
|[IEnumDebugThreads2](../../../extensibility/debugger/reference/ienumdebugthreads2.md)|DE|表示一个枚举，通过一组线程。|  
  
## <a name="TypeVisualizers"></a> 类型可视化工具  
 这些接口的类型可视化工具提供支持。 表达式计算器，通常会实现这些接口。  
  
|接口|由实现|描述|  
|---------------|--------------------|-----------------|  
|[IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md)|EE|表示要提供给类型可视化工具的字节数组。|  
|[IPropertyProxyEESide](../../../extensibility/debugger/reference/ipropertyproxyeeside.md)|EE|提供用于获取对要传递给类型可视化工具的数据访问方法。|  
|[IPropertyProxyProvider](../../../extensibility/debugger/reference/ipropertyproxyprovider.md)|EE|表示一个属性，它提供对访问[IPropertyProxyEESide](../../../extensibility/debugger/reference/ipropertyproxyeeside.md)实现。|  
  
## <a name="see-also"></a>请参阅  
 [API 参考](../../../extensibility/debugger/reference/api-reference-visual-studio-debugging.md)   
 [创建自定义调试引擎](../../../extensibility/debugger/creating-a-custom-debug-engine.md)
