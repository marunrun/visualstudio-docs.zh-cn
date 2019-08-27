---
title: IDebugMethodField |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugMethodField
helpviewer_keywords:
- IDebugMethodField interface
ms.assetid: a7dc9030-fc98-4cf1-b943-37a4003300b6
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 4d7f6fc12a3366200ca1e14c0e2d55f4f6d797f5
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65694347"
---
# <a name="idebugmethodfield"></a>IDebugMethodField
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此接口描述的方法。  
  
## <a name="syntax"></a>语法  
  
```  
IDebugMethodField : IDebugContainerField  
```  
  
## <a name="notes-for-implementers"></a>实施者的说明  
 符号提供程序实现此接口上实现的相同对象[IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)接口。 此接口是专用化，其中的一种方法。  
  
## <a name="notes-for-callers"></a>调用方的说明  
 使用[QueryInterface](https://msdn.microsoft.com/library/62fce95e-aafa-4187-b50b-e6611b74c3b3)若要获取此接口从[IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)接口如果[GetKind](../../../extensibility/debugger/reference/idebugfield-getkind.md)返回`FIELD_TYPE_METHOD`。 此外，这些方法[GetPropertyGetter](../../../extensibility/debugger/reference/idebugpropertyfield-getpropertygetter.md)， [GetPropertySetter](../../../extensibility/debugger/reference/idebugpropertyfield-getpropertysetter.md)，并[EnumConstructors](../../../extensibility/debugger/reference/idebugclassfield-enumconstructors.md)，则返回所有`IDebugMethodField`接口。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
 除了上的方法[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)并[IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)接口，此接口实现以下方法：  
  
|方法|描述|  
|------------|-----------------|  
|[EnumParameters](../../../extensibility/debugger/reference/idebugmethodfield-enumparameters.md)|创建方法的参数的枚举器。|  
|[GetThis](../../../extensibility/debugger/reference/idebugmethodfield-getthis.md)|获取包含方法的对象的"this"指针。|  
|[EnumAllLocals](../../../extensibility/debugger/reference/idebugmethodfield-enumalllocals.md)|创建所有本地变量的方法的枚举的器。|  
|[EnumLocals](../../../extensibility/debugger/reference/idebugmethodfield-enumlocals.md)|创建所选的方法的局部变量的枚举器。|  
|[IsCustomAttributeDefined](../../../extensibility/debugger/reference/idebugmethodfield-iscustomattributedefined.md)|确定是否已定义特定的自定义属性。|  
|[EnumStaticLocals](../../../extensibility/debugger/reference/idebugmethodfield-enumstaticlocals.md)|创建方法的静态局部变量的枚举器。|  
|[GetGlobalContainer](../../../extensibility/debugger/reference/idebugmethodfield-getglobalcontainer.md)|获取方法的全局容器。|  
|[EnumArguments](../../../extensibility/debugger/reference/idebugmethodfield-enumarguments.md)|创建调用该方法所需的每个参数的类型的枚举器。|  
  
## <a name="remarks"></a>备注  
 一种方法可以包含参数，以及本地变量。  
  
## <a name="requirements"></a>要求  
 标头： sh.h  
  
 命名空间:Microsoft.VisualStudio.Debugger.Interop  
  
 程序集：Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>请参阅  
 [符号提供程序接口](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)   
 [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)   
 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
