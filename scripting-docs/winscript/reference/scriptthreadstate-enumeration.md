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
ms.openlocfilehash: b4cebacf553b38e1edcbff66b6d17bc14156b10f
ms.sourcegitcommit: d8609a78b460d4783f5d59c0c89454910a4dbd21
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/14/2020
ms.locfileid: "88238772"
---
# <a name="scriptthreadstate-enumeration"></a>SCRIPTTHREADSTATE 枚举
指定脚本引擎中的线程的状态。 此枚举由 [IActiveScript：： GetScriptThreadState](../../winscript/reference/iactivescript-getscriptthreadstate.md) 方法使用。  
  
## <a name="syntax"></a>语法  
  
```cpp
typedef enum tagSCRIPTTHREADSTATE {  
    SCRIPTTHREADSTATE_NOTINSCRIPT  = 0,  
    SCRIPTTHREADSTATE_RUNNING      = 1  
} SCRIPTTHREADSTATE;  
```  
  
## <a name="enumeration-values"></a>枚举值  
  
|“值”|脚本线程状态|  
|-|-|  
|SCRIPTTHREADSTATE_NOTINSCRIPT|指定的线程当前未处理脚本事件、立即处理执行的脚本文本或运行脚本宏。|  
|SCRIPTTHREADSTATE_RUNNING|指定的线程正在积极地处理脚本事件、立即处理执行的脚本文本或运行脚本宏。|  
  
## <a name="see-also"></a>另请参阅  
 [活动脚本常量、枚举和错误代码](../../winscript/reference/active-script-constants-enumerations-and-error-codes.md)