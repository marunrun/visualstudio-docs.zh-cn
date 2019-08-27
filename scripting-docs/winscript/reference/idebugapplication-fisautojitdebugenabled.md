---
title: IDebugApplication::FIsAutoJitDebugEnabled |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugApplication.FIsAutoJitDebugEnabled
apilocation:
- pdm.dll
helpviewer_keywords:
- IDebugApplication::FIsAutoJitDebugEnabled
ms.assetid: 0551dd3b-e6eb-442a-8201-418f96fe62df
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: f594c5ce48ebd31a265ed438db176c5707d9b079
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62990865"
---
# <a name="idebugapplicationfisautojitdebugenabled"></a>IDebugApplication::FIsAutoJitDebugEnabled
确定是否在实时 (JIT) 调试程序已注册到自动调试非智能主机。  
  
## <a name="syntax"></a>语法  
  
```cpp
BOOL FIsAutoJitDebugEnabled();  
```  
  
#### <a name="parameters"></a>参数  
 此方法需要任何参数。  
  
## <a name="return-value"></a>返回值  
 如果该方法成功，并且 JIT 调试器注册到自动调试非智能主机，该方法返回`TRUE`。 否则，它将返回 `FALSE`。  
  
## <a name="remarks"></a>备注  
 此方法用于确定 JIT 调试器注册到自动调试非智能主机。  
  
## <a name="see-also"></a>请参阅  
 [IDebugApplication 接口](../../winscript/reference/idebugapplication-interface.md)