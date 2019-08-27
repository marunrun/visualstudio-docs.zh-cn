---
title: IWebAppDiagnosticsObjectInitialization 接口 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IWebAppDiagnosticsObjectInitialization Interface
ms.assetid: 32847838-01d9-4205-a811-3043d8c7a917
caps.latest.revision: 5
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: a992f8512d4927eeb58d6437ccb830abda688b28
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63443685"
---
# <a name="iwebappdiagnosticsobjectinitialization-interface"></a>IWebAppDiagnosticsObjectInitialization 接口
可以实现的类上实现此接口[IWebAppDiagnosticsSetup::CreateObjectWithSiteAtWebApp](../../winscript/reference/iwebappdiagnosticssetup-createobjectwithsiteatwebapp.md)。 [IWebAppDiagnosticsSetup 接口](../../winscript/reference/iwebappdiagnosticssetup-interface.md)实现的对象由实现[IDebugApplication 接口](../../winscript/reference/idebugapplication-interface.md)。 在大多数情况下此对象是 PDM。  
  
 创建对象后， [IWebAppDiagnosticsObjectInitialization::Initialize](../../winscript/reference/iwebappdiagnosticsobjectinitialization-initialize.md) PDM 调试应用程序的引用调用并`hPassToObject`参数的`CreateObjectWithSiteAtWebApp`。  
  
> [!IMPORTANT]
> `IWebAppDiagnosticsObjectInitialization` 在 activdbg100.h 中找到。  
  
## <a name="methods"></a>方法  
 此接口公开以下方法。  
  
|方法|描述|  
|------------|-----------------|  
|[IWebAppDiagnosticsObjectInitialization::Initialize](../../winscript/reference/iwebappdiagnosticsobjectinitialization-initialize.md)|初始化的对象。|