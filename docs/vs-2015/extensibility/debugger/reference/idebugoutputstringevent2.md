---
title: IDebugOutputStringEvent2 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugOutputStringEvent2
helpviewer_keywords:
- IDebugOutputStringEvent2 interface
ms.assetid: 86596fd1-cecc-4813-8add-dc3d70068f9b
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 844d93a6752538c6b7239b6c10688fdfbd98b401
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65695195"
---
# <a name="idebugoutputstringevent2"></a>IDebugOutputStringEvent2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此接口是由发送调试引擎 (DE) 会话调试管理器 (SDM) 以输出一个字符串。  
  
## <a name="syntax"></a>语法  
  
```  
IDebugOutputStringEvent2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>实施者的说明  
 DE 实现此接口以发送到的字符串**输出**在 IDE 的窗口。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)接口必须实现此接口作为对同一个对象。 使用 SDM [QueryInterface](https://msdn.microsoft.com/library/62fce95e-aafa-4187-b50b-e6611b74c3b3)访问`IDebugEvent2`接口。  
  
## <a name="notes-for-callers"></a>调用方的说明  
 DE 创建，并将此事件的对象将字符串发送到发送**输出**窗口。 通过使用发送该事件[IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) SDM 附加到正在调试的程序时提供的回调函数。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
 下表显示的方法`IDebugOutputStringEvent2`。  
  
|方法|描述|  
|------------|-----------------|  
|[GetString](../../../extensibility/debugger/reference/idebugoutputstringevent2-getstring.md)|获取可显示的消息。|  
  
## <a name="remarks"></a>备注  
 例如，在非托管代码中，可以源自要输出的字符串，当正在调试的程序将字符串发送到 Win32`OutputDebugString`函数。 此字符串是由 DE 截获和日志发送到作为 SDM`IDebugOutputStringEvent2`事件。  
  
 使用[IDebugMessageEvent2](../../../extensibility/debugger/reference/idebugmessageevent2.md)发送一条消息，需要用户响应。  
  
 使用[IDebugErrorEvent2](../../../extensibility/debugger/reference/idebugerrorevent2.md)发送错误消息，不需要进行响应。  
  
## <a name="requirements"></a>要求  
 标头： msdbg.h  
  
 命名空间:Microsoft.VisualStudio.Debugger.Interop  
  
 程序集：Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>请参阅  
 [IDebugMessageEvent2](../../../extensibility/debugger/reference/idebugmessageevent2.md)   
 [IDebugErrorEvent2](../../../extensibility/debugger/reference/idebugerrorevent2.md)   
 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)   
 [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
