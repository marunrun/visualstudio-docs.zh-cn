---
title: 活动脚本调试器接口 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- Active Script Debugger interfaces
- activdbg.h
ms.assetid: bf4750b1-4e58-442b-ab56-254e640de61d
caps.latest.revision: 15
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: ed8ff0361396deaaffd46f14ca1fc38869988593
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63422464"
---
# <a name="active-script-debugger-interfaces"></a>活动脚本调试器接口
Activdbg.h 和 activdbg100.h 标头文件提供接口、 枚举和结构在本部分中列出。 它们是用于调试脚本。  
  
> [!NOTE]
> `IJSDebug*`接口和`IEnumJsStackFrames`接口首次发布 Internet Explorer 11 中，用于调试脚本的本机代码。 这些接口的标头文件是 jscript9diag.h。  
  
## <a name="in-this-section"></a>本节内容  
 以下接口允许使用非特定于语言的、 中性主机调试：  
  
- [活动脚本调试器常量、枚举和结构](../../winscript/reference/active-script-debugger-constants-enumerations-and-structures.md)  
  
- [IActiveScriptDebug 接口](../../winscript/reference/iactivescriptdebug-interface.md)  
  
- [IActiveScriptErrorDebug 接口](../../winscript/reference/iactivescripterrordebug-interface.md)  
  
- [IActiveScriptErrorDebug110 接口](../../winscript/reference/iactivescripterrordebug110-interface.md)  
  
- [IActiveScriptSiteDebug 接口](../../winscript/reference/iactivescriptsitedebug-interface.md)  
  
- [IActiveScriptSiteDebug32 接口](../../winscript/reference/iactivescriptsitedebug32-interface.md)  
  
- [IActiveScriptSiteDebugEx 接口](../../winscript/reference/iactivescriptsitedebugex-interface.md)  
  
- [IActiveScriptWinRTErrorDebug 接口](../../winscript/reference/iactivescriptwinrterrordebug-interface.md)  
  
- [IApplicationDebugger 接口](../../winscript/reference/iapplicationdebugger-interface.md)  
  
- [IApplicationDebuggerUI 接口](../../winscript/reference/iapplicationdebuggerui-interface.md)  
  
- [IDebugApplication 接口](../../winscript/reference/idebugapplication-interface.md)  
  
- [IDebugApplication110 接口](../../winscript/reference/idebugapplication110-interface.md)  
  
- [IDebugApplicationNode 接口](../../winscript/reference/idebugapplicationnode-interface.md)  
  
- [IDebugApplicationNode100 接口](../../winscript/reference/idebugapplicationnode100-interface.md)  
  
- [IDebugApplicationNodeEvents 接口](../../winscript/reference/idebugapplicationnodeevents-interface.md)  
  
- [IDebugApplicationThread 接口](../../winscript/reference/idebugapplicationthread-interface.md)  
  
- [IDebugApplicationThread110 接口](../../winscript/reference/idebugapplicationthread110-interface.md)  
  
- [IDebugApplicationThreadEvents110 接口](../../winscript/reference/idebugapplicationthreadevents110-interface.md)  
  
- [IDebugAsyncOperation 接口](../../winscript/reference/idebugasyncoperation-interface.md)  
  
- [IDebugAsyncOperationCallBack 接口](../../winscript/reference/idebugasyncoperationcallback-interface.md)  
  
- [IDebugCodeContext 接口](../../winscript/reference/idebugcodecontext-interface.md)  
  
- [IDebugCookie 接口](../../winscript/reference/idebugcookie-interface.md)  
  
- [IDebugDocument 接口](../../winscript/reference/idebugdocument-interface.md)  
  
- [IDebugDocumentContext 接口](../../winscript/reference/idebugdocumentcontext-interface.md)  
  
- [IDebugDocumentHelper 接口](../../winscript/reference/idebugdocumenthelper-interface.md)  
  
- [IDebugDocumentHost 接口](../../winscript/reference/idebugdocumenthost-interface.md)  
  
- [IDebugDocumentInfo 接口](../../winscript/reference/idebugdocumentinfo-interface.md)  
  
- [IDebugDocumentProvider 接口](../../winscript/reference/idebugdocumentprovider-interface.md)  
  
- [IDebugDocumentText 接口](../../winscript/reference/idebugdocumenttext-interface.md)  
  
- [IDebugDocumentTextAuthor 接口](../../winscript/reference/idebugdocumenttextauthor-interface.md)  
  
- [IDebugDocumentTextEvents 接口](../../winscript/reference/idebugdocumenttextevents-interface.md)  
  
- [IDebugDocumentTextExternalAuthor 接口](../../winscript/reference/idebugdocumenttextexternalauthor-interface.md)  
  
- [IDebugExpression 接口](../../winscript/reference/idebugexpression-interface.md)  
  
- [IDebugExpressionCallBack 接口](../../winscript/reference/idebugexpressioncallback-interface.md)  
  
- [IDebugExpressionContext 接口](../../winscript/reference/idebugexpressioncontext-interface.md)  
  
- [IDebugFormatter 接口](../../winscript/reference/idebugformatter-interface.md)  
  
- [IDebugHelper 接口](../../winscript/reference/idebughelper-interface.md)  
  
- [IDebugSessionProvider 接口](../../winscript/reference/idebugsessionprovider-interface.md)  
  
- [IDebugSessionProviderEx 接口](../../winscript/reference/idebugsessionproviderex-interface.md)  
  
- [IDebugStackFrame 接口](../../winscript/reference/idebugstackframe-interface.md)  
  
- [IDebugStackFrameSniffer 接口](../../winscript/reference/idebugstackframesniffer-interface.md)  
  
- [IDebugStackFrameSnifferEx 接口](../../winscript/reference/idebugstackframesnifferex-interface.md)  
  
- [IDebugSyncOperation 接口](../../winscript/reference/idebugsyncoperation-interface.md)  
  
- [IDebugThreadCall 接口](../../winscript/reference/idebugthreadcall-interface.md)  
  
- [IEnumDebugApplicationNodes 接口](../../winscript/reference/ienumdebugapplicationnodes-interface.md)  
  
- [IEnumDebugCodeContexts 接口](../../winscript/reference/ienumdebugcodecontexts-interface.md)  
  
- [IEnumDebugExpressionContexts 接口](../../winscript/reference/ienumdebugexpressioncontexts-interface.md)  
  
- [IEnumDebugStackFrames 接口](../../winscript/reference/ienumdebugstackframes-interface.md)  
  
- [IEnumJsStackFrames 接口](../../winscript/reference/ienumjsstackframes-interface.md)  
  
- [IEnumRemoteDebugApplications 接口](../../winscript/reference/ienumremotedebugapplications-interface.md)  
  
- [IEnumRemoteDebugApplicationThreads 接口](../../winscript/reference/ienumremotedebugapplicationthreads-interface.md)  
  
- [IJsDebug 接口](../../winscript/reference/ijsdebug-interface.md)  
  
- [IJsDebugBreakPoint 接口](../../winscript/reference/ijsdebugbreakpoint-interface.md)  
  
- [IJsDebugDataTarget 接口](../../winscript/reference/ijsdebugdatatarget-interface.md)  
  
- [IJsDebugFrame 接口](../../winscript/reference/ijsdebugframe-interface.md)  
  
- [IJsDebugProcess 接口](../../winscript/reference/ijsdebugprocess-interface.md)  
  
- [IJsDebugProperty 接口](../../winscript/reference/ijsdebugproperty-interface.md)  
  
- [IJsDebugStackWalker 接口](../../winscript/reference/ijsdebugstackwalker-interface.md)  
  
- [IJsEnumDebugProperty 接口](../../winscript/reference/ijsenumdebugproperty-interface.md)  
  
- [IMachineDebugManager 接口](../../winscript/reference/imachinedebugmanager-interface.md)  
  
- [IMachineDebugManagerCookie 接口](../../winscript/reference/imachinedebugmanagercookie-interface.md)  
  
- [IMachineDebugManagerEvents 接口](../../winscript/reference/imachinedebugmanagerevents-interface.md)  
  
- [IProcessDebugManager 接口](../../winscript/reference/iprocessdebugmanager-interface.md)  
  
- [IProvideExpressionContexts 接口](../../winscript/reference/iprovideexpressioncontexts-interface.md)  
  
- [IRemoteDebugApplication 接口](../../winscript/reference/iremotedebugapplication-interface.md)  
  
- [IRemoteDebugApplication110 接口](../../winscript/reference/iremotedebugapplication110-interface.md)  
  
- [IRemoteDebugApplicationEx 接口](../../winscript/reference/iremotedebugapplicationex-interface.md)  
  
- [IRemoteDebugApplicationEvents 接口](../../winscript/reference/iremotedebugapplicationevents-interface.md)  
  
- [IRemoteDebugApplicationThread 接口](../../winscript/reference/iremotedebugapplicationthread-interface.md)  
  
- [IRemoteDebugApplicationThreadEx 接口](../../winscript/reference/iremotedebugapplicationthreadex-interface.md)  
  
- [ISetNextStatement 接口](../../winscript/reference/isetnextstatement-interface.md)  
  
- [ISimpleConnectionPoint 接口](../../winscript/reference/isimpleconnectionpoint-interface.md)  
  
- [IWebAppDiagnosticsSetup 接口](../../winscript/reference/iwebappdiagnosticssetup-interface.md)  
  
- [IWebAppDiagnosticsObjectInitialization 接口](../../winscript/reference/iwebappdiagnosticsobjectinitialization-interface.md)  
  
  以下部分列出了常量、 枚举和结构用于进行调试：  
  
- [活动脚本调试器常量、枚举和结构](../../winscript/reference/active-script-debugger-constants-enumerations-and-structures.md)  
  
## <a name="see-also"></a>请参阅  
 [活动脚本调试概述](../../winscript/active-script-debugging-overview.md)