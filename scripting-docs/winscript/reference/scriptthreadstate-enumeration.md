---
title: SCRIPTTHREADSTATE 枚举 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- SCRIPTTHREADSTATE
apilocation:
- scrobj.dll
helpviewer_keywords:
- SCRIPTTHREADSTATE enum
ms.assetid: 975ec66b-c095-40ac-8ba9-631adb97b589
caps.latest.revision: 7
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 906a309b25a1fe606fb37f8cbab70040e5a4c46f
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62840182"
---
# <a name="scriptthreadstate-enumeration"></a>SCRIPTTHREADSTATE 枚举
脚本引擎中指定的线程的状态。 此枚举由[IActiveScript::GetScriptThreadState](../../winscript/reference/iactivescript-getscriptthreadstate.md)方法。  
  
## <a name="syntax"></a>语法  
  
```cpp
typedef enum tagSCRIPTTHREADSTATE {  
    SCRIPTTHREADSTATE_NOTINSCRIPT  = 0,  
    SCRIPTTHREADSTATE_RUNNING      = 1  
} SCRIPTTHREADSTATE;  
```  
  
## <a name="enumeration-values"></a>枚举值  
  
|||  
|-|-|  
|SCRIPTTHREADSTATE_NOTINSCRIPT|指定的线程当前不是维护脚本化的事件，处理立即执行脚本文本，或运行脚本宏。|  
|SCRIPTTHREADSTATE_RUNNING|指定的线程主动维护脚本化的事件，处理立即执行脚本文本，或运行脚本宏。|  
  
## <a name="see-also"></a>请参阅  
 [活动脚本常量、枚举和错误代码](../../winscript/reference/active-script-constants-enumerations-and-error-codes.md)