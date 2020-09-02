---
title: IEnumDebugCustomAttributes |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IEnumCustomAttributes
helpviewer_keywords:
- IEnumDebugCustomAttributes interface
ms.assetid: 11aa768d-1852-44d6-9de3-17f9bafaded2
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 7a0e1b361e99ef1e32a7dd327e531a1049f4009a
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68158075"
---
# <a name="ienumdebugcustomattributes"></a>IEnumDebugCustomAttributes
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

枚举自定义属性。  
  
## <a name="syntax"></a>语法  
  
```  
IEnumCustomAttributes : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>实施者注意事项  
 符号提供程序实现此接口，以支持通过 [IDebugCustomAttribute](../../../extensibility/debugger/reference/idebugcustomattribute.md) 接口)  (自定义属性。  
  
## <a name="notes-for-callers"></a>调用方说明  
 [EnumCustomAttributes](../../../extensibility/debugger/reference/idebugcustomattributequery2-enumcustomattributes.md) 返回此接口。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
 下表显示的方法 `IEnumDebugCustomAttributes` 。  
  
|方法|说明|  
|------------|-----------------|  
|[下一页](../../../extensibility/debugger/reference/ienumdebugcustomattributes-next.md)|检索枚举序列中指定数量的自定义属性。|  
|[Skip](../../../extensibility/debugger/reference/ienumdebugcustomattributes-skip.md)|跳过枚举序列中指定数量的自定义属性。|  
|[重置](../../../extensibility/debugger/reference/ienumdebugcustomattributes-reset.md)|将枚举序列重置到开始处。|  
|[克隆](../../../extensibility/debugger/reference/ienumdebugcustomattributes-clone.md)|创建与当前枚举数包含相同枚举状态的枚举数。|  
|[GetCount](../../../extensibility/debugger/reference/ienumdebugcustomattributes-getcount.md)|获取枚举器中的自定义属性的数目。|  
  
## <a name="requirements"></a>要求  
 标头： sh。h  
  
 命名空间： VisualStudio  
  
 程序集： Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>另请参阅  
 [符号提供程序接口](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)   
 [EnumCustomAttributes](../../../extensibility/debugger/reference/idebugcustomattributequery2-enumcustomattributes.md)   
 [IDebugCustomAttribute](../../../extensibility/debugger/reference/idebugcustomattribute.md)
