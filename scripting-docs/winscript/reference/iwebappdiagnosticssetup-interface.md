---
title: IWebAppDiagnosticsSetup 接口 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IWebAppDiagnosticsSetup Interface
ms.assetid: ec7359f2-633e-4d59-b64b-9cab0134dfd0
caps.latest.revision: 4
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 1e9bb3905da6227b978bc27b96493500f8d6d2ff
ms.sourcegitcommit: dcbb876a5dd598f2538e62e1eabd4dc98595b53a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2019
ms.locfileid: "72984537"
---
# <a name="iwebappdiagnosticssetup-interface"></a>IWebAppDiagnosticsSetup 接口
PDM 调试应用程序实现此接口，以在正在调试的进程中创建 COM 对象，并启用 web 诊断。 如果 PDM 调试应用程序对象实现[IObjectWithSite](/windows/win32/api/ocidl/nn-ocidl-iobjectwithsite)，则 Internet Explorer 会在其创建后调用[SetSite](/windows/win32/api/ocidl/nf-ocidl-iobjectwithsite-setsite) ，并传入对[IWebBrowser2](/previous-versions/windows/internet-explorer/ie-developer/platform-apis/aa752127(v=vs.85))的引用。 WWA 应用程序调用[SetSite](/windows/win32/api/ocidl/nf-ocidl-iobjectwithsite-setsite)并传入 WWA 接口 IWebApplicationHost。 如果使用非 NULL 值调用[SetSite](/windows/win32/api/ocidl/nf-ocidl-iobjectwithsite-setsite) ，则[IWebAppDiagnosticsSetup：:D iagnosticssupported](../../winscript/reference/iwebappdiagnosticssetup-diagnosticssupported.md)返回 true。 如果不是，则返回 false，对[IWebAppDiagnosticsSetup：： CreateObjectWithSiteAtWebApp](../../winscript/reference/iwebappdiagnosticssetup-createobjectwithsiteatwebapp.md)的调用将失败。  
  
> [!IMPORTANT]
> `IWebAppDiagnosticsSetup` 由 PDM 11.0 和更高版本实现。 在 activdbg100.h 中发现。  
  
## <a name="methods"></a>方法  
 此接口公开以下方法。  
  
|方法|描述|  
|------------|-----------------|  
|[IWebAppDiagnosticsSetup::CreateObjectWithSiteAtWebApp](../../winscript/reference/iwebappdiagnosticssetup-createobjectwithsiteatwebapp.md)|获取由指定的筛选器隐藏的文本文档。|  
|[IWebAppDiagnosticsSetup::DiagnosticsSupported](../../winscript/reference/iwebappdiagnosticssetup-diagnosticssupported.md)|确定指定的文档是否属于此节点的一个子节点。|