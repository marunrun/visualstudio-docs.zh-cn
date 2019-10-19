---
title: IActiveScript：： Close |Microsoft Docs
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
ms.openlocfilehash: f858de42ef2948d218aac6c3194cc6af544da5e9
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72575782"
---
# <a name="iactivescriptclose"></a>IActiveScript::Close
使脚本引擎放弃当前加载的任何脚本，失去其状态，然后释放它所拥有的任何指向其他对象的接口指针，从而进入已关闭状态。 事件接收器、立即执行的脚本文本和已在进行的宏调用在状态更改之前完成（使用[IActiveScript：： InterruptScriptThread](../../winscript/reference/iactivescript-interruptscriptthread.md)取消正在运行的脚本线程）。 在释放接口之前，必须通过创建主机调用此方法，以防止出现循环引用问题。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT Close(void);  
```  
  
## <a name="return-value"></a>返回值  
 返回以下值之一：  
  
|“值”|含义|  
|-----------|-------------|  
|`S_OK`|成功。|  
|`E_UNEXPECTED`|不应进行调用（例如，脚本引擎已处于关闭状态）。|  
|`OLESCRIPT_S_PENDING`|此方法已成功排队，但尚未更改状态。 当状态更改时，将在[IActiveScriptSite：： OnStateChange](../../winscript/reference/iactivescriptsite-onstatechange.md)方法上回叫该站点。|  
|`S_FALSE`|方法已成功，但脚本已关闭。|  
  
## <a name="see-also"></a>请参阅  
 [IActiveScript](../../winscript/reference/iactivescript.md)