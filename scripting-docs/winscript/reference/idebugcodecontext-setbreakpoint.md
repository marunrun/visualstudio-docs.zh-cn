---
title: IDebugCodeContext::SetBreakPoint |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugCodeContext.SetBreakPoint
apilocation:
- jscript.dll
helpviewer_keywords:
- IDebugCodeContext::SetBreakPoint
ms.assetid: ecd42eae-66fa-40d3-9e47-08b826784108
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 7bbfe38c1db9f7c9afff34f5a92b8c43b0f4f9ba
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62974522"
---
# <a name="idebugcodecontextsetbreakpoint"></a>IDebugCodeContext::SetBreakPoint
设置或清除断点在此代码的上下文。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT SetBreakPoint(  
   BREAKPOINT_STATE  bps  
);  
```  
  
#### <a name="parameters"></a>参数  
 `bps`  
 [in]指定此代码的上下文的断点状态。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 此方法设置或清除断点在此代码的上下文。  
  
## <a name="see-also"></a>请参阅  
 [IDebugCodeContext 接口](../../winscript/reference/idebugcodecontext-interface.md)   
 [BREAKPOINT_STATE 枚举](../../winscript/reference/breakpoint-state-enumeration.md)