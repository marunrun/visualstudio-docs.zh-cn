---
title: IDebugPointerField |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugPointerField
helpviewer_keywords:
- IDebugPointerField interface
ms.assetid: d51bd5b2-f18e-4e27-b4fb-e6f652fbf635
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 9d92b1b4d6efda1b8f05c594368a05bd833c9f34
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65705830"
---
# <a name="idebugpointerfield"></a>IDebugPointerField
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此接口表示指针类型。  
  
## <a name="syntax"></a>语法  
  
```  
IDebugPointerField : IDebugContainerField  
```  
  
## <a name="notes-for-implementers"></a>实施者注意事项  
 符号提供程序实现此接口来表示指针。  
  
## <a name="notes-for-callers"></a>调用方说明  
 如果[GetKind](../../../extensibility/debugger/reference/idebugfield-getkind.md)返回，则使用[QueryInterface](https://msdn.microsoft.com/library/62fce95e-aafa-4187-b50b-e6611b74c3b3)从[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)接口获取此接口 `FIELD_TYPE_POINTER` 。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序的方法  
 除了和接口上的方法 `IDebugField` `IDebugContainerField` ，此接口还实现以下方法：  
  
|方法|说明|  
|------------|-----------------|  
|[GetDereferencedField](../../../extensibility/debugger/reference/idebugpointerfield-getdereferencedfield.md)|返回描述指针目标的 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) 。|  
  
## <a name="remarks"></a>备注  
 在 C/c + + 中，如果指针与数组表示法一起使用，则它可以是一个容器。 例如，给定 `char *pString` ， `pString` 具有指向的类型的指针 `char` 。 `pString[3]` 的类型为，它是指向的指针，该指针 `char` 引用该容器的第四个元素。  
  
## <a name="requirements"></a>要求  
 标头： sh。h  
  
 命名空间： VisualStudio  
  
 程序集： Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>另请参阅  
 [符号提供程序接口](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)   
 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)   
 [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)
