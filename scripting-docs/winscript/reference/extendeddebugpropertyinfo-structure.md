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
ms.openlocfilehash: 09f3c5a219fca9ec9b881e2ae8363aae4d48e03f
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72575837"
---
# <a name="extendeddebugpropertyinfo-structure"></a>ExtendedDebugPropertyInfo 结构
利用附加成员扩展 `DebugPropertyInfo` 结构，以对扩展属性进行特征化。  
  
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
  
## <a name="members"></a>Members  
 `dwValidFields`  
 枚举数据类型，用于指定要初始化的字段。  
  
 `bstrName`  
 上下文中的属性名称。  
  
 `bstrType`  
 格式化字符串形式的属性类型。  
  
 `bstrValue`  
 格式化字符串形式的属性值。  
  
 `bstrFullName`  
 属性的完整名称。  
  
 `dwAttrib`  
 指定 debug 属性特性的标志的枚举。  
  
 `pDebugProp`  
 与此 `ExtendedDebugPropertyInfo` 对应的 `IDebugProperty` 对象。  
  
 `nDISPID`  
 调度 id。  
  
 `nType`  
 扩展属性类型。  
  
 `varValue`  
 扩展属性值（如果它可以适合变体）。  
  
 `plbValue`  
 属性值的实际数据字节。  
  
 `pDebugExtProp`  
 与此 `ExtendedDebugPropertyInfo` 对应的 `IDebugExtendedProperty` 对象。  
  
## <a name="see-also"></a>请参阅  
 [DebugPropertyInfo 结构](../../winscript/reference/debugpropertyinfo-structure.md)   
 [IDebugProperty 接口](../../winscript/reference/idebugproperty-interface.md)   
 [IDebugExtendedProperty 接口](../../winscript/reference/idebugextendedproperty-interface.md)   
 [DBGPROP_ATTRIB_FLAGS](../../winscript/reference/dbgprop-attrib-flags.md)    
 [DBGPROP_INFO_FLAGS](../../winscript/reference/dbgprop-info-flags.md)