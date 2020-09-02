---
title: IDebugProperty2：： EnumChildren |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugProperty2::EnumChildren
helpviewer_keywords:
- IDebugProperty2::EnumChildren
ms.assetid: cf79f666-65d1-417c-af7c-9271bac9a267
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 6cd5b29978b6b67cc80e95b86603b0caf487c26c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68164958"
---
# <a name="idebugproperty2enumchildren"></a>IDebugProperty2::EnumChildren
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

检索属性的子元素的列表。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT EnumChildren (   
   DEBUGPROP_INFO_FLAGS      dwFields,  
   DWORD                     dwRadix,  
   REFGUID                   guidFilter,  
   DBG_ATTRIB_FLAGS          dwAttribFilter,  
   LPCOLESTR                 pszNameFilter,  
   DWORD                     dwTimeout,  
   IEnumDebugPropertyInfo2** ppEnum  
);  
```  
  
```csharp  
int EnumChildren (   
   enum_DEBUGPROP_INFO_FLAGS   dwFields,  
   uint                        dwRadix,  
   ref Guid                    guidFilter,  
   uint                        dwAttribFilter,  
   string                      pszNameFilter,  
   uint                        dwTimeout,  
   out IEnumDebugPropertyInfo2 ppEnum  
);  
```  
  
#### <a name="parameters"></a>参数  
 `dwFields`  
 中 [DEBUGPROP_INFO_FLAGS](../../../extensibility/debugger/reference/debugprop-info-flags.md) 枚举中的标志的组合，用于指定要在枚举的 [DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md) 结构中填充的字段。  
  
 `dwRadix`  
 中指定设置任何数值信息的格式时要使用的基数。  
  
 `guidFilter`  
 中与 `dwAttribFilter` 和参数一起用于 `pszNameFilter` 选择要枚举的子级的筛选器的 GUID `DEBUG_PROPERTY_INFO` 。 例如， `guidFilterLocals` 局部变量的筛选器。  
  
 `dwAttribFilter`  
 中 [DBG_ATTRIB_FLAGS](../../../extensibility/debugger/reference/dbg-attrib-flags.md) 枚举中的标志的组合，用于指定要枚举的对象的类型，例如， `DBG_ATTRIB_METHOD` 对于可能是此属性的子级的所有方法。 与和参数结合使用 `guidFilter` `pszNameFilter` 。  
  
 `pszNameFilter`  
 中与和参数一起使用的筛选器的名称，用于 `guidFilter` `dwAttribFilter` 选择 `DEBUG_PROPERTY_INFO` 要枚举的子级。 例如，将此参数设置为 "MyX" 可筛选名称为 "MyX" 的所有子级。  
  
 `dwTimeout`  
 中指定从此方法返回之前要等待的最长时间（以毫秒为单位）。 使用 `INFINITE` 无限期等待。  
  
 `ppEnum`  
 弄返回一个 [IEnumDebugPropertyInfo2](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2.md) 对象，该对象包含一个子属性列表。  
  
## <a name="return-value"></a>返回值  
 如果成功， `S_OK` 则返回; 否则返回错误代码。  
  
## <a name="see-also"></a>另请参阅  
 [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)   
 [DEBUGPROP_INFO_FLAGS](../../../extensibility/debugger/reference/debugprop-info-flags.md)   
 [DBG_ATTRIB_FLAGS](../../../extensibility/debugger/reference/dbg-attrib-flags.md)   
 [IEnumDebugPropertyInfo2](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2.md)
