---
title: IDebugContainerField | Microsoft Docs
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
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65686976"
---
# <a name="idebugcontainerfield"></a>IDebugContainerField
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此接口表示符号或其他符号或类型的容器类型。  
  
## <a name="syntax"></a>语法  
  
```  
IDebugContainerField : IDebugField  
```  
  
## <a name="notes-for-implementers"></a>实施者的说明  
 符号提供程序实现此接口上实现的相同对象[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)接口。 此接口也是表示容器的所有接口的类的基类。  
  
## <a name="notes-for-callers"></a>调用方的说明  
 在多个接口上的很多方法返回此接口。 由于这是基类的所有容器，更专业的接口可以通过从获取此接口使用[QueryInterface](https://msdn.microsoft.com/library/62fce95e-aafa-4187-b50b-e6611b74c3b3)。 此类接口包括[IDebugArrayField](../../../extensibility/debugger/reference/idebugarrayfield.md)， [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)， [IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md)，以及[IDebugPropertyField](../../../extensibility/debugger/reference/idebugpropertyfield.md)。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
 除了上的方法[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)接口，此接口实现了以下方法：  
  
|方法|描述|  
|------------|-----------------|  
|[EnumFields](../../../extensibility/debugger/reference/idebugcontainerfield-enumfields.md)|创建容器的字段的枚举器。|  
  
## <a name="remarks"></a>备注  
 数组 （变量的容器）、 （方法和变量的容器） 的类和方法 （容器参数和局部变量） 的容器的所有示例都。  
  
## <a name="requirements"></a>要求  
 标头： sh.h  
  
 命名空间:Microsoft.VisualStudio.Debugger.Interop  
  
 程序集：Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>请参阅  
 [符号提供程序接口](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)   
 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
