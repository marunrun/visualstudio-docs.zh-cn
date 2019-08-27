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
ms.openlocfilehash: 3be6989195eacdd4d70bd13790d55e4f6cfc769d
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63443639"
---
# <a name="scripterrordebugexceptionthrownkind-enumeration"></a>SCRIPT_ERROR_DEBUG_EXCEPTION_THROWN_KIND 枚举
显示已引发异常的类型。 此枚举由[IActiveScriptErrorDebug110::GetExceptionThrownKind](../../winscript/reference/iactivescripterrordebug110-getexceptionthrownkind.md)方法。  
  
> [!IMPORTANT]
> 这些常量由 PDM 11.0 和更高版本实现。 在 activdbg100.h 中发现。  
  
## <a name="syntax"></a>语法  
  
```cpp
typedef SCRIPT_ERROR_DEBUG_EXCEPTION_THROWN_KIND  
```  
  
## <a name="members"></a>成员  
  
|成员|“值”|描述|  
|------------|-----------|-----------------|  
|ETK_FIRST_CHANCE|0x00000000|此异常是首次异常。|  
|ETK_USER_UNHANDLED|0x00000001|此异常未在用户代码中进行处理。|  
|ETK_UNHANDLED|0x00000002|此异常未在代码中进行处理。|  
  
## <a name="see-also"></a>请参阅  
 [IActiveScriptErrorDebug110 接口](../../winscript/reference/iactivescripterrordebug110-interface.md)