---
title: IRemoteDebugApplication::CauseBreak | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IRemoteDebugApplication.CauseBreak
apilocation:
- pdm.dll
helpviewer_keywords:
- IRemoteDebugApplication::CauseBreak
ms.assetid: 6a2c27bb-dca0-475c-9918-bdbb70a50d26
caps.latest.revision: 9
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: ce0ebe3b32b11bdd79884504233b3f4e09a035f8
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62944342"
---
# <a name="iremotedebugapplicationcausebreak"></a>IRemoteDebugApplication::CauseBreak
导致应用程序在最早的机会在调试器中中断。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT CauseBreak();  
```  
  
#### <a name="parameters"></a>参数  
 此方法需要任何参数。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 调用此方法不会导致立即中断应用程序。 如果应用程序当前未执行脚本代码，应用程序实际上将中断之前，可能需要很长时间。  
  
## <a name="see-also"></a>请参阅  
 [IRemoteDebugApplication 接口](../../winscript/reference/iremotedebugapplication-interface.md)