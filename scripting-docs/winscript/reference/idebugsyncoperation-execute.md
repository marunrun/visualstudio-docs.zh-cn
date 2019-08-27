---
title: IDebugSyncOperation::Execute | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugSyncOperation.Execute
apilocation:
- jscript.dll
helpviewer_keywords:
- IDebugSyncOperation::Execute
ms.assetid: a45b8c7d-c51a-4098-877f-fbec2f1f6947
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: a2bc204169ff94a240e363eb8caa35ec8c7de9be
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63004873"
---
# <a name="idebugsyncoperationexecute"></a>IDebugSyncOperation::Execute
以同步方式执行该操作并返回。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT Execute(  
   IUnknown**  ppunkResult  
);  
```  
  
#### <a name="parameters"></a>参数  
 `ppunkResult`  
 [out]该操作返回的对象参数。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
|`E_ABORT`|通过调用中止了此操作`IDebugSyncOperation::InProgressAbort`方法。|  
  
## <a name="remarks"></a>备注  
 进程调试管理器中的目标线程调用`Execute`方法以同步方式。  
  
## <a name="see-also"></a>请参阅  
 [IDebugSyncOperation 接口](../../winscript/reference/idebugsyncoperation-interface.md)