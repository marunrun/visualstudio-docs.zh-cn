---
title: IWebAppDiagnosticsSetup：： CreateObjectWithSiteAtWebApp |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IWebAppDiagnosticsSetup::CreateObjectWithSiteAtWebApp
ms.assetid: 30975973-acb1-48f4-8266-5e097a57db22
caps.latest.revision: 5
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 253b995c200566868ac9ccc06b259e0a152e1676
ms.sourcegitcommit: dcbb876a5dd598f2538e62e1eabd4dc98595b53a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2019
ms.locfileid: "72984610"
---
# <a name="iwebappdiagnosticssetupcreateobjectwithsiteatwebapp"></a>IWebAppDiagnosticsSetup::CreateObjectWithSiteAtWebApp
此方法共同创建了一个类，其 ID 你使用 `dwClsContext`与 `rclsid` 传入。 这类似于[IRemoteDebugApplication：： CreateInstanceAtApplication](../../winscript/reference/iremotedebugapplication-createinstanceatapplication.md)的工作方式，不同之处在于 `CreateObjectWithSiteAtWebApp` 在 web 应用程序的 UI 线程上以异步方式创建对象。 由类 ID 指定的对象应实现[IWebAppDiagnosticsObjectInitialization 接口](../../winscript/reference/iwebappdiagnosticsobjectinitialization-interface.md)。 创建对象后，将使用对 PDM 调试应用程序的引用和 `CreateObjectWithSiteAtWebApp`的 `hPassToObject` 参数调用[IWebAppDiagnosticsObjectInitialization：： Initialize](../../winscript/reference/iwebappdiagnosticsobjectinitialization-initialize.md) 。 你可以使用此方法将句柄传递到使用[DuplicateHandle](/windows/win32/api/handleapi/nf-handleapi-duplicatehandle)复制的匿名管道的句柄。  
  
> [!IMPORTANT]
> [IWebAppDiagnosticsSetup 接口](../../winscript/reference/iwebappdiagnosticssetup-interface.md)由 PDM 11.0 和更高版本实现。 在 activdbg100.h 中发现。  
  
## <a name="syntax"></a>语法  
  
```cpp  
HRESULT CreateObjectWithSiteAtWebApp(        [in] REFCLSID rclsid,         [in] DWORD dwClsContext,         [in] REFIID riid,         [in] DWORD_PTR hPassToObject        );  
```  
  
#### <a name="parameters"></a>参数  
 `rclsid`  
 要创建的类的类 ID。  
  
 `dwClsContext`  
 要在其中运行代码的上下文。 在大多数情况下，它是 CLSCTX_INPROC_SERVER。  
  
 `riid`  
 未使用。  
  
 `hPassToObject`  
 在 UI 线程上创建对象后，如果对象实现[IWebAppDiagnosticsObjectInitialization 接口](../../winscript/reference/iwebappdiagnosticsobjectinitialization-interface.md)，将传递给该对象的值。