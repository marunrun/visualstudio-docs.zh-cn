---
title: IDebugBreakEvent2 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugBreakEvent2
helpviewer_keywords:
- IDebugBreakEvent2 interface
ms.assetid: 57dfdbc2-4e68-4dbf-9579-006cd6fb1c62
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 98e8c1b1669b3fdd1f442c6987e4e9d2b9fc4835
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65675376"
---
# <a name="idebugbreakevent2"></a>IDebugBreakEvent2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此接口通知会话调试管理器 (SDM) 已成功完成一个异步中断的值。  
  
## <a name="syntax"></a>语法  
  
```  
IDebugBreakEvent2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>实施者的说明  
 DE 实现此接口以支持在程序中的用户中断。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)接口必须实现此接口作为对同一个对象 (使用 SDM [QueryInterface](https://msdn.microsoft.com/library/62fce95e-aafa-4187-b50b-e6611b74c3b3)访问`IDebugEvent2`接口)。  
  
## <a name="notes-for-callers"></a>调用方的说明  
 SDM 调用[CauseBreak](../../../extensibility/debugger/reference/idebugprogram2-causebreak.md)时用户已请求要暂停正在调试的程序。 当已成功暂停程序时，将发送 DE`IDebugBreakEvent2`事件。 通过使用发送此事件[IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) SDM 它附加到正在调试的程序时所提供的回调函数。  
  
## <a name="remarks"></a>备注  
 例如，用户可以选择**全部中断**命令**调试**菜单以中断正在运行一个无限循环的程序。 SDM 告诉程序停止通过调用[CauseBreak](../../../extensibility/debugger/reference/idebugprogram2-causebreak.md)。 DE 发送`IDebugBreakEvent2`程序最后停止。  
  
## <a name="requirements"></a>要求  
 标头： msdbg.h  
  
 命名空间:Microsoft.VisualStudio.Debugger.Interop  
  
 程序集：Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>请参阅  
 [CauseBreak](../../../extensibility/debugger/reference/idebugprogram2-causebreak.md)   
 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)   
 [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
