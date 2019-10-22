---
title: IJsDebugFrame：： GetStackRange 方法 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IJsDebugFrame.GetStackRange
apilocation:
- jscript9diag.dll
ms.assetid: a6d1d8be-efc0-442d-9756-1959c8f102bd
caps.latest.revision: 4
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: d1ac3cbee9d16296632477f4128ec36370ab0d4a
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72574045"
---
# <a name="ijsdebugframegetstackrange-method"></a>IJsDebugFrame::GetStackRange 方法
返回逻辑 JavaScript 堆栈帧的绝对地址范围。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetStackRange(  
   UINT64 *pStart,  
   UINT64 *pEnd  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pStart`  
 弄帧最底端堆栈指针。  
  
 `pEnd`  
 弄帧最顶层的集指针。  
  
## <a name="return-value"></a>返回值  
  
## <a name="remarks"></a>备注  
 此方法可用于拼凑将从多个运行时收集的交错堆栈跟踪组合在一起。 起始堆栈指针可包含多个物理计算机堆栈帧（用于解释的 JavaScript 运行时帧）。 当堆栈从高到低地址增长时，开始 > 结束。  
  
## <a name="requirements"></a>要求  
 **标头：** jscript9diag  
  
## <a name="see-also"></a>请参阅  
 [IJsDebugFrame 接口](../../winscript/reference/ijsdebugframe-interface.md)