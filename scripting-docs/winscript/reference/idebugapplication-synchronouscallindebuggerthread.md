---
title: IDebugApplication::SynchronousCallInDebuggerThread | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugApplication.SynchronousCallInDebuggerThread
apilocation:
- pdm.dll
helpviewer_keywords:
- IDebugApplication::SynchronousCallInDebuggerThread
ms.assetid: 9daa1722-f25a-4691-aefc-fd28672fb883
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: d5460efaa3448c7812707e0baa7b2f5afe1d27a0
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62990559"
---
# <a name="idebugapplicationsynchronouscallindebuggerthread"></a>IDebugApplication::SynchronousCallInDebuggerThread
提供了为使调用方在调试器线程中运行代码的机制。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT SynchronousCallInDebuggerThread(  
   IDebugThreadCall*  pptc,  
   DWORD_PTR          dwParam1,  
   DWORD_PTR          dwParam2,  
   DWORD_PTR          dwParam3  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pptc`  
 [in]要调用的对象。  
  
 `dwParam1`  
 [in]第一个参数传递给`IDebugThreadCall::ThreadCallHandler`方法。  
  
 `dwParam2`  
 [in]第二个参数传递给`IDebugThreadCall::ThreadCallHandler`方法。  
  
 `dwParam3`  
 [in]第三个参数传递给`IDebugThreadCall::ThreadCallHandler`方法。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 语言引擎和主机通常使用此方法以实现基于其单个线程实现自由线程对象。  
  
## <a name="see-also"></a>请参阅  
 [IDebugApplication 接口](../../winscript/reference/idebugapplication-interface.md)   
 [IDebugThreadCall 接口](../../winscript/reference/idebugthreadcall-interface.md)