---
title: IDebugApplication110::CallableWaitForHandles |Microsoft Docs
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
ms.openlocfilehash: f74e3faa57e9ee4a38f77110334383bc2c72fe2f
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63446390"
---
# <a name="idebugapplication110callablewaitforhandles"></a>IDebugApplication110::CallableWaitForHandles
等待任何指定的句柄，以向发出信号，同时允许跨线程调用发布到此线程。 必须从调试器线程调用此方法。  
  
> [!IMPORTANT]
> [IDebugApplication110 接口](../../winscript/reference/idebugapplication110-interface.md)是实现由 PDM v11.0 和更高版本。 在 activdbg100.h 中发现。  
  
## <a name="syntax"></a>语法  
  
```cpp  
HRESULT CallableWaitForHandles([in] DWORD handleCount, [in, size_is(handleCount)] const HANDLE* pHandles, [out] DWORD* pIndex);  
```  
  
#### <a name="parameters"></a>参数  
 `handleCount`  
 若要等待的句柄数。  
  
 `pHandles`  
 组的句柄等待。  
  
 `pIndex`  
 HRESULT 值时的索引，则为 S_OK，`pHandles`已发出信号的句柄。  
  
## <a name="see-also"></a>请参阅  
 [IDebugApplication110 接口](../../winscript/reference/idebugapplication110-interface.md)