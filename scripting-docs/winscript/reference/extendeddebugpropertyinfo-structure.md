---
title: ExtendedDebugPropertyInfo 结构 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- ExtendedDebugPropertyInfo
apilocation:
- scrobj.dll
helpviewer_keywords:
- ExtendedDebugPropertyInfo structure
ms.assetid: f2cf6477-454b-4d13-95da-ae4c90daa175
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 1fe0eef00d2bf064a8a002925f4ba5607d36f31c
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62955173"
---
# <a name="extendeddebugpropertyinfo-structure"></a>ExtendedDebugPropertyInfo 结构
扩展了`DebugPropertyInfo`结构与其他成员协作来特征化的扩展的属性。  
  
## <a name="syntax"></a>语法  
  
```cpp
typedef struct ExtendedDebugPropertyInfo{  
   DBGPROP_INFO_FLAGS  dwValidFields;  
   LPOLESTR  bstrName;  
   LPOLESTR  bstrType;  
   LPOLESTR  bstrValue;  
   LPOLESTR  bstrFullName;  
   DBGPROP_ATTRIB_FLAGS  dwAttrib;  
   IDebugProperty*  pDebugProp;  
   DWORD  nDISPID;  
   DWORD  nType;  
   VARIANT  varValue;  
   ILockBytes*  plbValue;  
   IDebugExtendedProperty*  pDebugExtProp;  
};  
```  
  
## <a name="members"></a>成员  
 `dwValidFields`  
 枚举的数据类型，用于指定哪些字段进行初始化。  
  
 `bstrName`  
 在上下文中的属性名称。  
  
 `bstrType`  
 带格式的字符串形式的属性类型。  
  
 `bstrValue`  
 形式的格式化字符串的属性值。  
  
 `bstrFullName`  
 属性的完整名称。  
  
 `dwAttrib`  
 一个枚举，指定调试属性特性的标志。  
  
 `pDebugProp`  
 `IDebugProperty` 与此相对应的对象`ExtendedDebugPropertyInfo`。  
  
 `nDISPID`  
 调度 id。  
  
 `nType`  
 扩展的属性类型。  
  
 `varValue`  
 如果它可以变体中的调整扩展的属性的值。  
  
 `plbValue`  
 属性值的实际数据字节数。  
  
 `pDebugExtProp`  
 `IDebugExtendedProperty` 与此相对应的对象`ExtendedDebugPropertyInfo`。  
  
## <a name="see-also"></a>请参阅  
 [DebugPropertyInfo 结构](../../winscript/reference/debugpropertyinfo-structure.md)   
 [IDebugProperty 接口](../../winscript/reference/idebugproperty-interface.md)   
 [IDebugExtendedProperty 接口](../../winscript/reference/idebugextendedproperty-interface.md)   
 [DBGPROP_ATTRIB_FLAGS](../../winscript/reference/dbgprop-attrib-flags.md)   
 [DBGPROP_INFO_FLAGS](../../winscript/reference/dbgprop-info-flags.md)