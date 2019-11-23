---
title: IDebugApplication：： HandleRuntimeError |Microsoft Docs
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
ms.openlocfilehash: 2fd4ba2b811cd6c4e38c10a0c68c5808f2c0870a
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72574321"
---
# <a name="idebugapplicationhandleruntimeerror"></a>IDebugApplication::HandleRuntimeError
导致当前线程阻塞并将错误通知发送到调试器 IDE。  
  
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
 中发生的错误。  
  
 `pScriptSite`  
 中线程的脚本站点。  
  
 `pbra`  
 弄调试器恢复应用程序时要执行的操作。  
  
 `perra`  
 弄调试器恢复应用程序（如果出现错误）时要执行的操作。  
  
 `pfCallOnScriptError`  
 弄如果引擎应调用 `IActiveScriptSite::OnScriptError` 方法，则 `TRUE` 标志。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|值|说明|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 语言引擎在导致运行时错误的线程的上下文中调用此方法。 此方法使当前线程阻止并发送要发送到调试器 IDE 的错误通知。 调试器 IDE 恢复应用程序时，此方法将返回，并返回要执行的操作。  
  
> [!NOTE]
> 在运行时错误时，可以通过线程调用语言引擎来执行枚举堆栈帧或计算表达式等任务。  
  
## <a name="see-also"></a>另请参阅  
 [IDebugApplication 接口](../../winscript/reference/idebugapplication-interface.md)   
 [IActiveScriptErrorDebug 接口](../../winscript/reference/iactivescripterrordebug-interface.md)   
 [IActiveScriptSite](../../winscript/reference/iactivescriptsite.md)   
 [BREAKRESUMEACTION 枚举](../../winscript/reference/breakresumeaction-enumeration.md)   
 [ERRORRESUMEACTION 枚举](../../winscript/reference/errorresumeaction-enumeration.md)