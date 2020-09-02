---
title: IDebugPointerObject |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugPointerObject
helpviewer_keywords:
- IDebugPointerObject interface
ms.assetid: 257fa167-b46e-4ffb-9a12-272efbf26702
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 4cd84c3580d94491e09ce9e8cde8175f9e437be0
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65693400"
---
# <a name="idebugpointerobject"></a>IDebugPointerObject
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

> [!IMPORTANT]
> 在 Visual Studio 2015 中，不推荐使用这种实现表达式计算器的方式。 有关实现 CLR 表达式计算器的信息，请参阅 [Clr 表达式计算器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) 和 [托管表达式计算器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。  
  
 此接口表示指针对象。  
  
## <a name="syntax"></a>语法  
  
```  
IDebugPointerObject : IDebugObject  
```  
  
## <a name="notes-for-implementers"></a>实施者注意事项  
 表达式计算器实现此接口来表示指针对象。  
  
## <a name="notes-for-callers"></a>调用方说明  
 如果表示指针，则 [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) 接口可以使用 [QueryInterface](https://msdn.microsoft.com/library/62fce95e-aafa-4187-b50b-e6611b74c3b3) 获取此接口 `IDebugObject` 。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
 除了从 [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)继承的方法之外，接口还 `IDebugPointerObject` 公开以下方法。  
  
|方法|说明|  
|------------|-----------------|  
|[Dereference](../../../extensibility/debugger/reference/idebugpointerobject-dereference.md)|获取接口指向的对象。|  
|[GetBytes](../../../extensibility/debugger/reference/idebugpointerobject-getbytes.md)|获取接口作为一系列连续字节指向的值。|  
|[SetBytes](../../../extensibility/debugger/reference/idebugpointerobject-setbytes.md)|设置接口从一系列连续字节指向的值。|  
  
## <a name="remarks"></a>备注  
 表达式计算器使用此接口来表示分析树中的指针。  
  
## <a name="requirements"></a>要求  
 标头： ee。h  
  
 命名空间： VisualStudio  
  
 程序集： Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>另请参阅  
 [表达式计算接口](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)   
 [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
