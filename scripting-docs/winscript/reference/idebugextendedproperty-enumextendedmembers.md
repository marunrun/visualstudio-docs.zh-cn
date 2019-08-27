---
title: IDebugExtendedProperty::EnumExtendedMembers |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugExtendedProperty.EnumExtendedMembers
apilocation:
- scrobj.dll
helpviewer_keywords:
- IDebugExtendedProperty::EnumExtendedMembers
ms.assetid: 27cdb091-da4e-44d2-a631-31ae00468b98
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: c7e14d1bc8937221960d938f1bbfae8e307830f2
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62946140"
---
# <a name="idebugextendedpropertyenumextendedmembers"></a>IDebugExtendedProperty::EnumExtendedMembers
枚举扩展属性的成员。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT EnumExtendedMembers(  
   EX_DBGPROP_INFO_FLAGS  dwFieldSpec,  
   UINT  nRadix,  
   IEnumDebugExtendedPropertyInfo**  ppeepi  
);  
```  
  
#### <a name="parameters"></a>参数  
 `dwFieldSpec`  
 [in]指定要填充的确定枚举中的字段扩展的调试属性结构的 EX_DBGPROP_INFO_FLAGS 常量。  
  
 `nRadix`  
 [in]用于解释任何数字信息的基数。  
  
 `ppeepi`  
 [out]返回`IEnumDebugExtendedPropertyInfo`枚举的成员属性的接口。  
  
## <a name="return-value"></a>返回值  
 返回一个有效`HRESULT`，通常`S_OK`。  
  
## <a name="see-also"></a>请参阅  
 [IDebugExtendedProperty 接口](../../winscript/reference/idebugextendedproperty-interface.md)   
 [EX_DBGPROP_INFO_FLAGS](../../winscript/reference/ex-dbgprop-info-flags.md)   
 [ExtendedDebugPropertyInfo 结构](../../winscript/reference/extendeddebugpropertyinfo-structure.md)