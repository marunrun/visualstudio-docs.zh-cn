---
title: IWebAppDiagnosticsSetup：:D iagnosticsSupported |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IWebAppDiagnosticsSetup::DiagnosticsSupported
ms.assetid: 5bbcd0d0-1460-4cf7-bbb1-f4f4a04f739a
caps.latest.revision: 5
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: dd27e7c8759054fa2d7d67858d8d006fa9c9a152
ms.sourcegitcommit: dcbb876a5dd598f2538e62e1eabd4dc98595b53a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2019
ms.locfileid: "72984575"
---
# <a name="iwebappdiagnosticssetupdiagnosticssupported"></a>IWebAppDiagnosticsSetup::DiagnosticsSupported
确定此应用程序是否支持诊断。 如果已对使用非 NULL 值实现此接口的对象调用[SetSite](/windows/win32/api/ocidl/nf-ocidl-iobjectwithsite-setsite) ，则[DiagnosticsSupported](../../winscript/reference/iwebappdiagnosticssetup-diagnosticssupported.md)将返回 `true`。 否则，它将返回 `false`，对[IWebAppDiagnosticsSetup：： CreateObjectWithSiteAtWebApp](../../winscript/reference/iwebappdiagnosticssetup-createobjectwithsiteatwebapp.md)的调用将失败。  
  
> [!IMPORTANT]
> [IWebAppDiagnosticsSetup 接口](../../winscript/reference/iwebappdiagnosticssetup-interface.md)由 PDM 11.0 和更高版本实现。 在 activdbg100 中找到。  
  
## <a name="syntax"></a>语法  
  
```cpp  
HRESULT DiagnosticsSupported(        [out, retval] VARIANT_BOOL* pRetVal        );  
```  
  
#### <a name="parameters"></a>参数  
 `pRetVal`  
 如果已对使用非 NULL 值实现此接口的对象调用[SetSite](/windows/win32/api/ocidl/nf-ocidl-iobjectwithsite-setsite) ，则[DiagnosticsSupported](../../winscript/reference/iwebappdiagnosticssetup-diagnosticssupported.md)将返回 `true`。 否则，它将返回 `false`，对[IWebAppDiagnosticsSetup：： CreateObjectWithSiteAtWebApp](../../winscript/reference/iwebappdiagnosticssetup-createobjectwithsiteatwebapp.md)的调用将失败。