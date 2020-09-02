---
title: IDebugActivateDocumentEvent2 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65673695"
---
# <a name="idebugactivatedocumentevent2"></a>IDebugActivateDocumentEvent2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

调试引擎 (DE) 使用此接口请求要加载的文档。  
  
## <a name="syntax"></a>语法  
  
```  
IDebugActivateDocumentEvent2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>实施者注意事项  
 当需要打开源文件时，DE 将实现此接口。 此接口仅由使用或是脚本解释器一部分的调试引擎实现。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)接口必须在与此接口相同的对象上实现 (SDM 使用[QueryInterface](https://msdn.microsoft.com/library/62fce95e-aafa-4187-b50b-e6611b74c3b3)访问 `IDebugEvent2` 接口) 。  
  
## <a name="notes-for-callers"></a>调用方说明  
 如果需要打开一个源文件，则 DE 会创建并发送此事件对象。 使用 SDM 在附加到正在调试的程序时提供的 [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) 回调函数发送事件。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
 下表显示的方法 `IDebugActivateDocumentEvent2` 。  
  
|方法|说明|  
|-------------|-----------------|  
|[GetDocument](../../../extensibility/debugger/reference/idebugactivatedocumentevent2-getdocument.md)|获取要激活的文档。|  
|[GetDocumentContext](../../../extensibility/debugger/reference/idebugactivatedocumentevent2-getdocumentcontext.md)|获取描述文档中位置的文档上下文。|  
  
## <a name="remarks"></a>备注  
 使用此接口的典型情况是，如果在 HTML 页上的脚本代码中出现分析错误，脚本将此接口发送到 SDM，以便可以显示具有分析错误的文档。  
  
## <a name="requirements"></a>要求  
 标头： msdbg  
  
 命名空间： VisualStudio  
  
 程序集： Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>另请参阅  
 [IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md)   
 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)   
 [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
