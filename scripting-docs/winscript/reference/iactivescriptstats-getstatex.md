---
title: IActiveScriptStats：： GetStatEx |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptStats.GetStatEx
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScriptStats::GetStatEx
ms.assetid: f526f51d-8ab5-49ef-a8f7-ae0ac1cb46e4
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 2ca7cdb81fd7e228b26bfaa12d45e81335674a74
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72576122"
---
# <a name="iactivescriptstatsgetstatex"></a>IActiveScriptStats::GetStatEx
返回自定义脚本统计信息。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetStatEx(  
   REFGUID  guid,  
   ULONG*   pluHi,  
   ULONG*   pluLo  
);  
```  
  
#### <a name="parameters"></a>参数  
 `guid`  
 中指定要返回的统计信息。 完全由引擎定义与特定 GUID 对应的统计信息的语义。  
  
 `pluHi`  
 弄表示统计信息的64位无符号整数的高32位。  
  
 `pluLo`  
 弄表示统计信息的64位无符号整数的低32位。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
|`E_NOTIMPL`|未实现该方法。|  
  
## <a name="remarks"></a>备注  
 此方法允许自定义脚本引擎返回对自定义主机有意义的统计信息。  
  
> [!NOTE]
> 当前未实现此方法。  
  
## <a name="see-also"></a>请参阅  
 [IActiveScriptStats：： GetStat](../../winscript/reference/iactivescriptstats-getstat.md)    
 [IActiveScriptStats 接口](../../winscript/reference/iactivescriptstats-interface.md)