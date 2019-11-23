---
title: IActiveScriptStats：： GetStat |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptStats.GetStat
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScriptStats::GetStat
ms.assetid: 31fd15b3-0713-4b55-b4f7-bfd7ea198493
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 096f1cf5b9bf8b5533bd5c36d33f014c747ff9aa
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72574340"
---
# <a name="iactivescriptstatsgetstat"></a>IActiveScriptStats::GetStat
返回标准脚本统计信息之一。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetStat(  
   DWORD   stid,  
   ULONG*  pluHi,  
   ULONG*  pluLo  
);  
```  
  
#### <a name="parameters"></a>参数  
 `stid`  
 中指定要返回的统计信息。 必须为值：  
  
|常量|值|说明|  
|--------------|-----------|-----------------|  
|SCRIPTSTAT_STATEMENT_COUNT|1|返回自脚本启动或重置统计信息以来执行的语句数。|  
  
 `pluHi`  
 弄表示统计信息的64位无符号整数的高32位。  
  
 `pluLo`  
 弄表示统计信息的64位无符号整数的低32位。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括但不限于下表中的值。  
  
|值|说明|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 此方法返回标准脚本统计信息之一。  
  
## <a name="see-also"></a>另请参阅  
 [IActiveScriptStats::GetStatEx](../../winscript/reference/iactivescriptstats-getstatex.md)   
 [IActiveScriptStats 接口](../../winscript/reference/iactivescriptstats-interface.md)