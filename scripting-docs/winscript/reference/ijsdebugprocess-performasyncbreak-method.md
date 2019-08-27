---
title: 'Ijsdebugprocess:: Performasyncbreak 方法 |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IJsDebugProcess.PerformAsyncBreak
apilocation:
- jscript9diag.dll
ms.assetid: 2a6ee369-ea99-4332-8521-a1741ccb6292
caps.latest.revision: 4
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 5a4fdb70341744c764779d406372bbd55418fd29
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62557980"
---
# <a name="ijsdebugprocessperformasyncbreak-method"></a>IJsDebugProcess::PerformAsyncBreak 方法
将脚本引擎放入中断模式会导致它为在下一个脚本指令发生中断。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT PerformAsyncBreak(  
   DWORD threadId  
);  
```  
  
#### <a name="parameters"></a>参数  
 `threadId`  
 [in]线程 id。  
  
## <a name="return-value"></a>返回值  
  
## <a name="requirements"></a>要求  
 **标头：** jscript9diag.h  
  
## <a name="see-also"></a>请参阅  
 [IJsDebugProcess 接口](../../winscript/reference/ijsdebugprocess-interface.md)