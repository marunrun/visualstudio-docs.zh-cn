---
title: SCRIPTSTATE 枚举 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- SCRIPTSTATE
apilocation:
- scrobj.dll
helpviewer_keywords:
- SCRIPTSTATE enum
ms.assetid: 5f5deb05-c4bb-4964-8077-e624c6b2a14e
caps.latest.revision: 7
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: d66d119c80c2b089c3d8a75a8e95d7095e9f9797
ms.sourcegitcommit: d8609a78b460d4783f5d59c0c89454910a4dbd21
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/14/2020
ms.locfileid: "88238798"
---
# <a name="scriptstate-enumeration"></a>SCRIPTSTATE 枚举
指定脚本引擎的状态。 此枚举由 [IActiveScript：： GetScriptState](../../winscript/reference/iactivescript-getscriptstate.md) 、 [IActiveScript：： SetScriptState](../../winscript/reference/iactivescript-setscriptstate.md) 和 [IActiveScriptSite：： OnStateChange](../../winscript/reference/iactivescriptsite-onstatechange.md) 方法使用。  
  
## <a name="syntax"></a>语法  
  
```cpp
typedef enum tagSCRIPTSTATE {  
    SCRIPTSTATE_UNINITIALIZED = 0,  
    SCRIPTSTATE_INITIALIZED   = 5,  
    SCRIPTSTATE_STARTED       = 1,  
    SCRIPTSTATE_CONNECTED     = 2,  
    SCRIPTSTATE_DISCONNECTED  = 3,  
    SCRIPTSTATE_CLOSED        = 4  
} SCRIPTSTATE;  
```  
  
## <a name="enumeration-values"></a>枚举值  
  
|“值”|脚本状态|  
|-|-|  
|SCRIPTSTATE_UNINITIALIZED|脚本刚刚创建，但尚未使用 `IPersist*` 接口和 [IActiveScript：： SetScriptSite](../../winscript/reference/iactivescript-setscriptsite.md) 进行初始化。|  
|SCRIPTSTATE_INITIALIZED|脚本已初始化，但没有在连接到其他对象 (或接收事件) 或执行任何代码的情况下运行。 可以通过调用 [IActiveScriptParse：:P arsescripttext](../../winscript/reference/iactivescriptparse-parsescripttext.md) 方法查询代码的执行。|  
|SCRIPTSTATE_STARTED|脚本可以执行代码，但尚未接收 [IActiveScript：： AddNamedItem](../../winscript/reference/iactivescript-addnameditem.md) 方法添加的对象的事件。|  
|SCRIPTSTATE_CONNECTED|加载并连接脚本以接收事件。|  
|SCRIPTSTATE_DISCONNECTED|脚本已加载并具有运行时执行状态，但暂时与接收事件断开连接。|  
|SCRIPTSTATE_CLOSED|脚本已关闭。 脚本引擎不再运行，并不再针对多数方法返回错误。|  
  
## <a name="see-also"></a>另请参阅  
 [活动脚本常量、枚举和错误代码](../../winscript/reference/active-script-constants-enumerations-and-error-codes.md)