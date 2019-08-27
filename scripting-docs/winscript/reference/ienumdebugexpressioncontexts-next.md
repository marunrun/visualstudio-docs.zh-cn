---
title: IEnumDebugExpressionContexts::Next | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IEnumDebugExpressionContexts.Next
apilocation:
- jscript.dll
helpviewer_keywords:
- IEnumDebugExpressionContexts::Next
ms.assetid: aa223b0b-f7c1-4368-a59e-677e60133baf
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 5128ba9ac90fc99cfec81b2c81711547947bfa49
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62807346"
---
# <a name="ienumdebugexpressioncontextsnext"></a>IEnumDebugExpressionContexts::Next
检索指定的数目的枚举序列中的段。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT Next(  
   ULONG                      celt,  
   IDebugExpressionContext**  ppdec,  
   ULONG*                     pceltFetched  
);  
```  
  
#### <a name="parameters"></a>参数  
 `celt`  
 [in]若要检索的段的数目。  
  
 `ppdec`  
 [out]返回一个数组`IDebugExpressionContext`表示要检索的段的接口。  
  
 `pceltFetched`  
 [out]提取的枚举器实际段数。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 此方法检索枚举序列中的指定的段数。  
  
## <a name="see-also"></a>请参阅  
 [IEnumDebugExpressionContexts 接口](../../winscript/reference/ienumdebugexpressioncontexts-interface.md)