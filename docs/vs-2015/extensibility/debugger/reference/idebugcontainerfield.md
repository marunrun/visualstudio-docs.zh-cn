---
title: IDebugContainerField |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugContainerField
helpviewer_keywords:
- IDebugContainerField interface
ms.assetid: a8bbe061-c382-4fe9-a193-3f7d12216041
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 2656d3f5a3313a4538e3e0e6454dd671da635904
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65686976"
---
# <a name="idebugcontainerfield"></a>IDebugContainerField
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此接口表示作为其他符号或类型的容器的符号或类型。  
  
## <a name="syntax"></a>语法  
  
```  
IDebugContainerField : IDebugField  
```  
  
## <a name="notes-for-implementers"></a>实施者注意事项  
 符号提供程序在实现 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) 接口的同一对象上实现此接口。 此接口也是表示容器的所有接口的基类。  
  
## <a name="notes-for-callers"></a>调用方说明  
 许多接口上的许多方法都返回此接口。 由于这是所有容器的基类，因此可以通过使用 [QueryInterface](https://msdn.microsoft.com/library/62fce95e-aafa-4187-b50b-e6611b74c3b3)从此接口获取更多专用接口。 此类接口包括 [IDebugArrayField](../../../extensibility/debugger/reference/idebugarrayfield.md)、 [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)、 [IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md)和 [IDebugPropertyField](../../../extensibility/debugger/reference/idebugpropertyfield.md)。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
 除了 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) 接口上的方法，此接口还实现以下方法：  
  
|方法|说明|  
|------------|-----------------|  
|[EnumFields](../../../extensibility/debugger/reference/idebugcontainerfield-enumfields.md)|创建容器字段的枚举器。|  
  
## <a name="remarks"></a>备注  
 数组 (容器) 、方法和变量的类 (容器) 和方法 (参数和局部变量的容器) 是容器的所有示例。  
  
## <a name="requirements"></a>要求  
 标头： sh。h  
  
 命名空间： VisualStudio  
  
 程序集： Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>另请参阅  
 [符号提供程序接口](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)   
 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
