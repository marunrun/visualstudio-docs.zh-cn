---
title: IEnumRemoteDebugApplications::Next | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IEnumRemoteDebugApplications.Next
apilocation:
- scrobj.dll
helpviewer_keywords:
- IEnumRemoteDebugApplications::Next
ms.assetid: 33f6c620-6dd3-4057-b982-b88a7a1f02b4
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 9b14874891e739fc95b877e41e76559a1ab0060a
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62963232"
---
# <a name="ienumremotedebugapplicationsnext"></a>IEnumRemoteDebugApplications::Next
`Next`方法检索枚举序列中的指定的段数。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT Next(  
   ULONG                      celt,  
   IRemoteDebugApplication**  ppda,  
   ULONG*                     pceltFetched  
);  
```  
  
#### <a name="parameters"></a>参数  
 `celt`  
 [in]若要检索的段的数目。  
  
 `ppda`  
 [out]返回一个数组`IRemoteDebugApplication`表示要检索的段的接口。  
  
 `pceltFetched`  
 [out]提取的枚举器实际段数。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 此方法检索枚举序列中的指定的段数。  
  
## <a name="see-also"></a>请参阅  
 [IEnumRemoteDebugApplications 接口](../../winscript/reference/ienumremotedebugapplications-interface.md)