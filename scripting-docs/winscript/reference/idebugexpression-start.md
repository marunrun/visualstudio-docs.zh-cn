---
title: IDebugExpression：： Start |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugExpression.Start
apilocation:
- jscript.dll
helpviewer_keywords:
- IDebugExpression::Start
ms.assetid: a7af3470-62b5-40f0-987d-63b6b22538b3
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 1c8c3666adfc83f3ad60b942cd3f7fe9eedfccba
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72576428"
---
# <a name="idebugexpressionstart"></a>IDebugExpression::Start
开始计算表达式。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT Start(  
   IDebugExpressionCallBack*  pdecb  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pdecb`  
 中用于指示表达式计算完成时间的回调。 如果 `NULL`此参数，则不会触发任何事件，客户端必须使用 `QueryIsComplete`轮询表达式状态。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|值|说明|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 此方法开始计算表达式。  
  
## <a name="see-also"></a>另请参阅  
 [IDebugExpression::Abort](../../winscript/reference/idebugexpression-abort.md)   
 [IDebugExpression 接口](../../winscript/reference/idebugexpression-interface.md)