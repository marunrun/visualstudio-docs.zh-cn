---
title: IEnumDebugExtendedPropertyInfo::Skip |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IEnumDebugExtendedPropertyInfo.Skip
apilocation:
- scrobj.dll
helpviewer_keywords:
- IEnumDebugExtendedPropertyInfo::Skip
ms.assetid: a0b4a9fc-e122-482b-9384-b83c460b61fe
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 87913f15f8799be0ad3f6616eeea53a8a627e3d0
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62963450"
---
# <a name="ienumdebugextendedpropertyinfoskip"></a>IEnumDebugExtendedPropertyInfo::Skip
跳过指定的数目的`ExtendedDebugPropertyInfo`枚举序列中的结构。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT Skip(  
   ULONG celt  
);  
```  
  
#### <a name="parameters"></a>参数  
 `celt`  
 [in]数`ExtendedDebugPropertyInfo`要跳过枚举序列中的结构。  
  
## <a name="return-value"></a>返回值  
 返回一个有效`HRESULT`，通常`S_OK`。 返回`S_FALSE`，并将当前元素指针设置到枚举末尾，如果`celt`大于枚举器中剩余的元素数。  
  
## <a name="see-also"></a>请参阅  
 [IEnumDebugExtendedPropertyInfo 接口](../../winscript/reference/ienumdebugextendedpropertyinfo-interface.md)   
 [ExtendedDebugPropertyInfo 结构](../../winscript/reference/extendeddebugpropertyinfo-structure.md)