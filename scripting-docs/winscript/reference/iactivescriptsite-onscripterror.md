---
title: IActiveScriptSite：： OnScriptError |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptSite.OnScriptError
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScriptSite_OnScriptError
ms.assetid: 5c9c85cc-21ad-4232-be83-a24cc7570108
caps.latest.revision: 7
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 9f0078b53515a881d7f2ac1475cf5565fa22a025
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72570268"
---
# <a name="iactivescriptsiteonscripterror"></a>IActiveScriptSite::OnScriptError
通知宿主在引擎运行脚本时出现执行错误。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT OnScriptError(  
    IActiveScriptError *pase  // address of error interface  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pase`  
 中错误对象的[IActiveScriptError](../../winscript/reference/iactivescripterror.md)接口的地址。 主机可以使用此接口来获取有关执行错误的信息。  
  
## <a name="return-value"></a>返回值  
 如果错误已正确处理，则返回 `S_OK`; 否则返回 OLE 定义的错误代码。  
  
## <a name="see-also"></a>请参阅  
 [IActiveScriptSite](../../winscript/reference/iactivescriptsite.md)