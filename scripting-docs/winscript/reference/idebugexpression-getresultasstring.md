---
title: IDebugExpression：： GetResultAsString |Microsoft Docs
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
ms.openlocfilehash: 56b8f637744227763f55b7c024745d7ae4448b40
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72573516"
---
# <a name="idebugexpressiongetresultasstring"></a>IDebugExpression::GetResultAsString
以字符串和操作的返回值的形式返回表达式求值的结果。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetResultAsString(  
   HRESULT*  phrResult,  
   BSTR*     pbstrResult  
);  
```  
  
#### <a name="parameters"></a>参数  
 `phrResult`  
 弄操作的返回值。  
  
 `pbstrResult`  
 弄表达式计算的结果。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
|`E_PENDING`|操作仍处于挂起状态。|  
  
## <a name="remarks"></a>备注  
 此方法将表达式计算的结果作为字符串返回，操作的 `HRESULT`。  
  
 如果 `Abort` 中止操作，则此方法将返回 `S_OK` 和 `phrResult` 返回 `E_ABORT`。  
  
## <a name="see-also"></a>请参阅  
 [IDebugExpression 接口](../../winscript/reference/idebugexpression-interface.md)