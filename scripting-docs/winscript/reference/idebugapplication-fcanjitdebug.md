---
title: IDebugApplication：： FCanJitDebug |Microsoft Docs
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
ms.openlocfilehash: d68240ffd86935e9936642c09d5131f70b46e9ab
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72576880"
---
# <a name="idebugapplicationfcanjitdebug"></a>IDebugApplication::FCanJitDebug
确定是否注册了实时（JIT）调试器。  
  
## <a name="syntax"></a>语法  
  
```cpp
BOOL FCanJitDebug();  
```  
  
#### <a name="parameters"></a>参数  
 此方法不采用任何参数。  
  
## <a name="return-value"></a>返回值  
 如果该方法成功并且已注册 JIT 调试器，则该方法将返回 `TRUE`。 否则，它将返回 `FALSE`。  
  
## <a name="remarks"></a>备注  
 此方法确定 JIT 调试器是否已注册。  
  
## <a name="see-also"></a>请参阅  
 [IDebugApplication 接口](../../winscript/reference/idebugapplication-interface.md)