---
title: IEnumDebugExtendedPropertyInfo：： Skip |Microsoft Docs
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
ms.openlocfilehash: 8e5c187f3484154a2758b67300c98d4cb9fc9023
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72574231"
---
# <a name="ienumdebugextendedpropertyinfoskip"></a>IEnumDebugExtendedPropertyInfo::Skip
跳过枚举序列中指定数目的 `ExtendedDebugPropertyInfo` 结构。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT Skip(  
   ULONG celt  
);  
```  
  
#### <a name="parameters"></a>参数  
 `celt`  
 中要跳过的枚举序列中 `ExtendedDebugPropertyInfo` 的结构数。  
  
## <a name="return-value"></a>返回值  
 返回一个有效 `HRESULT`，通常 `S_OK`。 如果 `celt` 大于枚举器中剩余的元素数，则返回 `S_FALSE`，并将当前元素指针设置为枚举的结尾。  
  
## <a name="see-also"></a>另请参阅  
 [IEnumDebugExtendedPropertyInfo 接口](../../winscript/reference/ienumdebugextendedpropertyinfo-interface.md)   
 [ExtendedDebugPropertyInfo 结构](../../winscript/reference/extendeddebugpropertyinfo-structure.md)