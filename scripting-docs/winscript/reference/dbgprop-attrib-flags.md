---
title: DBGPROP_ATTRIB_FLAGS | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- DBGPROP_ATTRIB_FLAGS
apilocation:
- scrobj.dll
f1_keywords:
- DBGPROP_ATTRIB_FLAGS
helpviewer_keywords:
- DBGPROP_ATTRIB_FLAGS
ms.assetid: 90314496-527b-4357-9df8-125a360bf216
caps.latest.revision: 10
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 0324353d716430148b4b3c7b8adf9262e0dc3b7b
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62955271"
---
# <a name="dbgpropattribflags"></a>DBGPROP_ATTRIB_FLAGS
描述 `IDebugProperty` 的各种特性。 `DebugPropertyInfo` 结构的成员。  
  
## <a name="syntax"></a>语法  
  
```cpp
enum {  
DBGPROP_ATTRIB_NO_ATTRIB  =0x00000000,  
   DBGPROP_ATTRIB_VALUE_IS_INVALID  =0x00000008,  
   DBGPROP_ATTRIB_VALUE_IS_EXPANDABLE  =0x00000010,  
   DBGPROP_ATTRIB_VALUE_READONLY  =0x00000800,  
   DBGPROP_ATTRIB_ACCESS_PUBLIC  =0x00001000,  
   DBGPROP_ATTRIB_ACCESS_PRIVATE  =0x00002000,  
   DBGPROP_ATTRIB_ACCESS_PROTECTED  =0x00004000,  
   DBGPROP_ATTRIB_ACCESS_FINAL  =0x00008000,  
   DBGPROP_ATTRIB_STORAGE_GLOBAL  =0x00010000,  
   DBGPROP_ATTRIB_STORAGE_STATIC  =0x00020000,  
   DBGPROP_ATTRIB_STORAGE_FIELD  =0x00040000,  
   DBGPROP_ATTRIB_STORAGE_VIRTUAL  =0x00080000,  
   DBGPROP_ATTRIB_TYPE_IS_CONSTANT  =0x00100000,  
   DBGPROP_ATTRIB_TYPE_IS_SYNCHRONIZED  =0x00200000,  
   DBGPROP_ATTRIB_TYPE_IS_VOLATILE  =0x00400000,  
   DBGPROP_ATTRIB_HAS_EXTENDED_ATTRIBS  =0x00800000  
   DBGPROP_ATTRIB_VALUE_IS_RETURN_VALUE  =0x08000000,  
};  
  
```  
  
## <a name="members"></a>成员  
 DBGPROP_ATTRIB_NO_ATTRIB  
 表示没有特性。  
  
 DBGPROP_ATTRIB_VALUE_IS_INVALID  
 表示 `DebugPropertyInfo::bstrValue` 中的值无效。  
  
 DBGPROP_ATTRIB_VALUE_IS_EXPANDABLE  
 表示引用或属性具有子级。  
  
 DBGPROP_ATTRIB_VALUE_READONLY  
 表示值是只读的。  
  
 DBGPROP_ATTRIB_ACCESS_PUBLIC  
 表示对象具有公共访问。  
  
 DBGPROP_ATTRIB_ACCESS_PRIVATE  
 表示对象具有私有访问。  
  
 DBGPROP_ATTRIB_ACCESS_PROTECTED  
 表示对象具有受保护的访问。  
  
 DBGPROP_ATTRIB_ACCESS_FINAL  
 表示对象具有最终访问。  
  
 DBGPROP_ATTRIB_STORAGE_GLOBAL  
 表示全局存储。  
  
 DBGPROP_ATTRIB_STORAGE_STATIC  
 表示静态存储。  
  
 DBGPROP_ATTRIB_STORAGE_FIELD  
 表示对象是一个属性。  
  
 DBGPROP_ATTRIB_STORAGE_VIRTUAL  
 表示虚拟存储。  
  
 DBGPROP_ATTRIB_TYPE_IS_CONSTANT  
 表示对象的类型是常量。  
  
 DBGPROP_ATTRIB_TYPE_IS_SYNCHRONIZED  
 表示该插槽是线程同步的。  
  
 DBGPROP_ATTRIB_TYPE_IS_VOLATILE  
 表示该插槽的持久存储是可变的。  
  
 DBGPROP_ATTRIB_HAS_EXTENDED_ATTRIBS  
 表示该插槽具有超越这些预定义位的特性。  
  
 DBGPROP_ATTRIB_VALUE_IS_RETURN_VALUE  
 表示该值是来自函数的返回值。  
  
## <a name="remarks"></a>备注  
 这些标志也用于筛选对象的子级。 这些值可使按位“或”组合。  
  
## <a name="see-also"></a>请参阅  
 [IDebugProperty 接口](../../winscript/reference/idebugproperty-interface.md)   
 [DebugPropertyInfo 结构](../../winscript/reference/debugpropertyinfo-structure.md)