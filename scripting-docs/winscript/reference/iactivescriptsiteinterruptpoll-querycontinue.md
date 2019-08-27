---
title: IActiveScriptSiteInterruptPoll::QueryContinue |Microsoft Docs
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
ms.openlocfilehash: 63ce45c0973d65d240136d7b42aef0c078b00c9a
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62992295"
---
# <a name="iactivescriptsiteinterruptpollquerycontinue"></a>IActiveScriptSiteInterruptPoll::QueryContinue
使宿主可以指定应终止脚本。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT QueryContinue();  
```  
  
#### <a name="parameters"></a>参数  
 此方法需要任何参数。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|调用成功，且主机允许脚本继续运行。|  
|`S_FALSE`|成功的调用和脚本终止的主机请求。|  
  
## <a name="remarks"></a>备注  
 除非承载的脚本应终止的返回值`QueryContinue`方法是`S_OK`。 返回值为`S_FALSE`指示主机显式请求脚本终止。  
  
 可以使用多线程的主机`IActiveScript::InterruptScriptThread`方法终止脚本。  
  
## <a name="see-also"></a>请参阅  
 [IActiveScriptSiteInterruptPoll 接口](../../winscript/reference/iactivescriptsiteinterruptpoll-interface.md)   
 [IActiveScript::InterruptScriptThread](../../winscript/reference/iactivescript-interruptscriptthread.md)