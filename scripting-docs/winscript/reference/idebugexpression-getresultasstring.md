---
title: IDebugExpression::GetResultAsString |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugExpression.GetResultAsString
apilocation:
- jscript.dll
helpviewer_keywords:
- IDebugExpression::GetResultAsString
ms.assetid: edadd2ad-9369-4878-bf87-cea15be9f363
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 84255e364630245564a0cbab5d38c6dff38df0a8
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62978466"
---
# <a name="idebugexpressiongetresultasstring"></a>IDebugExpression::GetResultAsString
返回一个字符串和操作的返回值为表达式计算的结果。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetResultAsString(  
   HRESULT*  phrResult,  
   BSTR*     pbstrResult  
);  
```  
  
#### <a name="parameters"></a>参数  
 `phrResult`  
 [out]操作的返回值。  
  
 `pbstrResult`  
 [out]表达式计算的结果。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
|`E_PENDING`|该操作仍是挂起。|  
  
## <a name="remarks"></a>备注  
 此方法返回的表达式计算为一个字符串，该操作的结果`HRESULT`。  
  
 此方法返回`S_OK`并`phrResult`返回`E_ABORT`如果`Abort`中止操作。  
  
## <a name="see-also"></a>请参阅  
 [IDebugExpression 接口](../../winscript/reference/idebugexpression-interface.md)