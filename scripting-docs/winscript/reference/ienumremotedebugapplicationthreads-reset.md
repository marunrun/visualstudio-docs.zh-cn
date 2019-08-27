---
title: IEnumRemoteDebugApplicationThreads::Reset | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IEnumRemoteDebugApplicationThreads.Reset
apilocation:
- pdm.dll
helpviewer_keywords:
- IEnumRemoteDebugApplicationThreads::Reset
ms.assetid: a6ad8a01-4cc0-4f9c-9cfe-c7448c753473
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 7a7c6fca01af5a3413ace6d95ca5c5879f4318ee
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62807181"
---
# <a name="ienumremotedebugapplicationthreadsreset"></a>IEnumRemoteDebugApplicationThreads::Reset
将枚举序列重置到开头。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT Reset();  
```  
  
#### <a name="parameters"></a>参数  
 此方法需要任何参数。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 此方法将枚举序列重置到开头。  
  
## <a name="see-also"></a>请参阅  
 [IEnumRemoteDebugApplicationThreads 接口](../../winscript/reference/ienumremotedebugapplicationthreads-interface.md)