---
title: IActiveScriptWinRTErrorDebug::GetRestrictedErrorReference |Microsoft Docs
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
ms.openlocfilehash: d4696c66ec331c08f3419d79f0f48feb3bf9d80f
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63432952"
---
# <a name="iactivescriptwinrterrordebuggetrestrictederrorreference"></a>IActiveScriptWinRTErrorDebug::GetRestrictedErrorReference
如果可用，则返回 Windows 运行时限制引用错误。  
  
> [!IMPORTANT]
> [IActiveScriptWinRTErrorDebug 接口](../../winscript/reference/iactivescriptwinrterrordebug-interface.md)是实现由 PDM v11.0 和更高版本。 在 activdbg100.h 中发现。  
  
## <a name="syntax"></a>语法  
  
```cpp  
HRESULT GetRestrictedErrorReference([out] BSTR * referenceString);  
```  
  
#### <a name="parameters"></a>参数  
 `referenceString`  
 [out]引用错误字符串。  
  
## <a name="see-also"></a>请参阅  
 [IActiveScriptWinRTErrorDebug 接口](../../winscript/reference/iactivescriptwinrterrordebug-interface.md)