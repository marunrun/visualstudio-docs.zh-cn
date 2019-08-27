---
title: IDebugPropertyCreateEvent2 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugPropertyCreateEvent2
helpviewer_keywords:
- IDebugPropertyCreateEvent2 interface
ms.assetid: 33b3082b-a42e-488a-a1e4-dadf506f922c
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: d1558aa8ca9cad93b00cf90f02f3af6d346b036b
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65698667"
---
# <a name="idebugpropertycreateevent2"></a>IDebugPropertyCreateEvent2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

创建与特定文档相关联的属性时，此接口是由调试引擎 (DE) 发送到会话调试管理器 (SDM) 中。  
  
## <a name="syntax"></a>语法  
  
```  
IDebugPropertyCreateEvent2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>实施者的说明  
 DE 实现此接口来报告已创建一个属性。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)接口必须实现此接口作为对同一个对象。 使用 SDM [QueryInterface](https://msdn.microsoft.com/library/62fce95e-aafa-4187-b50b-e6611b74c3b3)访问`IDebugEvent2`接口。 如果 DE 已创建与已加载或创建的脚本关联的属性和该脚本需要出现在 IDE 中实现此接口。  
  
## <a name="notes-for-callers"></a>调用方的说明  
 DE 创建，并将此事件对象发送到已创建了一个属性的报表。 通过使用发送该事件[IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) SDM 附加到正在调试的程序时提供的回调函数。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
 下表显示的方法`IDebugPropertyCreateEvent2`接口。  
  
|方法|描述|  
|------------|-----------------|  
|[GetDebugProperty](../../../extensibility/debugger/reference/idebugpropertycreateevent2-getdebugproperty.md)|获取新的属性。|  
  
## <a name="remarks"></a>备注  
 如果属性具有特定文档或与之关联的脚本，DE 可以将发送此事件到 SDM 才能更新**脚本文档**窗口与文档的名称。 将调用 SDM [GetExtendedInfo](../../../extensibility/debugger/reference/idebugproperty2-getextendedinfo.md)带有参数`guidDocument`检索`VARIANT`包含[IUnknown](https://msdn.microsoft.com/library/e6b85472-e54b-4b8c-b19f-4454d6c05a8f)指针。 将调用 SDM [QueryInterface](https://msdn.microsoft.com/library/62fce95e-aafa-4187-b50b-e6611b74c3b3)来检索此指针上[IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md)接口，用于更新**脚本文档**窗口。  
  
## <a name="requirements"></a>要求  
 标头： msdbg.h  
  
 命名空间:Microsoft.VisualStudio.Debugger.Interop  
  
 程序集：Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>请参阅  
 [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)   
 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)   
 [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)   
 [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
