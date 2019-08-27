---
title: IDebugObject | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugObject
helpviewer_keywords:
- IDebugObject interface
ms.assetid: 05cd8bf4-c9ee-4b49-b782-2263c33067d6
caps.latest.revision: 15
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: c179a4443c23373fb92adf522ee0af34acb19c3f
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65695273"
---
# <a name="idebugobject"></a>IDebugObject
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种方式实现表达式计算器已弃用。 有关实现 CLR 表达式计算器的信息，请参阅[CLR 表达式计算器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)并[托管表达式计算器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。  
  
 此接口表示联编程序创建要封装的符号和表达式的值的对象。  
  
## <a name="syntax"></a>语法  
  
```  
IDebugObject : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>实施者的说明  
 表达式计算器实现此接口表示的对象。  
  
## <a name="notes-for-callers"></a>调用方的说明  
 此接口是表达式计算器分析表达式中使用的所有对象的基类。 返回通过调用[绑定](../../../extensibility/debugger/reference/idebugbinder-bind.md)方法。 [QueryInterface](https://msdn.microsoft.com/library/62fce95e-aafa-4187-b50b-e6611b74c3b3)从此接口获取更多专用的接口。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
 下表显示的方法`IDebugObject`。  
  
|方法|描述|  
|------------|-----------------|  
|[GetSize](../../../extensibility/debugger/reference/idebugobject-getsize.md)|获取对象的大小。|  
|[GetValue](../../../extensibility/debugger/reference/idebugobject-getvalue.md)|获取对象的值作为一系列连续的字节数。|  
|[SetValue](../../../extensibility/debugger/reference/idebugobject-setvalue.md)|设置对象的值从一系列连续的字节数。|  
|[SetReferenceValue](../../../extensibility/debugger/reference/idebugobject-setreferencevalue.md)|设置此对象的引用值。|  
|[GetMemoryContext](../../../extensibility/debugger/reference/idebugobject-getmemorycontext.md)|获取表示对象的值的地址的内存上下文。|  
|[GetManagedDebugObject](../../../extensibility/debugger/reference/idebugobject-getmanageddebugobject.md)|调试引擎的地址空间中创建托管对象的副本。|  
|[IsNullReference](../../../extensibility/debugger/reference/idebugobject-isnullreference.md)|测试此对象是否为 null 引用。|  
|[IsEqual](../../../extensibility/debugger/reference/idebugobject-isequal.md)|与此对象进行比较。|  
|[IsReadOnly](../../../extensibility/debugger/reference/idebugobject-isreadonly.md)|确定此对象是只读的。|  
|[IsProxy](../../../extensibility/debugger/reference/idebugobject-isproxy.md)|确定对象是否透明代理。|  
  
## <a name="remarks"></a>备注  
 表达式计算器使用此接口作为基类，用于表示分析树中的对象。  
  
## <a name="requirements"></a>要求  
 标头： ee.h  
  
 命名空间:Microsoft.VisualStudio.Debugger.Interop  
  
 程序集：Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>请参阅  
 [表达式计算接口](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)   
 [GetElement](../../../extensibility/debugger/reference/idebugarrayobject-getelement.md)   
 [Bind](../../../extensibility/debugger/reference/idebugbinder-bind.md)
