---
title: IActiveScriptSiteDebugEx：： OnCanNotJITScriptErrorDebug |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptSiteDebugEx.OnCanNotJITScriptErrorDebug
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScriptSiteDebugEx::OnCanNotJITScriptErrorDebug
ms.assetid: 83f81476-bf12-47f2-897d-1d37d21137d4
caps.latest.revision: 6
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 7358d2b372f0801b8c45816e1fc36018b37799b2
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72572177"
---
# <a name="iactivescriptsitedebugexoncannotjitscripterrordebug"></a>IActiveScriptSiteDebugEx::OnCanNotJITScriptErrorDebug
当进程调试管理器找不到实时脚本调试器时，向宿主通知脚本运行时错误。  
  
 若要在主机中实现调试器，应处理[IActiveScriptSiteDebug：： OnScriptErrorDebug](../../winscript/reference/iactivescriptsitedebug-onscripterrordebug.md)。 根据用户操作，主机可以附加调试器并返回，也可以在 OnScriptErrorDebug `pfEnterDebugger` 参数中返回调试程序的启动。 还应实现此接口，以获取有关运行时错误的通知，即使没有进程调试管理器可以解释的外部调试器也是如此。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT OnCanNotJITScriptErrorDebug(  
   IActiveScriptErrorDebug*  pErrorDebug  
   BOOL *pfCallOnScriptErrorWhenContinuing  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pErrorDebug`  
 中发生的运行时错误。  
  
 `pfCallOnScriptErrorWhenContinuingt`  
 弄如果用户决定在不调试的情况下继续操作，是否调用[IActiveScriptSiteDebug：： OnScriptErrorDebug](../../winscript/reference/iactivescriptsitedebug-onscripterrordebug.md) 。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 还应实现此接口以获取通知。  
  
## <a name="see-also"></a>请参阅  
 [IActiveScriptSiteDebugEx 接口](../../winscript/reference/iactivescriptsitedebugex-interface.md)