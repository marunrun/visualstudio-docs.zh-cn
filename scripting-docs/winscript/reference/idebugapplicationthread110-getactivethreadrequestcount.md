---
title: IDebugApplicationThread110::GetActiveThreadRequestCount | Microsoft Docs
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
ms.openlocfilehash: 3df2f0c44e42cf9e2c2aa846db4b88821fd73996
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63440570"
---
# <a name="idebugapplicationthread110getactivethreadrequestcount"></a>IDebugApplicationThread110::GetActiveThreadRequestCount
从 PDM 的线程切换当前正在处理的机制返回线程请求的数。 此数字通常是 0 或 1。 但是，如果数字可能会更高版本一个线程调用开始处理，但触发同步调用线程，带或否则为将线程挂起并允许再次处理的传入呼叫 (例如，通过触发[IRemoteDebugApplicationEvents 接口](../../winscript/reference/iremotedebugapplicationevents-interface.md)事件，该调试器线程上发出事件)。  
  
> [!IMPORTANT]
> [IDebugApplicationThread110 接口](../../winscript/reference/idebugapplicationthread110-interface.md)是实现由 PDM v11.0 和更高版本。 在 activdbg100.h 中发现。  
  
## <a name="syntax"></a>语法  
  
```cpp  
HRESULT GetActiveThreadRequestCount([out, annotation("_Out_")] UINT * puiThreadRequests);  
```  
  
#### <a name="parameters"></a>参数  
 `puiThreadRequests`  
 [out]线程请求数。  
  
## <a name="see-also"></a>请参阅  
 [IDebugApplicationThread110 接口](../../winscript/reference/idebugapplicationthread110-interface.md)