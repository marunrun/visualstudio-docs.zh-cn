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
ms.openlocfilehash: bc4ef840310c27ccbadce2ed4f632514b555ef98
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72575658"
---
# <a name="scriptthreadstate-enumeration"></a>SCRIPTTHREADSTATE 枚举
指定脚本引擎中的线程的状态。 此枚举由[IActiveScript：： GetScriptThreadState](../../winscript/reference/iactivescript-getscriptthreadstate.md)方法使用。  
  
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
|SCRIPTTHREADSTATE_NOTINSCRIPT|指定的线程当前未处理脚本事件、立即处理执行的脚本文本或运行脚本宏。|  
|SCRIPTTHREADSTATE_RUNNING|指定的线程正在积极地处理脚本事件、立即处理执行的脚本文本或运行脚本宏。|  
  
## <a name="see-also"></a>请参阅  
 [活动脚本常量、枚举和错误代码](../../winscript/reference/active-script-constants-enumerations-and-error-codes.md)