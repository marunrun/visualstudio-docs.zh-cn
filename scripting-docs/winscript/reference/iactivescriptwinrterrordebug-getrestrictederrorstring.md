---
title: IActiveScriptWinRTErrorDebug::GetRestrictedErrorString |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IActiveScriptWinRTErrorDebug::GetRestrictedErrorString
ms.assetid: d901e049-fb1b-4101-a04a-1395d657f1cf
caps.latest.revision: 5
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 154909183e044267053a04ebc489de6dddd55788
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63425865"
---
# <a name="iactivescriptwinrterrordebuggetrestrictederrorstring"></a>IActiveScriptWinRTErrorDebug::GetRestrictedErrorString
如果可用，则返回 Windows 运行时限制错误字符串。  
  
> [!IMPORTANT]
> [IActiveScriptWinRTErrorDebug 接口](../../winscript/reference/iactivescriptwinrterrordebug-interface.md)是实现由 PDM v11.0 和更高版本。 在 activdbg100.h 中发现。  
  
## <a name="syntax"></a>语法  
  
```cpp  
HRESULT GetRestrictedErrorString([out] BSTR * errorString);   
```  
  
#### <a name="parameters"></a>参数  
 `errorString`  
 [out]受限制的错误字符串。  
  
## <a name="see-also"></a>请参阅  
 [IActiveScriptWinRTErrorDebug 接口](../../winscript/reference/iactivescriptwinrterrordebug-interface.md)