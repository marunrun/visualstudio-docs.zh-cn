---
title: IDebugEnumField | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugEnumField
helpviewer_keywords:
- IDebugEnumField interface
ms.assetid: 42f685bf-0f39-47f4-98b0-6022efe2bf97
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: ac993e3a4676f1c84a193ddbf6e9a3b5bc8fa235
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65676506"
---
# <a name="idebugenumfield"></a>IDebugEnumField
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此接口表示一个枚举类型。  
  
## <a name="syntax"></a>语法  
  
```  
IDebugEnumField : IDebugContainerField  
```  
  
## <a name="notes-for-implementers"></a>实施者的说明  
 符号提供程序实现此接口来表示一个枚举。  
  
## <a name="notes-for-callers"></a>调用方的说明  
 使用[QueryInterface](https://msdn.microsoft.com/library/62fce95e-aafa-4187-b50b-e6611b74c3b3)若要获取此接口从[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)接口如果[GetKind](../../../extensibility/debugger/reference/idebugfield-getkind.md)返回`FIELD_TYPE_ENUM`。  
  
## <a name="methods-in-vtable-order"></a>VTable 顺序中的方法  
 除了上的方法`IDebugField`和`IDebugContainerField`接口，此接口实现以下方法：  
  
|方法|描述|  
|------------|-----------------|  
|[GetUnderlyingSymbol](../../../extensibility/debugger/reference/idebugenumfield-getunderlyingsymbol.md)|返回[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)描述了此枚举类型名称。|  
|[GetStringFromValue](../../../extensibility/debugger/reference/idebugenumfield-getstringfromvalue.md)|返回与给定的值相关联的枚举常量的名称。|  
|[GetValueFromString](../../../extensibility/debugger/reference/idebugenumfield-getvaluefromstring.md)|返回与给定的枚举常量名称关联的值|  
|[GetValueFromStringCaseInsensitive](../../../extensibility/debugger/reference/idebugenumfield-getvaluefromstringcaseinsensitive.md)|返回与给定的枚举常量名但忽略大小写相关联的值。|  
  
## <a name="remarks"></a>备注  
 它是实际绑定到的位置的基础符号[绑定](../../../extensibility/debugger/reference/idebugbinder-bind.md)。  
  
## <a name="requirements"></a>要求  
 标头： sh.h  
  
 命名空间:Microsoft.VisualStudio.Debugger.Interop  
  
 程序集：Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>请参阅  
 [符号提供程序接口](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)   
 [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)   
 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)   
 [Bind](../../../extensibility/debugger/reference/idebugbinder-bind.md)
