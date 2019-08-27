---
title: DebugPropertyInfo 结构 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- DebugPropertyInfo
apilocation:
- scrobj.dll
helpviewer_keywords:
- DebugPropertyInfo structure
ms.assetid: 3246efbc-c212-4024-8f07-6414c2f85e75
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 99208626b41f2463178bccecf73c21a1d15fa765
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62955258"
---
# <a name="debugpropertyinfo-structure"></a>DebugPropertyInfo 结构
描述一个对象具有名称、 类型和值的实际层次结构。 它用来描述本地变量、 参数、 监视变量和表达式的调试属性，并注册。  
  
## <a name="syntax"></a>语法  
  
```cpp
typedef struct DebugPropertyInfo{  
   DBGPROP_INFO_FLAGS  dwValidFields;  
   BSTR  bstrName;  
   BSTR  bstrType;  
   BSTR  bstrValue;  
   BSTR  bstrFullName;  
   DBGPROP_ATTRIB_FLAGS  dwAttrib;  
   IDebugProperty*  pDebugProp;  
};  
```  
  
## <a name="members"></a>成员  
 dwValidFields  
 枚举的数据类型，用于指定哪些字段进行初始化。  
  
 bstrName  
 在上下文中的属性名称。  
  
 bstrType  
 属性类型，为带格式的字符串。  
  
 bstrValue  
 属性值，作为带格式的字符串。  
  
 bstrFullName  
 属性的完整名称。  
  
 dwAttrib  
 一个枚举，指定调试属性特性的标志。  
  
 pDebugProp  
 `IDebugProperty`由在此信息描述`DebugPropertyInfo`结构。  
  
## <a name="see-also"></a>请参阅  
 [IDebugProperty 接口](../../winscript/reference/idebugproperty-interface.md)   
 [DBGPROP_ATTRIB_FLAGS](../../winscript/reference/dbgprop-attrib-flags.md)   
 [DBGPROP_INFO_FLAGS](../../winscript/reference/dbgprop-info-flags.md)