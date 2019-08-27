---
title: IWebAppDiagnosticsSetup::CreateObjectWithSiteAtWebApp | Microsoft Docs
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
ms.openlocfilehash: 42f92cfe9245a5e3a6342c31fc996ae2db50ef70
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63443698"
---
# <a name="iwebappdiagnosticssetupcreateobjectwithsiteatwebapp"></a>IWebAppDiagnosticsSetup::CreateObjectWithSiteAtWebApp
此方法共同创建的类中的传递其 ID`rclsid`使用`dwClsContext`。 这是类似的方式[IRemoteDebugApplication::CreateInstanceAtApplication](../../winscript/reference/iremotedebugapplication-createinstanceatapplication.md)的工作原理，不同之处在于的情况下`CreateObjectWithSiteAtWebApp`web 应用程序的 UI 线程上以异步方式创建对象。 指定的类 ID 的对象应实现[IWebAppDiagnosticsObjectInitialization 接口](../../winscript/reference/iwebappdiagnosticsobjectinitialization-interface.md)。 创建对象后， [IWebAppDiagnosticsObjectInitialization::Initialize](../../winscript/reference/iwebappdiagnosticsobjectinitialization-initialize.md) PDM 调试应用程序的引用调用并`hPassToObject`参数的`CreateObjectWithSiteAtWebApp`。 可以使用此方法以传递到应用程序的句柄到复制使用匿名管道[DuplicateHandle](http://go.microsoft.com/fwlink/?LinkId=232450)。  
  
> [!IMPORTANT]
> [IWebAppDiagnosticsSetup 接口](../../winscript/reference/iwebappdiagnosticssetup-interface.md)是实现由 PDM v11.0 和更高版本。 在 activdbg100.h 中发现。  
  
## <a name="syntax"></a>语法  
  
```cpp  
HRESULT CreateObjectWithSiteAtWebApp(        [in] REFCLSID rclsid,         [in] DWORD dwClsContext,         [in] REFIID riid,         [in] DWORD_PTR hPassToObject        );  
```  
  
#### <a name="parameters"></a>参数  
 `rclsid`  
 若要创建类的类 ID。  
  
 `dwClsContext`  
 将在其中运行代码的上下文。 在大多数情况下是 CLSCTX_INPROC_SERVER。  
  
 `riid`  
 未使用。  
  
 `hPassToObject`  
 一个值，将传递给该对象在 UI 线程上创建后如果对象实现[IWebAppDiagnosticsObjectInitialization 接口](../../winscript/reference/iwebappdiagnosticsobjectinitialization-interface.md)。