---
title: IEnumRemoteDebugApplicationThreads::Skip | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IEnumRemoteDebugApplicationThreads.Skip
apilocation:
- pdm.dll
helpviewer_keywords:
- IEnumRemoteDebugApplicationThreads::Skip
ms.assetid: bb13a18b-bcf8-4542-8b1a-55a4f2769536
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: a8ef51b7e1b5e038534fda6e3585304515c7d165
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62807168"
---
# <a name="ienumremotedebugapplicationthreadsskip"></a>IEnumRemoteDebugApplicationThreads::Skip
将跳过枚举序列中的指定的段数。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT Skip(  
   ULONG  celt  
);  
```  
  
#### <a name="parameters"></a>参数  
 `celt`  
 [in]若要跳过枚举序列中的段的数目。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 此方法将跳过枚举序列中的指定的段数。  
  
## <a name="see-also"></a>请参阅  
 [IEnumRemoteDebugApplicationThreads 接口](../../winscript/reference/ienumremotedebugapplicationthreads-interface.md)