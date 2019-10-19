---
title: JS_PROPERTY_ATTRIBUTES 枚举 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- JS_PROPERTY_ATTRIBUTES
apilocation:
- jscript9diag.dll
ms.assetid: e83b9b6c-5b21-48d1-92b6-22bed926b18b
caps.latest.revision: 7
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 94a72228e1ad6ab49568f3291ad9add7209ef3da
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72571746"
---
# <a name="js_property_attributes-enumeration"></a>JS_PROPERTY_ATTRIBUTES 枚举
指示属性的特性。  
  
## <a name="syntax"></a>语法  
  
```cpp
enum JS_PROPERTY_ATTRIBUTES{   JS_PROPERTY_ATTRIBUTE_NONE = 0,   JS_PROPERTY_HAS_CHILDREN = 0x1,   JS_PROPERTY_FAKE = 0x2,   JS_PROPERTY_METHOD = 0x4,   JS_PROPERTY_READONLY = 0x8,   JS_PROPERTY_NATIVE_WINRT_POINTER = 0x10} JS_PROPERTY_ATTRIBUTES;  
```  
  
## <a name="members"></a>Members  
  
|“属性”|描述|  
|----------|-----------------|  
|`JS_PROPERTY_ATTRIBUTE_NONE`|属性没有特性。|  
|`JS_PROPERTY_HAS_CHILDREN`|属性具有子级。|  
|`JS_PROPERTY_FAKE`|属性表示一个虚设节点，如 "[方法]"。|  
|`JS_PROPERTY_METHOD`|属性是一个方法。|  
|`JS_PROPERTY_READONLY`|该属性是只读的。|  
|`JS_PROPERTY_NATIVE_WINRT_POINTER`|属性是指向本机 WinRT 对象的指针。|  
  
## <a name="requirements"></a>要求  
 **标头：** jscript9diag  
  
## <a name="see-also"></a>请参阅  
 [Windows 脚本接口参考](../../winscript/reference/windows-script-interfaces-reference.md)