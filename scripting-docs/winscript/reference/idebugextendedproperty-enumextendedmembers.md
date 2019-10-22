---
title: IDebugExtendedProperty：： EnumExtendedMembers |Microsoft Docs
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
ms.openlocfilehash: f6fd225be9504254965eab77b912f50fb5c777e3
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72576393"
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
 中指定 EX_DBGPROP_INFO_FLAGS 常量，这些常量确定要填写的枚举扩展调试属性结构中的字段。  
  
 `nRadix`  
 中用于解释任何数值信息的基数。  
  
 `ppeepi`  
 弄返回枚举成员属性的 `IEnumDebugExtendedPropertyInfo` 接口。  
  
## <a name="return-value"></a>返回值  
 返回一个有效 `HRESULT`，通常 `S_OK`。  
  
## <a name="see-also"></a>请参阅  
 [IDebugExtendedProperty 接口](../../winscript/reference/idebugextendedproperty-interface.md)   
 [EX_DBGPROP_INFO_FLAGS](../../winscript/reference/ex-dbgprop-info-flags.md)    
 [ExtendedDebugPropertyInfo 结构](../../winscript/reference/extendeddebugpropertyinfo-structure.md)