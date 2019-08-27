---
title: IActiveScript::Close | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScript.Close
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScript_Close
ms.assetid: cc7dd63b-1d7e-410a-857b-09ea3aade275
caps.latest.revision: 6
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 53b71471ada55751de301391fdcc70387c1bb6c2
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62935674"
---
# <a name="iactivescriptclose"></a>IActiveScript::Close
使脚本引擎放弃所有当前加载的脚本，会丢失其状态，并释放任何对其他对象，因此进入关闭的状态的接口指针。 事件接收器、 立即执行的脚本文本和宏已正在进行的调用完成之前的状态更改 (使用[iactivescript:: Interruptscriptthread](../../winscript/reference/iactivescript-interruptscriptthread.md)取消正在运行的脚本线程)。 接口发布若要避免循环引用问题之前，必须通过创建主机调用此方法。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT Close(void);  
```  
  
## <a name="return-value"></a>返回值  
 返回以下值之一：  
  
|“值”|含义|  
|-----------|-------------|  
|`S_OK`|成功。|  
|`E_UNEXPECTED`|不应在调用 （例如，脚本引擎本来就处于关闭状态）。|  
|`OLESCRIPT_S_PENDING`|已成功，该方法已排入队列但尚未未更改状态。 当状态更改的站点是上要回拨[IActiveScriptSite::OnStateChange](../../winscript/reference/iactivescriptsite-onstatechange.md)方法。|  
|`S_FALSE`|该方法成功，但该脚本已关闭。|  
  
## <a name="see-also"></a>请参阅  
 [IActiveScript](../../winscript/reference/iactivescript.md)