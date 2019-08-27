---
title: 活动脚本调试概述 | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Active Script Debugging overview
ms.assetid: ce4ec768-d017-4dfa-a7e3-cced3a29e679
caps.latest.revision: 11
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 31fb3f5bf88b0caf179a43d02358bb6a9f1a2831
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62975794"
---
# <a name="active-script-debugging-overview"></a>活动脚本调试概述
活动脚本调试接口可以进行中性语言调试和中性主机调试，并支持各种开发环境。  
  
 ![脚本主机进程](../winscript/media/scp56activdbgarchgif.gif "Scp56ActivDbgArchgif")  
图 1  
  
 中性语言调试环境可以支持任何编程语言或混合使用编程语言，无需具备这些语言的专业知识。 调试环境还支持跨语言单步执行和断点。 （本概述侧重介绍支持脚本语言，例如 VBScript 和 [!INCLUDE[javascript](../javascript/includes/javascript-md.md)]。）  
  
 中性主机调试器可自动与任何活动脚本主机一起使用，例如 Internet Explorer 或自定义主机。 主机控制调试器向用户显示的内容，包括从文档树的结构到调试文档的内容和语法着色等各方面内容。 这样可以让经过调试的源代码显示在主机文档的上下文中。 例如，Internet Explorer 可以显示 HTML 页面中的脚本。  
  
 下面各小节介绍了活动调试中的每个关键组件及其关联的接口。 但是在继续下一步之前，必须先定义活动调试的几个关键概念：  
  
 **主机应用程序**  
 承载脚本引擎并提供一组可编写脚本的对象（或“对象模型”）的应用程序。  
  
 **语言引擎**  
 对特定语言进行分析、执行和调试抽象的组件。  
  
 **调试器 IDE**  
 通过与主机应用程序和语言引擎进行通信来提供调试 UI 的应用程序。  
  
 **计算机调试管理器**用于维护可调试应用程序进程的注册表的组件。  
  
 **进程调试管理器**  
 维护特定应用程序的可调试文档树并跟踪正在运行的线程等的组件。  
  
 **文档上下文**  
 文档上下文是表示主机文档源代码中特定范围的抽象。  
  
 **代码上下文**  
 代码上下文表示语言引擎正在运行的代码中的特定位置（“虚拟指令指针”）。  
  
 **表达式上下文**  
 语言引擎可以计算表达式的特定上下文（例如堆栈帧）。  
  
 **对象浏览**  
 对象名称、类型、值和子对象的结构化并且与语言无关的表示形式，适用于实现“监视窗口”UI。  
  
 下面概述了活动调试的各关键组件和对应的相关接口，以及有关这些接口的详细信息。  
  
## <a name="language-engine"></a>语言引擎  
 语言引擎提供以下功能：  
  
- 语言分析和执行。  
  
- 调试支持（断点等）。  
  
- 表达式计算。  
  
- 语法着色。  
  
- 对象浏览。  
  
- 堆栈枚举和分析。  
  
  下面列出了一些接口，脚本引擎需要支持这些接口才能提供调试、表达式计算和对象浏览功能。 主机应用程序使用这些接口在其文档上下文和引擎的代码上下文之间进行映射，调试器 UI 也可以使用这些接口来执行表达式计算、堆栈枚举和对象浏览。  
  
  [IActiveScriptDebug 接口](../winscript/reference/iactivescriptdebug-interface.md)  
  提供语法着色和代码上下文枚举功能。  
  
  [IActiveScriptErrorDebug 接口](../winscript/reference/iactivescripterrordebug-interface.md)  
  出错时返回文档上下文和堆栈帧。  
  
  [IActiveScriptSiteDebug 接口](../winscript/reference/iactivescriptsitedebug-interface.md)  
  主机提供的从脚本引擎指向调试器的链接。  
  
  [IDebugCodeContext 接口](../winscript/reference/idebugcodecontext-interface.md)  
  在线程中提供虚拟的“指令指针”。  
  
  [IEnumDebugCodeContexts 接口](../winscript/reference/ienumdebugcodecontexts-interface.md)  
  枚举文档上下文对应的代码上下文。  
  
  [IDebugStackFrame 接口](../winscript/reference/idebugstackframe-interface.md)  
  表示线程堆栈上的逻辑堆栈帧。  
  
  [IDebugExpressionContext 接口](../winscript/reference/idebugexpressioncontext-interface.md)  
  提供可在其中计算表达式的上下文。  
  
  [IDebugStackFrameSniffer 接口](../winscript/reference/idebugstackframesniffer-interface.md)  
  提供枚举逻辑堆栈帧的一种方式。  
  
  [IDebugExpression 接口](../winscript/reference/idebugexpression-interface.md)  
  表示异步计算的表达式。  
  
  [IDebugSyncOperation 接口](../winscript/reference/idebugsyncoperation-interface.md)  
  允许脚本引擎在嵌套在特定受阻线程中时需要执行的操作。  
  
  [IDebugAsyncOperation 接口](../winscript/reference/idebugasyncoperation-interface.md)  
  提供对同步调试操作的异步访问。  
  
  [IDebugAsyncOperationCallBack 接口](../winscript/reference/idebugasyncoperationcallback-interface.md)  
  提供与 `IDebugAsyncOperation` 接口计算进度相关的状态事件。  
  
  [IEnumDebugExpressionContexts 接口](../winscript/reference/ienumdebugexpressioncontexts-interface.md)  
  枚举 `IDebugExpressionContexts` 对象的集合。  
  
  [IProvideExpressionContexts 接口](../winscript/reference/iprovideexpressioncontexts-interface.md)  
  提供枚举特定组件已知的表达式上下文的一种方式。  
  
  [IDebugFormatter 接口](../winscript/reference/idebugformatter-interface.md)  
  允许语言或 IDE 自定义 VARIANT 值或 VARTYPE 类型与字符串之间的转换。  
  
  [IDebugStackFrameSnifferEx 接口](../winscript/reference/idebugstackframesnifferex-interface.md)  
  枚举 PDM 的逻辑堆栈帧。  
  
## <a name="hosts"></a>主机  
 主机：  
  
- 承载语言引擎。  
  
- 提供对象模型（即可以编写脚本的对象集）。  
  
- 定义可进行调试的文档树及其内容。  
  
- 将脚本组织到虚拟应用程序中。  
  
  有两种类型的主机：  
  
- 非智能主机仅支持基本的活动脚本接口。 它不能控制文档结构或组织；文件结构和组织完全由提供给语言引擎的脚本决定。  
  
- 智能主机支持的接口更多，可以定义文档树、文档内容和语法着色。 下一小节将介绍一组帮助程序接口。通过这些接口可以更轻松地让主机成为智能主机。  
  
### <a name="smart-host-helper-interfaces"></a>智能主机帮助程序接口  
 `IDebugDocumentHelper` 方法提供了一组经过大幅度简化的接口。主机使用这些接口可以获得智能承载的好处，同时无需处理全套主机接口的所有复杂性（和功能）。  
  
 当然，主机不用必须使用这些接口。 但使用这些接口可以避免实现或使用很多更复杂的接口。  
  
 [IDebugDocumentHelper 接口](../winscript/reference/idebugdocumenthelper-interface.md)  
 由 PDM 实现，为进行智能承载所需的很多接口提供实现。  
  
 [IDebugDocumentHost 接口](../winscript/reference/idebugdocumenthost-interface.md)  
 由主机实现（可选），用于向调试器公开主机特有的功能（如语法着色）。  
  
 有关详细信息，请参阅[实现智能主机帮助程序接口](../winscript/implementing-smart-host-helper-interfaces.md)。  
  
### <a name="full-smart-host-interfaces"></a>全部智能主机接口  
 下面是智能主机在不使用帮助程序接口时必须实现或使用的全套接口。  
  
 由主机实现的接口：  
  
 [IDebugDocumentInfo 接口](../winscript/reference/idebugdocumentinfo-interface.md)  
 提供可实例化，也可不实例化的文档的信息。  
  
 [IDebugDocumentProvider 接口](../winscript/reference/idebugdocumentprovider-interface.md)  
 提供按需实例化文档的方法。  
  
 [IDebugDocument 接口](../winscript/reference/idebugdocument-interface.md)  
 所有调试文档的基接口。  
  
 [IDebugDocumentText 接口](../winscript/reference/idebugdocumenttext-interface.md)  
 提供纯文本版本的调试文档的访问权限。  
  
 [IDebugDocumentTextAuthor 接口](../winscript/reference/idebugdocumenttextauthor-interface.md)  
 允许编辑纯文本版本的调试文档。  
  
 [IDebugDocumentContext 接口](../winscript/reference/idebugdocumentcontext-interface.md)  
 提供正在调试的一部分文档的抽象表示形式。  
  
 由 PDM 代表主机实现的接口：  
  
 [IDebugApplicationNode 接口](../winscript/reference/idebugapplicationnode-interface.md)  
 通过在项目树中提供上下文来扩展 `IDebugDocumentProvider` 接口的功能。  
  
## <a name="debugger-ide"></a>调试器 IDE  
 IDE 是一个与语言无关的调试 UI。 提供以下功能：  
  
- 文档查看器/编辑器。  
  
- 断点管理。  
  
- 表达式计算和监视窗口。  
  
- 堆栈帧浏览。  
  
- 对象/类浏览。  
  
- 浏览虚拟应用程序结构。  
  
  由调试器实现的接口：  
  
  [IApplicationDebugger 接口](../winscript/reference/iapplicationdebugger-interface.md)  
  由调试器 IDE 会话公开的主接口。  
  
  [IApplicationDebuggerUI 接口](../winscript/reference/iapplicationdebuggerui-interface.md)  
  向外部组件授予对调试器的用户界面 (UI) 的更大控制权。  
  
  [IDebugExpressionCallBack 接口](../winscript/reference/idebugexpressioncallback-interface.md)  
  提供 `IDebugExpression` 计算进度的状态事件。  
  
  [IDebugDocumentTextEvents 接口](../winscript/reference/idebugdocumenttextevents-interface.md)  
  提供指示关联文本文档的更改的事件。  
  
  [IDebugApplicationNodeEvents 接口](../winscript/reference/idebugapplicationnodeevents-interface.md)  
  提供 `IDebugApplicationNode` 接口的事件接口。  
  
### <a name="machine-debug-manager"></a>计算机调试管理器  
 计算机调试管理器通过维护和枚举一系列的活动虚拟应用程序来提供虚拟应用程序和调试程序之间的连线点。  
  
 [IDebugSessionProvider 接口](../winscript/reference/idebugsessionprovider-interface.md)  
 为正在运行的应用程序建立调试会话。  
  
 [IMachineDebugManager 接口](../winscript/reference/imachinedebugmanager-interface.md)  
 计算机调试管理器的主接口。  
  
 [IMachineDebugManagerCookie 接口](../winscript/reference/imachinedebugmanagercookie-interface.md)  
 与 `IMachineDebugManager` 接口类似，但此接口支持调试 cookie。  
  
 [IMachineDebugManagerEvents 接口](../winscript/reference/imachinedebugmanagerevents-interface.md)  
 由计算机调试管理器维护的正在运行的应用程序列表中的信号变化。  
  
 [IEnumRemoteDebugApplications 接口](../winscript/reference/ienumremotedebugapplications-interface.md)  
 枚举计算机上正在运行的应用程序。  
  
### <a name="process-debug-manager"></a>进程调试管理器  
 PDM 执行下列操作：  
  
- 同步多个语言引擎的调试。  
  
- 维护可调试文档树。  
  
- 合并堆栈帧。  
  
- 跨语言引擎协调断点和单步执行。  
  
- 跟踪线程。  
  
- 维护用于异步处理的调试程序线程。  
  
- 与计算机调试管理器和调试器 IDE 进行通信。  
  
  以下是进程调试管理器提供的接口。  
  
  [IProcessDebugManager 接口](../winscript/reference/iprocessdebugmanager-interface.md)  
  进程调试管理器的主接口。 此接口可以在进程中创建、添加或删除虚拟应用程序。  
  
  [IRemoteDebugApplication 接口](../winscript/reference/iremotedebugapplication-interface.md)  
  表示正在运行的应用程序。  
  
  [IDebugApplication 接口](../winscript/reference/idebugapplication-interface.md)  
  公开不可远程处理的调试方法，供语言引擎和主机使用。  
  
  [IRemoteDebugApplicationThread 接口](../winscript/reference/iremotedebugapplicationthread-interface.md)  
  表示特定应用程序中的执行线程。  
  
  [IDebugApplicationThread 接口](../winscript/reference/idebugapplicationthread-interface.md)  
  允许语言引擎和主机提供线程同步功能并维护特定于线程的调试状态信息。  
  
  [IEnumRemoteDebugApplicationThreads 接口](../winscript/reference/ienumremotedebugapplicationthreads-interface.md)  
  枚举应用程序中正在运行的线程。  
  
  [IDebugThreadCall 接口](../winscript/reference/idebugthreadcall-interface.md)  
  调度封送调用。  
  
  [IDebugApplicationNode 接口](../winscript/reference/idebugapplicationnode-interface.md)  
  维持文档在层次结构中的位置。  
  
  [IEnumDebugApplicationNodes 接口](../winscript/reference/ienumdebugapplicationnodes-interface.md)  
  枚举与应用程序关联的节点的子节点。  
  
  [IEnumDebugStackFrames 接口](../winscript/reference/ienumdebugstackframes-interface.md)  
  枚举从引擎合并的线程对应的堆栈帧。  
  
  [IDebugCookie 接口](../winscript/reference/idebugcookie-interface.md)  
  允许在脚本调试器中设置调试 cookie。  
  
  [IDebugHelper 接口](../winscript/reference/idebughelper-interface.md)  
  充当对象浏览器的中心和脚本引擎的简单连接点。  
  
  [ISimpleConnectionPoint 接口](../winscript/reference/isimpleconnectionpoint-interface.md)  
  向脚本引擎提供用于描述和枚举在特定连接点上触发的事件的一种简单方式。  
  
## <a name="see-also"></a>请参阅  
 [活动脚本调试器接口](../winscript/reference/active-script-debugger-interfaces.md)
