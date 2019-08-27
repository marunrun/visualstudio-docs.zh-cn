---
title: IDebugApplication::HandleRuntimeError |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugApplication.HandleRuntimeError
apilocation:
- pdm.dll
helpviewer_keywords:
- IDebugApplication::HandleRuntimeError
ms.assetid: f8f3bbaf-09e5-4d01-8a35-f380bc7ff8ed
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: c2c9a8b15b5095ac346ba047d6668aada7647a31
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63412438"
---
# <a name="idebugapplicationhandleruntimeerror"></a>IDebugApplication::HandleRuntimeError
导致当前线程被阻塞，并将错误的通知发送到调试器 IDE。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT HandleRuntimeError(  
   IActiveScriptErrorDebug*  pErrorDebug,  
   IActiveScriptSite*        pScriptSite,  
   BREAKRESUMEACTION*        pbra,  
   ERRORRESUMEACTION*        perra,  
   BOOL*                     pfCallOnScriptError  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pErrorDebug`  
 [in]发生的错误。  
  
 `pScriptSite`  
 [in]线程的脚本站点。  
  
 `pbra`  
 [out]在调试器恢复应用程序时要执行的操作。  
  
 `perra`  
 [out]在调试器恢复应用程序，如果出现错误时要执行的操作。  
  
 `pfCallOnScriptError`  
 [out]这是标志`TRUE`如果引擎应调用`IActiveScriptSite::OnScriptError`方法。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 语言引擎会导致运行时错误的线程的上下文中调用此方法。 此方法会导致阻止当前线程，并发送错误通知发送到调试器 IDE。 当调试器 IDE 继续应用程序时，此方法返回要执行的操作。  
  
> [!NOTE]
> 在运行时错误可能由要执行此类任务，如枚举堆栈帧或对表达式求值的线程调用语言引擎。  
  
## <a name="see-also"></a>请参阅  
 [IDebugApplication 接口](../../winscript/reference/idebugapplication-interface.md)   
 [IActiveScriptErrorDebug 接口](../../winscript/reference/iactivescripterrordebug-interface.md)   
 [IActiveScriptSite](../../winscript/reference/iactivescriptsite.md)   
 [BREAKRESUMEACTION 枚举](../../winscript/reference/breakresumeaction-enumeration.md)   
 [ERRORRESUMEACTION 枚举](../../winscript/reference/errorresumeaction-enumeration.md)