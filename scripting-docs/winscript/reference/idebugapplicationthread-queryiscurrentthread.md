---
title: IDebugApplicationThread::QueryIsCurrentThread | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugApplicationThread.QueryIsCurrentThread
apilocation:
- pdm.dll
helpviewer_keywords:
- IDebugApplicationThread::QueryIsCurrentThread
ms.assetid: 1580d3aa-3be8-4779-ac7b-41ab5c9edede
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 7d8871d197d662d179fa4d1ed8d420c48ecc5ab3
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62974561"
---
# <a name="idebugapplicationthreadqueryiscurrentthread"></a>IDebugApplicationThread::QueryIsCurrentThread
确定此线程是否当前正在运行的线程。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT QueryIsCurrentThread();  
```  
  
#### <a name="parameters"></a>参数  
 此方法需要任何参数。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|该方法成功，这是当前运行的线程。|  
|`S_FALSE`|这不是当前运行的线程。|  
  
## <a name="remarks"></a>备注  
 此方法确定此线程是否当前正在运行的线程。  
  
## <a name="see-also"></a>请参阅  
 [IDebugApplicationThread 接口](../../winscript/reference/idebugapplicationthread-interface.md)