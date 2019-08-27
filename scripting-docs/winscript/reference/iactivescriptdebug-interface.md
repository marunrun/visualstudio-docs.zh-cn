---
title: IActiveScriptDebug 接口 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IActiveScriptDebug interface
ms.assetid: e3e28cba-ee08-4a52-973a-b74be488c348
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 6341b5c3763d6e4c836b3bdc0539552fcbe7f980
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62955024"
---
# <a name="iactivescriptdebug-interface"></a>IActiveScriptDebug 接口
由脚本引擎实现该支持调试。 通常情况下，实现的对象`IActiveScriptDebug`接口还实现`IActiveScript`接口。 如果是这样，调用`IActiveScript::QueryInterface`方法来获取`IActiveScriptDebug`接口。  
  
 `IActiveScriptDebug`接口提供了有关方式：  
  
- 若要继续使用文档管理的智能主机。  
  
- 进程调试管理器来同步多个脚本引擎的调试。  
  
  除了继承的方法之外`IUnknown`，则`IActiveScriptDebug`接口公开以下方法。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
  
|方法|描述|  
|------------|-----------------|  
|[IActiveScriptDebug::GetScriptTextAttributes](../../winscript/reference/iactivescriptdebug-getscripttextattributes.md)|返回脚本文本的任意块的文本属性。|  
|[IActiveScriptDebug::GetScriptletTextAttributes](../../winscript/reference/iactivescriptdebug-getscriptlettextattributes.md)|返回任意 scriptlet 的文本属性。|  
|[IActiveScriptDebug::EnumCodeContextsOfPosition](../../winscript/reference/iactivescriptdebug-enumcodecontextsofposition.md)|委托给`IDebugDocumentContext::EnumCodeContexts`。|