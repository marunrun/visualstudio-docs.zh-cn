---
title: IDebugApplication110：： SynchronousCallInMainThread |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IDebugApplication110::SynchronousCallInMainThread
ms.assetid: 57475ae5-1520-45ef-800d-ccfc6235a5d1
caps.latest.revision: 5
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: db2b94d51cc5c9a65355aae7405fb162f564e0cc
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72573649"
---
# <a name="idebugapplication110synchronouscallinmainthread"></a>IDebugApplication110::SynchronousCallInMainThread
在主线程上进行同步调用。  
  
> [!IMPORTANT]
> [IDebugApplication110 接口](../../winscript/reference/idebugapplication110-interface.md)由 PDM 11.0 和更高版本实现。 在 activdbg100.h 中发现。  
  
## <a name="syntax"></a>语法  
  
```cpp  
HRESULT SynchronousCallInMainThread([in] IDebugThreadCall* pptc, [in] DWORD_PTR dwParam1, [in] DWORD_PTR dwParam2, [in] DWORD_PTR dwParam3);  
```  
  
#### <a name="parameters"></a>参数  
 `pptc`  
 要调用的[IDebugThreadCall 接口](../../winscript/reference/idebugthreadcall-interface.md)对象。  
  
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