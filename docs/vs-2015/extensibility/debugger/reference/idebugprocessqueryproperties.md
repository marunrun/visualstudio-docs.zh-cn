---
title: IDebugProcessQueryProperties |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- IDebugProcessQueryProperties
ms.assetid: ce29a248-81a0-42c0-99a7-1606e8c548ec
caps.latest.revision: 5
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 2ad6e7d10b2a6a83aa11a0296f4804704cd12c9d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62537246"
---
# <a name="idebugprocessqueryproperties"></a>IDebugProcessQueryProperties
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此接口是 [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md) 实现程序实现的扩展接口。 它允许实施者获取有关调试过程环境的信息。  
  
## <a name="syntax"></a>语法  
  
```  
IDebugProcessQueryProperties: IUnknown  
```  
  
## <a name="notes-for-implementers"></a>实施者注意事项  
 实现此接口可获取有关调试过程的执行环境的信息。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
 下表显示的方法 `IDebugProcessQueryProperties` 。  
  
|方法|说明|  
|------------|-----------------|  
|[QueryProperty](../../../extensibility/debugger/reference/idebugprocessqueryproperties-queryproperty.md)|查询属性值。|  
|[QueryProperties](../../../extensibility/debugger/reference/idebugprocessqueryproperties-queryproperties.md)|查询属性值。|  
  
## <a name="remarks"></a>备注  
 很少实现此接口。  
  
## <a name="requirements"></a>要求  
 标头： Portpriv  
  
 命名空间： VisualStudio  
  
 程序集： Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>另请参阅  
 [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)   
 [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
