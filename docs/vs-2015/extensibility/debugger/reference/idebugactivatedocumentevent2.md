---
title: IDebugActivateDocumentEvent2 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugActivateDocumentEvent2
helpviewer_keywords:
- IDebugActivateDocumentEvent2 interface
ms.assetid: 6f37edd7-a48c-4b41-b160-dff9be63a284
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: c2087cb8f1b9a4b89448f3bf07f869d16ed44dc8
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65673695"
---
# <a name="idebugactivatedocumentevent2"></a>IDebugActivateDocumentEvent2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

调试引擎 (DE) 使用此接口来请求要加载的文档。  
  
## <a name="syntax"></a>语法  
  
```  
IDebugActivateDocumentEvent2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>实施者的说明  
 当它需要要打开的源文件时，DE 实现此接口。 只能通过使用或属于脚本解释器的调试引擎实现此接口。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)接口必须实现此接口作为对同一个对象 (使用 SDM [QueryInterface](https://msdn.microsoft.com/library/62fce95e-aafa-4187-b50b-e6611b74c3b3)访问`IDebugEvent2`接口)。  
  
## <a name="notes-for-callers"></a>调用方的说明  
 DE 创建，并需要已打开的源代码文件时发送此事件对象。 通过使用发送该事件[IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) SDM 它附加到正在调试的程序时所提供的回调函数。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
 下表显示的方法`IDebugActivateDocumentEvent2`。  
  
|方法|描述|  
|-------------|-----------------|  
|[GetDocument](../../../extensibility/debugger/reference/idebugactivatedocumentevent2-getdocument.md)|获取要激活的文档。|  
|[GetDocumentContext](../../../extensibility/debugger/reference/idebugactivatedocumentevent2-getdocumentcontext.md)|获取用于描述文档中的位置的文档上下文。|  
  
## <a name="remarks"></a>备注  
 在其中使用此接口的典型情况是如果 HTML 页面上的脚本代码中出现分析错误，脚本 DE 此接口向发送 SDM，这样可以显示包含分析错误的文档。  
  
## <a name="requirements"></a>要求  
 标头： msdbg.h  
  
 命名空间:Microsoft.VisualStudio.Debugger.Interop  
  
 程序集：Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>请参阅  
 [IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md)   
 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)   
 [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
