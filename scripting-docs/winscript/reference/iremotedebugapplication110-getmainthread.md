---
title: IRemoteDebugApplication110::GetMainThread | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IRemoteDebugApplication110::GetMainThread
ms.assetid: 9982acc9-3d35-4dcf-8ca9-662469de4072
caps.latest.revision: 4
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 8a4b51d87f89d77bebf065ce5f52a297ada333d3
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383502"
---
# <a name="iremotedebugapplication110getmainthread"></a>IRemoteDebugApplication110::GetMainThread
主线程返回对调用的宿主[SetSite](http://go.microsoft.com/fwlink/?LinkId=232439)，否则将返回 E_FAIL。  
  
> [!IMPORTANT]
> [IRemoteDebugApplication 接口](../../winscript/reference/iremotedebugapplication-interface.md)是实现由 PDM v11.0 和更高版本。 在 activdbg100.h 中发现。  
  
## <a name="syntax"></a>语法  
  
```cpp  
HRESULT GetMainThread([out] IRemoteDebugApplicationThread **ppThread);  
```  
  
#### <a name="parameters"></a>参数  
 `ppThread`  
 [out]主[IRemoteDebugApplicationThread 接口](../../winscript/reference/iremotedebugapplicationthread-interface.md)。  
  
## <a name="see-also"></a>请参阅  
 [IRemoteDebugApplication 接口](../../winscript/reference/iremotedebugapplication-interface.md)   
 [IRemoteDebugApplication110 接口](../../winscript/reference/iremotedebugapplication110-interface.md)