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
ms.openlocfilehash: fe6a05c5e73d26a8daa9e46c317422d85d1c40be
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62840156"
---
# <a name="scriptstate-enumeration"></a>SCRIPTSTATE 枚举
指定脚本引擎的状态。 此枚举由[IActiveScript::GetScriptState](../../winscript/reference/iactivescript-getscriptstate.md) ， [iactivescript:: Setscriptstate](../../winscript/reference/iactivescript-setscriptstate.md) ，并[IActiveScriptSite::OnStateChange](../../winscript/reference/iactivescriptsite-onstatechange.md)方法。  
  
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
  
|||  
|-|-|  
|SCRIPTSTATE_UNINITIALIZED|脚本刚刚创建，但尚未被初始化使用`IPersist*`接口和[iactivescript:: Setscriptsite](../../winscript/reference/iactivescript-setscriptsite.md) 。|  
|SCRIPTSTATE_INITIALIZED|脚本已初始化但未运行 （连接到其他对象或接收器事件） 或执行任何代码。 代码可以通过调用查询的执行[iactivescriptparse:: Parsescripttext](../../winscript/reference/iactivescriptparse-parsescripttext.md)方法。|  
|SCRIPTSTATE_STARTED|脚本可执行代码，但尚不接收由添加的对象的事件[iactivescript:: Addnameditem](../../winscript/reference/iactivescript-addnameditem.md)方法。|  
|SCRIPTSTATE_CONNECTED|脚本已加载并连接接收器事件。|  
|SCRIPTSTATE_DISCONNECTED|脚本加载和运行时执行状态，但暂时与接收器事件断开连接。|  
|SCRIPTSTATE_CLOSED|脚本已关闭。 脚本引擎不再运行，并不再针对多数方法返回错误。|  
  
## <a name="see-also"></a>请参阅  
 [活动脚本常量、枚举和错误代码](../../winscript/reference/active-script-constants-enumerations-and-error-codes.md)