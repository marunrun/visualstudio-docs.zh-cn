---
title: IDebugField | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugField
helpviewer_keywords:
- IDebugField interface
ms.assetid: adecdd1c-b1b9-4027-92da-74cbe910636f
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 8bc18204d3cbe20635ab0680a50b4d1555dce2ce
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65690307"
---
# <a name="idebugfield"></a>IDebugField
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此接口表示的字段，即符号或类型的说明。  
  
## <a name="syntax"></a>语法  
  
```  
IDebugField : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>实施者的说明  
 符号提供程序的所有字段的基类为实现此接口。  
  
## <a name="notes-for-callers"></a>调用方的说明  
 此接口是所有字段的基类。 返回值的基础[GetKind](../../../extensibility/debugger/reference/idebugfield-getkind.md)，此接口可能会使用返回的专用化程度接口[QueryInterface](https://msdn.microsoft.com/library/62fce95e-aafa-4187-b50b-e6611b74c3b3)。 此外，许多接口返回`IDebugField`中各种方法的对象。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
 下表显示的方法`IDebugField`。  
  
|方法|描述|  
|------------|-----------------|  
|[GetInfo](../../../extensibility/debugger/reference/idebugfield-getinfo.md)|获取的符号的类型的可显示信息。|  
|[GetKind](../../../extensibility/debugger/reference/idebugfield-getkind.md)|获取字段的类型。|  
|[GetType](../../../extensibility/debugger/reference/idebugfield-gettype.md)|获取字段的类型。|  
|[GetContainer](../../../extensibility/debugger/reference/idebugfield-getcontainer.md)|获取字段的容器。|  
|[GetAddress](../../../extensibility/debugger/reference/idebugfield-getaddress.md)|获取字段的地址。|  
|[GetSize](../../../extensibility/debugger/reference/idebugfield-getsize.md)|获取一个字段，以字节为单位的大小。|  
|[GetExtendedInfo](../../../extensibility/debugger/reference/idebugfield-getextendedinfo.md)|获取扩展字段的信息。|  
|[Equal](../../../extensibility/debugger/reference/idebugfield-equal.md)|比较两个字段。|  
|[GetTypeInfo](../../../extensibility/debugger/reference/idebugfield-gettypeinfo.md)|获取的符号的类型的独立于类型的信息。|  
  
## <a name="remarks"></a>备注  
 类型等效于 C 语言`typedef`。  
  
 在下面的示例C++语言的示例中，`weather`是类类型，并`sunny`并`stormy`符号：  
  
```cpp#  
class weather;  
weather sunny;  
weather stormy;  
```  
  
 字段表示符号，还是可以通过调用确定类型[GetKind](../../../extensibility/debugger/reference/idebugfield-getkind.md)并检查[FIELD_KIND](../../../extensibility/debugger/reference/field-kind.md)结果。 如果`FIELD_KIND_TYPE`设置位，则该字段是类型，并且如果`FIELD_KIND_SYMBOL`设置位，它是一个符号。  
  
## <a name="requirements"></a>要求  
 标头： sh.h  
  
 命名空间:Microsoft.VisualStudio.Debugger.Interop  
  
 程序集：Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>请参阅  
 [符号提供程序接口](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)
