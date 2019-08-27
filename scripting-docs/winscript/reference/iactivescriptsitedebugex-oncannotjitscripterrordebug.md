---
title: IActiveScriptSiteDebugEx::OnCanNotJITScriptErrorDebug |Microsoft Docs
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
ms.openlocfilehash: 4c643478da37b5a66c22b201ef8f8248df02e4ec
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62992345"
---
# <a name="iactivescriptsitedebugexoncannotjitscripterrordebug"></a>IActiveScriptSiteDebugEx::OnCanNotJITScriptErrorDebug
通知主机有关脚本运行时错误进程调试管理器时未找到恰时脚本调试器。  
  
 若要在你的主机中实现一个调试器，您应处理[IActiveScriptSiteDebug::OnScriptErrorDebug](../../winscript/reference/iactivescriptsitedebug-onscripterrordebug.md)。 根据用户操作，主机可以将附加调试器，并返回，或返回 OnScriptErrorDebug 中调试器的起始`pfEnterDebugger`参数。 此外应实现此接口，用于获取有关运行时错误通知，即使有可由进程调试管理器理解没有外部调试器。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT OnCanNotJITScriptErrorDebug(  
   IActiveScriptErrorDebug*  pErrorDebug  
   BOOL *pfCallOnScriptErrorWhenContinuing  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pErrorDebug`  
 [in]发生的运行时错误。  
  
 `pfCallOnScriptErrorWhenContinuingt`  
 [out]是否需要调用[IActiveScriptSiteDebug::OnScriptErrorDebug](../../winscript/reference/iactivescriptsitedebug-onscripterrordebug.md)如果用户决定继续而不进行调试。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 此外应实现此接口可收到通知。  
  
## <a name="see-also"></a>请参阅  
 [IActiveScriptSiteDebugEx 接口](../../winscript/reference/iactivescriptsitedebugex-interface.md)