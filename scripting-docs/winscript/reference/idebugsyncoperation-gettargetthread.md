---
title: IDebugSyncOperation：： GetTargetThread |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugSyncOperation.GetTargetThread
apilocation:
- jscript.dll
helpviewer_keywords:
- IDebugSyncOperation::GetTargetThread
ms.assetid: e6eeeb90-b5ed-4727-8434-fa3186c25013
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: d6675356439d60e5c204760e69640a0f50bf40fc
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72576676"
---
# <a name="idebugsyncoperationgettargetthread"></a>IDebugSyncOperation::GetTargetThread
返回此同步操作的目标应用程序线程。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetTargetThread(  
   IDebugApplicationThread**  ppatTarget  
);  
```  
  
#### <a name="parameters"></a>参数  
 `ppatTarget`  
 弄此同步操作的目标应用程序线程。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 此方法返回此同步操作的目标应用程序线程。  
  
## <a name="see-also"></a>请参阅  
 [IDebugSyncOperation 接口](../../winscript/reference/idebugsyncoperation-interface.md)