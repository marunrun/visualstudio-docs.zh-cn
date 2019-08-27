---
title: 'Ijsdebugprocess:: Createstackwalker 方法 |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IJsDebugProcess.CreateStackWalker
apilocation:
- jscript9diag.dll
ms.assetid: 9d02e21d-7900-4942-8d17-cd04a2261463
caps.latest.revision: 4
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: cb084b665467ae023bb885ee0de221f0409a0160
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62557728"
---
# <a name="ijsdebugprocesscreatestackwalker-method"></a>IJsDebugProcess::CreateStackWalker 方法
堆栈查看器的工厂方法。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT CreateStackWalker(  
   DWORD threadId,  
   IJsDebugStackWalker **ppStackWalker  
);  
```  
  
#### <a name="parameters"></a>参数  
 `threadId`  
 [in]线程 id。  
  
 `ppStackWalker`  
 [out]新的堆栈查看器对象。  
  
## <a name="return-value"></a>返回值  
  
## <a name="remarks"></a>备注  
 如果线程在其上没有 JavaScript，则返回 E_JsDEBUG_UNKNOWN_THREAD。 目标进程停止时，可能仅调用此方法。  
  
## <a name="requirements"></a>要求  
 **标头：** jscript9diag.h  
  
## <a name="see-also"></a>请参阅  
 [IJsDebugProcess 接口](../../winscript/reference/ijsdebugprocess-interface.md)