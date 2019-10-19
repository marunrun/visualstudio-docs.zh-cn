---
title: IDebugApplication110：： CallableWaitForHandles |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IDebugApplication110::CallableWaitForHandles
ms.assetid: 02e79b60-0d67-47f9-bf78-b65a02c9c014
caps.latest.revision: 4
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 22af0e9dcf548bbd2f0f8c179b4889d5294eb284
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72575078"
---
# <a name="idebugapplication110callablewaitforhandles"></a>IDebugApplication110::CallableWaitForHandles
等待任何指定的句柄终止，同时允许跨线程调用发送到此线程。 必须从调试器线程调用此方法。  
  
> [!IMPORTANT]
> [IDebugApplication110 接口](../../winscript/reference/idebugapplication110-interface.md)由 PDM 11.0 和更高版本实现。 在 activdbg100.h 中发现。  
  
## <a name="syntax"></a>语法  
  
```cpp  
HRESULT CallableWaitForHandles([in] DWORD handleCount, [in, size_is(handleCount)] const HANDLE* pHandles, [out] DWORD* pIndex);  
```  
  
#### <a name="parameters"></a>参数  
 `handleCount`  
 要等待的句柄数。  
  
 `pHandles`  
 要等待的句柄集。  
  
 `pIndex`  
 如果 HRESULT 值为 S_OK，则为已发出信号的句柄 `pHandles` 的索引。  
  
## <a name="see-also"></a>请参阅  
 [IDebugApplication110 接口](../../winscript/reference/idebugapplication110-interface.md)