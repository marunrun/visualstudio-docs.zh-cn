---
title: IDebugAsyncOperation::Start | Microsoft Docs
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
ms.openlocfilehash: b3e02869abab65878412f96b77d5782b9717a1b6
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62821923"
---
# <a name="idebugasyncoperationstart"></a>IDebugAsyncOperation::Start
将导致异步操作以开始。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT Start(  
   IDebugAsyncOperationCallBack*  padocb  
);  
```  
  
#### <a name="parameters"></a>参数  
 `padocb`  
 接收来自此操作的状态事件回调接口。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
|`E_UNEXPECTED`|操作已处于挂起状态。|  
  
## <a name="remarks"></a>备注  
 此方法将导致`IDebugSyncOperation::Execute`获取从线程中异步调用`IDebugSyncOperation::GetTargetThread`。 调用此方法应只从在调试程序线程中;否则，它将不返回直到完成该操作。  
  
## <a name="see-also"></a>请参阅  
 [IDebugAsyncOperation::Abort](../../winscript/reference/idebugasyncoperation-abort.md)   
 [IDebugAsyncOperation 接口](../../winscript/reference/idebugasyncoperation-interface.md)   
 [IDebugSyncOperation::Execute](../../winscript/reference/idebugsyncoperation-execute.md)   
 [IDebugSyncOperation::GetTargetThread](../../winscript/reference/idebugsyncoperation-gettargetthread.md)