---
title: IActiveScriptSiteInterruptPoll：： QueryContinue |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptSiteInterruptPoll.QueryContinue
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScriptSiteInterruptPoll::QueryContinue
ms.assetid: 41ac3807-f8b4-4a0e-bcc6-556bc89f3904
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 7ce2ad61b54dce510035dd8e97d0dfb2accbf7a7
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72572236"
---
# <a name="iactivescriptsiteinterruptpollquerycontinue"></a>IActiveScriptSiteInterruptPoll::QueryContinue
允许主机指定脚本应终止。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT QueryContinue();  
```  
  
#### <a name="parameters"></a>参数  
 此方法不采用任何参数。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|值|说明|  
|-----------|-----------------|  
|`S_OK`|调用成功，主机允许脚本继续运行。|  
|`S_FALSE`|调用成功，并且宿主请求脚本终止。|  
  
## <a name="remarks"></a>备注  
 托管脚本应终止，除非 `S_OK``QueryContinue` 方法的返回值。 `S_FALSE` 的返回值指示宿主显式请求脚本终止。  
  
 多线程主机可以使用 `IActiveScript::InterruptScriptThread` 方法来终止脚本。  
  
## <a name="see-also"></a>另请参阅  
 [IActiveScriptSiteInterruptPoll 接口](../../winscript/reference/iactivescriptsiteinterruptpoll-interface.md)   
 [IActiveScript::InterruptScriptThread](../../winscript/reference/iactivescript-interruptscriptthread.md)