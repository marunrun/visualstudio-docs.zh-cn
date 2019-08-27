---
title: 'Ijsdebugstackwalker:: Getnext 方法 |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IJsDebugStackWalker.GetNext
apilocation:
- jscript9diag.dll
ms.assetid: 0b124768-50d3-4a69-876c-1aa337839a4e
caps.latest.revision: 4
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: ba8931a01f3afe05f791f4d89da60a9354868215
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62977869"
---
# <a name="ijsdebugstackwalkergetnext-method"></a>IJsDebugStackWalker::GetNext 方法
获取下一个帧。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetNext(  
   IJsDebugFrame **ppFrame  
);  
```  
  
#### <a name="parameters"></a>参数  
 `ppFrame`  
 [out]表示堆栈帧的对象。  
  
## <a name="return-value"></a>返回值  
  
## <a name="remarks"></a>备注  
 没有更多的堆栈帧来枚举时，返回 E_JsDEBUG_OUTSIDE_OF_VM  
  
## <a name="requirements"></a>要求  
 **标头：** jscript9diag.h  
  
## <a name="see-also"></a>请参阅  
 [IJsDebugStackWalker 接口](../../winscript/reference/ijsdebugstackwalker-interface.md)