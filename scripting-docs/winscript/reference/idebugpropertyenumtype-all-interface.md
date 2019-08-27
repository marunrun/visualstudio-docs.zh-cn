---
title: IDebugPropertyEnumType_All Interface | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugPropertyEnumType_All
apilocation:
- scrobj.dll
helpviewer_keywords:
- IDebugPropertyEnumType_All interface
ms.assetid: 4d0f4fd5-e5f7-47cb-b746-860d6363e2cd
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: b9ddd9fb24aa83a6027d6d705de6a748a96b2e28
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62979105"
---
# <a name="idebugpropertyenumtypeall-interface"></a>IDebugPropertyEnumType_All 接口
`IDebugPropertyEnumType`接口定义，以便其 Iid 的每个可以作为一个筛选器，传递`IDebugProperty::EnumMembers`请求相应的枚举器时。  
  
## <a name="syntax"></a>语法  
  
```cpp
IDebugPropertyEnumType_All : IUnknown  
```  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
  
|方法|描述|  
|------------|-----------------|  
|[IDebugPropertyEnumType_All::GetName](../../winscript/reference/idebugpropertyenumtype-all-getname.md)|返回描述名称的文本字符串|  
  
 以下接口继承自`IDebugPropertyEnumType_All`，并没有更多的方法。  
  
```cpp
IDebugPropertyEnumType_Arguments : IDebugPropertyEnumType_All   
IDebugPropertyEnumType_Locals : IDebugPropertyEnumType_All   
IDebugPropertyEnumType_LocalsPlusArgs : IDebugPropertyEnumType_All   
IDebugPropertyEnumType_Registers : IDebugPropertyEnumType_All  
```  
  
## <a name="see-also"></a>请参阅  
 [IDebugProperty::EnumMembers](../../winscript/reference/idebugproperty-enummembers.md)