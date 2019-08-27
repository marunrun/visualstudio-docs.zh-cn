---
title: IDebugPropertyField | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugPropertyField
helpviewer_keywords:
- IDebugPropertyField interface
ms.assetid: b50edb2c-fb8d-4def-993d-17d23d2027c1
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: bad60a24c9120c1425a5d9041a32755feeb6e6c9
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65692143"
---
# <a name="idebugpropertyfield"></a>IDebugPropertyField
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此接口提供允许获取和设置属性的函数。  
  
## <a name="syntax"></a>语法  
  
```  
IDebugPropertyField : IDebugContainerField  
```  
  
## <a name="notes-for-implementers"></a>实施者的说明  
 符号提供程序实现此接口上实现的相同对象[IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)。 此接口是支持属性的概念的类的专用化。  
  
## <a name="notes-for-callers"></a>调用方的说明  
 使用[QueryInterface](https://msdn.microsoft.com/library/62fce95e-aafa-4187-b50b-e6611b74c3b3)若要获取此接口从[IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)接口如果[GetKind](../../../extensibility/debugger/reference/idebugfield-getkind.md)方法将返回`FIELD_KIND_PROP`。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
 除了上的方法[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)并[IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)接口，此接口实现以下方法：  
  
|方法|描述|  
|------------|-----------------|  
|[GetPropertyGetter](../../../extensibility/debugger/reference/idebugpropertyfield-getpropertygetter.md)|获取获取的属性的方法。|  
|[GetPropertySetter](../../../extensibility/debugger/reference/idebugpropertyfield-getpropertysetter.md)|获取设置的属性的方法。|  
  
## <a name="remarks"></a>备注  
 属性是一个托管的代码的概念，表示视为变量的方法。 属性不存在于非托管C++。  
  
## <a name="requirements"></a>要求  
 标头： sh.h  
  
 命名空间:Microsoft.VisualStudio.Debugger.Interop  
  
 程序集：Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>请参阅  
 [符号提供程序接口](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)   
 [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)
