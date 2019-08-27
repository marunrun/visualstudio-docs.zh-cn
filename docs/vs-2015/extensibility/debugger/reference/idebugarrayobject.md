---
title: IDebugArrayObject | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugArrayObject
helpviewer_keywords:
- IDebugArrayObject method
ms.assetid: a1c8e77e-dee1-4748-a516-6ab032a8f54f
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 8f8ec4c883078663d0e252d6a04ae7441f12f31d
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65686992"
---
# <a name="idebugarrayobject"></a>IDebugArrayObject
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种方式实现表达式计算器已弃用。 有关实现 CLR 表达式计算器的信息，请参阅[CLR 表达式计算器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)并[托管表达式计算器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。  
  
 此接口表示一个数组对象。  
  
## <a name="syntax"></a>语法  
  
```  
IDebugArrayObject : IDebugObject  
```  
  
## <a name="notes-for-implementers"></a>实施者的说明  
 表达式计算器实现此接口来表示一个数组。  
  
## <a name="notes-for-callers"></a>调用方的说明  
 [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)接口可以获取此接口通过[QueryInterface](https://msdn.microsoft.com/library/62fce95e-aafa-4187-b50b-e6611b74c3b3)如果该对象表示一个数组。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
 除了上的方法`IDebugObject`接口，以下方法的实现基于`IDebugArrayObject`接口。  
  
|方法|描述|  
|------------|-----------------|  
|[GetCount](../../../extensibility/debugger/reference/idebugarrayobject-getcount.md)|获取数组中元素的计数。|  
|[GetElement](../../../extensibility/debugger/reference/idebugarrayobject-getelement.md)|获取数组的元素。|  
|[GetElements](../../../extensibility/debugger/reference/idebugarrayobject-getelements.md)|获取数组的所有元素。|  
|[GetRank](../../../extensibility/debugger/reference/idebugarrayobject-getrank.md)|获取数组的秩。|  
|[GetDimensions](../../../extensibility/debugger/reference/idebugarrayobject-getdimensions.md)|获取数组的维数。|  
  
## <a name="remarks"></a>备注  
 表达式计算器使用此接口来表示分析树中的数组。  
  
## <a name="requirements"></a>要求  
 标头： ee.h  
  
 命名空间:Microsoft.VisualStudio.Debugger.Interop  
  
 程序集：Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>请参阅  
 [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
