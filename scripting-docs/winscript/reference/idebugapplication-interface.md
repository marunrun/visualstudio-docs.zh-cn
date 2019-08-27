---
title: IDebugApplication 接口 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IDebugApplication interface
ms.assetid: 5dfa941b-4cd9-46fa-a230-3f41df9ea205
caps.latest.revision: 9
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 8229f234f8a8ce607f36c48e070cb3d40a211d45
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62990826"
---
# <a name="idebugapplication-interface"></a>IDebugApplication 接口
语言引擎和主机公开非远程调试方法，供使用。  
  
 除了继承的方法之外`IRemoteDebugApplication`，则`IDebugApplication`接口公开以下方法。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
  
|方法|描述|  
|------------|-----------------|  
|[IDebugApplication::SetName](../../winscript/reference/idebugapplication-setname.md)|设置应用程序的名称。|  
|[IDebugApplication::StepOutComplete](../../winscript/reference/idebugapplication-stepoutcomplete.md)|通知进程调试管理器中单步执行模式的语言引擎即将返回给调用方。|  
|[IDebugApplication::DebugOutput](../../winscript/reference/idebugapplication-debugoutput.md)|会导致调试器 IDE 将显示给定的字符串。|  
|[IDebugApplication::StartDebugSession](../../winscript/reference/idebugapplication-startdebugsession.md)|启动默认调试器 IDE，并将调试会话附加到此应用程序，如果尚未附加。|  
|[IDebugApplication::HandleBreakPoint](../../winscript/reference/idebugapplication-handlebreakpoint.md)|导致当前线程被阻塞，并将断点的通知发送到调试器 IDE。|  
|[IDebugApplication::Close](../../winscript/reference/idebugapplication-close.md)|使此应用程序释放所有引用并进入非活动状态。|  
|[IDebugApplication::GetBreakFlags](../../winscript/reference/idebugapplication-getbreakflags.md)|返回应用程序的当前中断标志。|  
|[IDebugApplication::GetCurrentThread](../../winscript/reference/idebugapplication-getcurrentthread.md)|返回与当前运行的线程关联的线程。|  
|[IDebugApplication::CreateAsyncDebugOperation](../../winscript/reference/idebugapplication-createasyncdebugoperation.md)|提供对给定同步调试操作的异步访问。|  
|[IDebugApplication::AddStackFrameSniffer](../../winscript/reference/idebugapplication-addstackframesniffer.md)|将堆栈帧的枚举器提供程序添加到此应用程序。|  
|[IDebugApplication::RemoveStackFrameSniffer](../../winscript/reference/idebugapplication-removestackframesniffer.md)|删除此应用程序中的堆栈帧的枚举器提供程序。|  
|[IDebugApplication::QueryCurrentThreadIsDebuggerThread](../../winscript/reference/idebugapplication-querycurrentthreadisdebuggerthread.md)|确定当前正在运行的线程是调试器线程。|  
|[IDebugApplication::SynchronousCallInDebuggerThread](../../winscript/reference/idebugapplication-synchronouscallindebuggerthread.md)|提供了为使调用方在调试器线程中运行代码的机制。|  
|[IDebugApplication::CreateApplicationNode](../../winscript/reference/idebugapplication-createapplicationnode.md)|创建一个新的应用程序节点与特定文档提供程序相关联。|  
|[IDebugApplication::FireDebuggerEvent](../../winscript/reference/idebugapplication-firedebuggerevent.md)|触发将泛型事件发送到调试器的`IApplicationDebugger`接口。|  
|[IDebugApplication::HandleRuntimeError](../../winscript/reference/idebugapplication-handleruntimeerror.md)|导致当前线程被阻塞，并将错误的通知发送到调试器 IDE。|  
|[IDebugApplication::FCanJitDebug](../../winscript/reference/idebugapplication-fcanjitdebug.md)|确定是否在实时 (JIT) 调试程序已注册。|  
|[IDebugApplication::FIsAutoJitDebugEnabled](../../winscript/reference/idebugapplication-fisautojitdebugenabled.md)|确定如果 JIT 调试器注册到自动调试非智能主机。|  
|[IDebugApplication::AddGlobalExpressionContextProvider](../../winscript/reference/idebugapplication-addglobalexpressioncontextprovider.md)|将全局表达式上下文提供程序添加到此应用程序。|  
|[IDebugApplication::RemoveGlobalExpressionContextProvider](../../winscript/reference/idebugapplication-removeglobalexpressioncontextprovider.md)|此应用程序中删除全局表达式上下文提供程序。|