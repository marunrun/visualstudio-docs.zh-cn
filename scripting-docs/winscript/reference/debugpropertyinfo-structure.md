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
ms.openlocfilehash: 793c83b467460f0744abffe3f161f7510f56257a
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72575070"
---
# <a name="debugpropertyinfo-structure"></a>DebugPropertyInfo 结构
描述具有名称、类型和值的分层性质的对象。 它用于描述本地变量、参数、监视变量和表达式以及寄存器的调试属性。  
  
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
  
## <a name="members"></a>Members  
 dwValidFields  
 枚举数据类型，用于指定要初始化的字段。  
  
 bstrName  
 上下文中的属性名称。  
  
 bstrType  
 格式化字符串形式的属性类型。  
  
 bstrValue  
 格式化字符串形式的属性值。  
  
 bstrFullName  
 属性的完整名称。  
  
 dwAttrib  
 指定 debug 属性特性的标志的枚举。  
  
 pDebugProp  
 此 `DebugPropertyInfo` 结构中的信息所描述的 `IDebugProperty`。  
  
## <a name="see-also"></a>请参阅  
 [IDebugProperty 接口](../../winscript/reference/idebugproperty-interface.md)   
 [DBGPROP_ATTRIB_FLAGS](../../winscript/reference/dbgprop-attrib-flags.md)    
 [DBGPROP_INFO_FLAGS](../../winscript/reference/dbgprop-info-flags.md)