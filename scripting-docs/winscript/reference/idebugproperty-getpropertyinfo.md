---
title: IDebugProperty：： GetPropertyInfo |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugProperty.GetPropertyInfo
apilocation:
- scrobj.dll
helpviewer_keywords:
- IDebugProperty::GetPropertyInfo
ms.assetid: b201c0c4-bff6-4285-880f-67be90584c5f
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: e0698e09cd9643322a237a81d971248577fd97e0
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72562323"
---
# <a name="idebugpropertygetpropertyinfo"></a>IDebugProperty::GetPropertyInfo
获取描述方法或索引属性的 `IDebugProperty` 的值。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetPropertyInfo (  
   DBGPROP_INFO_FLAGSdwFields,  
   UINT nRadix,  
   DebugPropertyInfo* pPropertyInfo  
);  
```  
  
#### <a name="parameters"></a>参数  
 `dwFields`  
 中指定 `DBGPROP_INFO_FLAGS` 常数，这些常数确定要在 `DebugPropertyInfo` 结构中填充的字段。  
  
 `nRadix`  
 中用于设置任何数字信息格式的基数。  
  
 `pPropertyInfo`  
 弄返回描述属性的 `DebugPropertyInfo` 结构。  
  
## <a name="return-value"></a>返回值  
 返回一个有效 `HRESULT`，通常 `S_OK`。  
  
## <a name="see-also"></a>另请参阅  
 [IDebugProperty 接口](../../winscript/reference/idebugproperty-interface.md)   
 [DBGPROP_INFO_FLAGS](../../winscript/reference/dbgprop-info-flags.md)   
 [DebugPropertyInfo 结构](../../winscript/reference/debugpropertyinfo-structure.md)