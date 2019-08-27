---
title: IActiveScriptErrorDebug 接口 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IActiveScriptErrorDebug interface
ms.assetid: e5d50427-c033-4138-ac6e-3b2dfb3b750a
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 936770859d3bdfe81c84245d32ae63346b142a01
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63009527"
---
# <a name="iactivescripterrordebug-interface"></a>IActiveScriptErrorDebug 接口
提供文档上下文信息的编译时错误和运行时异常。 `IActiveScriptError::QueryInterface`方法支持`IActiveScriptErrorDebug`接口。  
  
 除了继承的方法之外`IActiveScriptError`，则`IActiveScriptErrorDebug`接口公开以下方法。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
  
|方法|描述|  
|------------|-----------------|  
|[IActiveScriptErrorDebug::GetDocumentContext](../../winscript/reference/iactivescripterrordebug-getdocumentcontext.md)|此错误提供的文档上下文。|  
|[IActiveScriptErrorDebug::GetStackFrame](../../winscript/reference/iactivescripterrordebug-getstackframe.md)|提供了适用于运行时错误的堆栈帧。|