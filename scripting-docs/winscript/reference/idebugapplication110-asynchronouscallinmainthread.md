---
title: IDebugApplication110::AsynchronousCallInMainThread | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IDebugApplication110::AsynchronousCallInMainThread
ms.assetid: 13b80ff0-4bed-48c1-8031-d4147b51bf6c
caps.latest.revision: 6
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: d1b5e52d65a5fd70c4ec7de9ced9a0175940d93f
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63446405"
---
# <a name="idebugapplication110asynchronouscallinmainthread"></a>IDebugApplication110::AsynchronousCallInMainThread
在主线程上进行异步调用。  
  
> [!IMPORTANT]
> [IDebugApplication110 接口](../../winscript/reference/idebugapplication110-interface.md)是实现由 PDM v11.0 和更高版本。 在 activdbg100.h 中发现。  
  
## <a name="syntax"></a>语法  
  
```cpp  
HRESULT AsynchronousCallInMainThread([in] IDebugThreadCall* pptc, [in] DWORD_PTR dwParam1, [in] DWORD_PTR dwParam2, [in] DWORD_PTR dwParam3);  
```  
  
#### <a name="parameters"></a>参数  
 `pptc`  
 [IDebugThreadCall 接口](../../winscript/reference/idebugthreadcall-interface.md)对象调用。  
  
 `dwParam1`  
 调用的第一个参数。  
  
 `dwParam1`  
 调用的第一个参数。  
  
 `dwParam2`  
 调用的第二个参数。  
  
 `dwParam3`  
 调用的第三个参数。  
  
## <a name="see-also"></a>请参阅  
 [IDebugApplication110 接口](../../winscript/reference/idebugapplication110-interface.md)