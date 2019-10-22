---
title: IActiveScriptWinRTErrorDebug：： GetRestrictedErrorReference |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IActiveScriptWinRTErrorDebug::GetRestrictedErrorReference
ms.assetid: fcf60971-9518-4b24-a3a6-1e2e30a02cea
caps.latest.revision: 5
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 4665071fe26ed3dadbaadbcbaa79217562d311c6
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72577912"
---
# <a name="iactivescriptwinrterrordebuggetrestrictederrorreference"></a>IActiveScriptWinRTErrorDebug::GetRestrictedErrorReference
如果有，则返回 Windows 运行时受限引用错误。  
  
> [!IMPORTANT]
> [IActiveScriptWinRTErrorDebug 接口](../../winscript/reference/iactivescriptwinrterrordebug-interface.md)由 PDM 11.0 和更高版本实现。 在 activdbg100.h 中发现。  
  
## <a name="syntax"></a>语法  
  
```cpp  
HRESULT GetRestrictedErrorReference([out] BSTR * referenceString);  
```  
  
#### <a name="parameters"></a>参数  
 `referenceString`  
 弄引用错误字符串。  
  
## <a name="see-also"></a>请参阅  
 [IActiveScriptWinRTErrorDebug 接口](../../winscript/reference/iactivescriptwinrterrordebug-interface.md)