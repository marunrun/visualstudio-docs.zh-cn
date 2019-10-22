---
title: IDebugAsyncOperation：： Start |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugAsyncOperation.Start
apilocation:
- pdm.dll
helpviewer_keywords:
- IDebugAsyncOperation::Start
ms.assetid: a7272364-28e0-48ae-8405-b8bce8a6b9fd
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 485eb34ebe200e7f7898d9338effed37cbf2aa10
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72573242"
---
# <a name="idebugasyncoperationstart"></a>IDebugAsyncOperation::Start
导致开始异步操作。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT Start(  
   IDebugAsyncOperationCallBack*  padocb  
);  
```  
  
#### <a name="parameters"></a>参数  
 `padocb`  
 从此操作接收状态事件的回调接口。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
|`E_UNEXPECTED`|操作已挂起。|  
  
## <a name="remarks"></a>备注  
 此方法导致在从 `IDebugSyncOperation::GetTargetThread` 获取的线程中以异步方式调用 `IDebugSyncOperation::Execute`。 只应从调试器线程内调用此方法;否则，在操作完成之前，不会返回。  
  
## <a name="see-also"></a>请参阅  
 [IDebugAsyncOperation：： Abort](../../winscript/reference/idebugasyncoperation-abort.md)    
 [IDebugAsyncOperation 接口](../../winscript/reference/idebugasyncoperation-interface.md)   
 [IDebugSyncOperation：： Execute](../../winscript/reference/idebugsyncoperation-execute.md)    
 [IDebugSyncOperation::GetTargetThread](../../winscript/reference/idebugsyncoperation-gettargetthread.md)