---
title: IActiveScriptSiteDebug 接口 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IActiveScriptSiteDebug interface
ms.assetid: 2557ee09-688b-4c03-a821-180c24dfa0e6
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 3cd8043648586ed3c614cbb137e51d992d7ae29b
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62992467"
---
# <a name="iactivescriptsitedebug-interface"></a>IActiveScriptSiteDebug 接口
智能主机实现`IActiveScriptSiteDebug`界面，用于执行文档管理和参与调试。 `IActiveScriptSite`对象通常提供的实现`IActiveScriptSiteDebug`接口。 如果此操作后，调用`IActiveScriptSite::QueryInterface`方法来获取`IActiveScriptSiteDebug`接口。  
  
 除了继承的方法之外`IUnknown`，则`IActiveScriptSiteDebug`接口公开以下方法。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
  
|方法|描述|  
|------------|-----------------|  
|[IActiveScriptSiteDebug::GetDocumentContextFromPosition](../../winscript/reference/iactivescriptsitedebug-getdocumentcontextfromposition.md)|语言引擎用于委派`IDebugCodeContext::GetSourceContext`。|  
|[IActiveScriptSiteDebug::GetApplication](../../winscript/reference/iactivescriptsitedebug-getapplication.md)|返回与此脚本站点关联的调试应用程序对象。|  
|[IActiveScriptSiteDebug::GetRootApplicationNode](../../winscript/reference/iactivescriptsitedebug-getrootapplicationnode.md)|获取应在哪个脚本添加文档的应用程序节点。|  
|[IActiveScriptSiteDebug::OnScriptErrorDebug](../../winscript/reference/iactivescriptsitedebug-onscripterrordebug.md)|允许智能主机以确定如何处理运行时错误。|