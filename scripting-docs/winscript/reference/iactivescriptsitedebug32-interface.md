---
title: IActiveScriptSiteDebug32 接口 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 03f42217-303d-46e7-9792-61a5ab95252c
caps.latest.revision: 5
author: mikejo5000
ms.author: mikejo
ms.openlocfilehash: 2a55161f76fcd98b52ddb769c640aca0e903239b
ms.sourcegitcommit: 9a9c61ca115c22d33bb902153eb0853789c7be4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85835259"
---
# <a name="iactivescriptsitedebug32-interface"></a>IActiveScriptSiteDebug32 接口
智能主机实现 `IActiveScriptSiteDebug32` 接口以执行文档管理并参与调试。 `IActiveScriptSite`对象通常提供接口的实现 `IActiveScriptSiteDebug32` 。 如果已完成此操作，请调用 `IActiveScriptSite::QueryInterface` 方法来获取 `IActiveScriptSiteDebug32` 接口。  
  
 除了从继承的方法之外 `IUnknown` ，接口还 `IActiveScriptSiteDebug32` 公开以下方法。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
  
|方法|说明|  
|------------|-----------------|  
|[IActiveScriptSiteDebug32::GetApplication](../../winscript/reference/iactivescriptsitedebug32-getapplication.md)|返回与此脚本网站关联的调试应用程序对象。|  
|[IActiveScriptSiteDebug32::GetDocumentContextFromPosition](../../winscript/reference/iactivescriptsitedebug32-getdocumentcontextfromposition.md)|供语言引擎用来委托 `IDebugCodeContext::GetSourceContext` 。|