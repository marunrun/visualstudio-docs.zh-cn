---
title: IDebugApplication::QueryCurrentThreadIsDebuggerThread | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugApplication.QueryCurrentThreadIsDebuggerThread
apilocation:
- pdm.dll
helpviewer_keywords:
- IDebugApplication::QueryCurrentThreadIsDebuggerThread
ms.assetid: e22ad8a4-a8be-423d-80f2-28256a7448ed
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 2ed53bcdb5e0d613a757c0c60f4791b0c59e3476
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62990813"
---
# <a name="idebugapplicationquerycurrentthreadisdebuggerthread"></a>IDebugApplication::QueryCurrentThreadIsDebuggerThread
确定当前正在运行的线程是调试器线程。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT QueryCurrentThreadIsDebuggerThread();  
```  
  
#### <a name="parameters"></a>参数  
 此方法需要任何参数。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|该方法成功，并且当前正在运行的线程是调试器线程。|  
|`S_FALSE`|当前正在运行的线程不是调试器线程。|  
  
## <a name="remarks"></a>备注  
 此方法确定当前正在运行的线程是调试器线程。  
  
## <a name="see-also"></a>请参阅  
 [IDebugApplication 接口](../../winscript/reference/idebugapplication-interface.md)