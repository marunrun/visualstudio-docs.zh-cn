---
title: IDebugApplication：： StepOutComplete |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugApplication.StepOutComplete
apilocation:
- pdm.dll
helpviewer_keywords:
- IDebugApplication::StepOutComplete
ms.assetid: 9675b214-7be5-4cf7-a63f-7865f3c54371
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: f50d7e8a8936e52f4177450e7d163c4cfeaa55df
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72571037"
---
# <a name="idebugapplicationstepoutcomplete"></a>IDebugApplication::StepOutComplete
向进程调试管理器通知单步模式下的语言引擎将要返回到其调用方。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT StepOutComplete();  
```  
  
#### <a name="parameters"></a>参数  
 此方法不采用任何参数。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 语言引擎仅在单步模式下调用此方法，然后再返回到其调用方。 进程调试管理器使用此机会通知应在第一次机会时中断的所有其他脚本引擎。 此方法是实现跨语言步骤模式的方式。  
  
## <a name="see-also"></a>请参阅  
 [IDebugApplication 接口](../../winscript/reference/idebugapplication-interface.md)