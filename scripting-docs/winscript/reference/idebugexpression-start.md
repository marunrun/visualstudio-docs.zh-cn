---
title: IDebugExpression::Start | Microsoft Docs
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
ms.openlocfilehash: e80f3fb8087d39c76f59cf5c6bc8719c1cbaf5e4
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62978518"
---
# <a name="idebugexpressionstart"></a>IDebugExpression::Start
开始表达式的计算。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT Start(  
   IDebugExpressionCallBack*  pdecb  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pdecb`  
 [in]指示表达式计算过程何时完成的回调。 如果此参数为`NULL`，不触发任何事件，并且客户端必须使用轮询表达式状态`QueryIsComplete`。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 此方法首先计算表达式。  
  
## <a name="see-also"></a>请参阅  
 [IDebugExpression::Abort](../../winscript/reference/idebugexpression-abort.md)   
 [IDebugExpression 接口](../../winscript/reference/idebugexpression-interface.md)