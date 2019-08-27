---
title: IDebugProperty2::EnumChildren |Microsoft Docs
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
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68164958"
---
# <a name="idebugproperty2enumchildren"></a>IDebugProperty2::EnumChildren
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

检索的属性的子级的列表。  
  
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
 [in]中的标志的组合[DEBUGPROP_INFO_FLAGS](../../../extensibility/debugger/reference/debugprop-info-flags.md)枚举，用于指定哪些字段中枚举[DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md)结构是必填。  
  
 `dwRadix`  
 [in]指定用于格式化数值的任何信息的基数。  
  
 `guidFilter`  
 [in]与使用的筛选器的 GUID`dwAttribFilter`并`pszNameFilter`选择其中的参数`DEBUG_PROPERTY_INFO`子级都要枚举。 例如，`guidFilterLocals`本地变量的筛选器。  
  
 `dwAttribFilter`  
 [in]中的标志的组合[DBG_ATTRIB_FLAGS](../../../extensibility/debugger/reference/dbg-attrib-flags.md)枚举，用于指定哪种类型的对象，若要枚举，例如`DBG_ATTRIB_METHOD`可能是此属性的子级的所有方法。 与结合`guidFilter`和`pszNameFilter`参数。  
  
 `pszNameFilter`  
 [in]用于筛选器的名称`guidFilter`并`dwAttribFilter`选择其中的参数`DEBUG_PROPERTY_INFO`子级都要枚举。 例如，将此参数设置为"MyX"筛选器，为所有子项具有名称"MyX。"  
  
 `dwTimeout`  
 [in]指定以毫秒为单位，此方法返回前等待的最长时间。 使用`INFINITE`无限期等待。  
  
 `ppEnum`  
 [out]返回[IEnumDebugPropertyInfo2](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2.md)对象，其中包含的子属性的列表。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则返回错误代码。  
  
## <a name="see-also"></a>请参阅  
 [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)   
 [DEBUGPROP_INFO_FLAGS](../../../extensibility/debugger/reference/debugprop-info-flags.md)   
 [DBG_ATTRIB_FLAGS](../../../extensibility/debugger/reference/dbg-attrib-flags.md)   
 [IEnumDebugPropertyInfo2](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2.md)
