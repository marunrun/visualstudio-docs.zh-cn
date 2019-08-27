---
title: IDebugApplication::FCanJitDebug | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugApplication.FCanJitDebug
apilocation:
- pdm.dll
helpviewer_keywords:
- IDebugApplication::FCanJitDebug
ms.assetid: d7ddac65-4864-411f-bf66-34a46c03f239
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 2d5dc03d7d2511f5b50969c062104759e78fcf03
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62990927"
---
# <a name="idebugapplicationfcanjitdebug"></a>IDebugApplication::FCanJitDebug
确定是否在实时 (JIT) 调试程序已注册。  
  
## <a name="syntax"></a>语法  
  
```cpp
BOOL FCanJitDebug();  
```  
  
#### <a name="parameters"></a>参数  
 此方法需要任何参数。  
  
## <a name="return-value"></a>返回值  
 如果该方法成功，并且注册 JIT 调试器，该方法返回`TRUE`。 否则，它将返回 `FALSE`。  
  
## <a name="remarks"></a>备注  
 此方法确定是否已注册 JIT 调试器。  
  
## <a name="see-also"></a>请参阅  
 [IDebugApplication 接口](../../winscript/reference/idebugapplication-interface.md)