---
title: IEnumRemoteDebugApplications：： Skip |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IEnumRemoteDebugApplications.Skip
apilocation:
- scrobj.dll
helpviewer_keywords:
- IEnumRemoteDebugApplications::Skip
ms.assetid: 9f6578d9-8de5-419c-b1b5-7cb07b6367fb
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 0d1b4d183d3a4009302f207f530ce9b2391e2037
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72575203"
---
# <a name="ienumremotedebugapplicationsskip"></a>IEnumRemoteDebugApplications::Skip
跳过枚举序列中指定数量的段。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT Skip(  
   ULONG  celt  
);  
```  
  
#### <a name="parameters"></a>参数  
 `celt`  
 中枚举序列中要跳过的段数。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 此方法跳过枚举序列中指定数量的段。  
  
## <a name="see-also"></a>请参阅  
 [IEnumRemoteDebugApplications 接口](../../winscript/reference/ienumremotedebugapplications-interface.md)