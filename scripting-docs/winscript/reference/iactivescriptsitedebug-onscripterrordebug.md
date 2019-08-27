---
title: IActiveScriptSiteDebug::OnScriptErrorDebug | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptSiteDebug.OnScriptErrorDebug
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScriptSiteDebug::OnScriptErrorDebug
ms.assetid: 87f201da-36eb-49a2-b000-e1e1e8c4cdb7
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 50e8c7baa42d6f2f36dc71b768797dfe2a464bf3
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62992433"
---
# <a name="iactivescriptsitedebugonscripterrordebug"></a>IActiveScriptSiteDebug::OnScriptErrorDebug
允许智能主机以确定如何处理运行时错误。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT OnScriptErrorDebug(  
   IActiveScriptErrorDebug*  pErrorDebug,  
   BOOL*                     pfEnterDebugger,  
   BOOL*                     pfCallOnScriptErrorWhenContinuing  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pErrorDebug`  
 [in]发生的运行时错误  
  
 `pfEnterDebugger`  
 [out]指示是否将错误传递给调试程序执行 JIT 调试标记。  
  
 `pfCallOnScriptErrorWhenContinuing`  
 [out]指示是否将调用`IActiveScriptSite::OnScriptError`当用户决定继续而不进行调试。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括但不限于以下表中的值。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 智能主机可以使用此方法来确定如何处理运行时错误。  
  
## <a name="see-also"></a>请参阅  
 [IActiveScriptSiteDebug 接口](../../winscript/reference/iactivescriptsitedebug-interface.md)