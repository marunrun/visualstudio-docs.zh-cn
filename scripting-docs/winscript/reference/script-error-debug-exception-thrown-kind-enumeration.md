---
title: SCRIPT_ERROR_DEBUG_EXCEPTION_THROWN_KIND 枚举 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: b3aa4966-e110-4b30-b368-1281a9740dbd
caps.latest.revision: 4
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 8eb089efbf608b488465809f997ffc82fc2c2e3c
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72574401"
---
# <a name="script_error_debug_exception_thrown_kind-enumeration"></a>SCRIPT_ERROR_DEBUG_EXCEPTION_THROWN_KIND 枚举
显示已引发异常的类型。 此枚举由[IActiveScriptErrorDebug110：： GetExceptionThrownKind](../../winscript/reference/iactivescripterrordebug110-getexceptionthrownkind.md)方法使用。  
  
> [!IMPORTANT]
> 这些常量由 PDM 11.0 和更高版本实现。 在 activdbg100.h 中发现。  
  
## <a name="syntax"></a>语法  
  
```cpp
typedef SCRIPT_ERROR_DEBUG_EXCEPTION_THROWN_KIND  
```  
  
## <a name="members"></a>Members  
  
|成员|“值”|描述|  
|------------|-----------|-----------------|  
|ETK_FIRST_CHANCE|0x00000000|此异常是首次异常。|  
|ETK_USER_UNHANDLED|0x00000001|此异常未在用户代码中进行处理。|  
|ETK_UNHANDLED|0x00000002|此异常未在代码中进行处理。|  
  
## <a name="see-also"></a>请参阅  
 [IActiveScriptErrorDebug110 接口](../../winscript/reference/iactivescripterrordebug110-interface.md)