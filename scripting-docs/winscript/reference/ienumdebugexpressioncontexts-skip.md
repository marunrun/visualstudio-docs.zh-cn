---
title: IEnumDebugExpressionContexts::Skip | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IEnumDebugExpressionContexts.Skip
apilocation:
- jscript.dll
helpviewer_keywords:
- IEnumDebugExpressionContexts::Skip
ms.assetid: 3498cbb5-8581-4dcd-b016-e86b049c7831
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 5176eb83c4c5bfe517066d8ea7f52b76e121fb26
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62963515"
---
# <a name="ienumdebugexpressioncontextsskip"></a>IEnumDebugExpressionContexts::Skip
将跳过枚举序列中的指定的段数。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT Skip(  
   ULONG  celt  
);  
```  
  
#### <a name="parameters"></a>参数  
 `celt`  
 [in]若要跳过枚举序列中的段的数目。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 此方法将跳过枚举序列中的指定的段数。  
  
## <a name="see-also"></a>请参阅  
 [IEnumDebugExpressionContexts 接口](../../winscript/reference/ienumdebugexpressioncontexts-interface.md)