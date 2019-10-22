---
title: IDebugApplicationThread110：： GetActiveThreadRequestCount |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IDebugApplicationThread110::GetActiveThreadRequestCount
ms.assetid: 025d2072-1d7f-4448-8aa3-38a014313570
caps.latest.revision: 6
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: e7f038c1d0958701a14899825a2adb0a11cf604d
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72574477"
---
# <a name="idebugapplicationthread110getactivethreadrequestcount"></a>IDebugApplicationThread110::GetActiveThreadRequestCount
返回当前正在处理的 PDM 线程切换机制中的线程请求数。 此数字通常为0或1。 但是，如果一个线程调用开始处理，但触发线程的同步调用，或以其他方式挂起线程，并允许再次处理传入调用（例如，通过触发[IRemoteDebugApplicationEventsInterface](../../winscript/reference/iremotedebugapplicationevents-interface.md)事件，在调试器线程上发出。  
  
> [!IMPORTANT]
> [IDebugApplicationThread110 接口](../../winscript/reference/idebugapplicationthread110-interface.md)由 PDM 11.0 和更高版本实现。 在 activdbg100.h 中发现。  
  
## <a name="syntax"></a>语法  
  
```cpp  
HRESULT GetActiveThreadRequestCount([out, annotation("_Out_")] UINT * puiThreadRequests);  
```  
  
#### <a name="parameters"></a>参数  
 `puiThreadRequests`  
 弄线程请求数。  
  
## <a name="see-also"></a>请参阅  
 [IDebugApplicationThread110 接口](../../winscript/reference/idebugapplicationthread110-interface.md)