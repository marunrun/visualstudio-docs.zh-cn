---
title: IActiveScriptParse32 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: c39c14aa-beb7-4eca-8b8c-2181da1c2e3e
caps.latest.revision: 6
author: mikejo5000
ms.author: mikejo
ms.openlocfilehash: 568feacfe75de22a330c892a44fa4f4f6fd0e3b8
ms.sourcegitcommit: 9a9c61ca115c22d33bb902153eb0853789c7be4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85835311"
---
# <a name="iactivescriptparse32"></a>IActiveScriptParse32
如果 Windows 脚本引擎允许将原始文本代码 scriptlet 添加到脚本中，或允许在运行时计算表达式文本，则它实现 `IActiveScriptParse32` 接口。 对于没有独立创作环境的解释型脚本语言（如 VBScript），这提供了一种替代机制（而不是 `IPersist*` ）以将脚本代码添加到脚本引擎中，并将脚本片段附加到各种对象事件。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
  
|方法|说明|  
|------------|-----------------|  
|[IActiveScriptParse32::AddScriptlet](../../winscript/reference/iactivescriptparse32-addscriptlet.md)|向脚本中添加代码 scriptlet。|  
|[IActiveScriptParse32::InitNew](../../winscript/reference/iactivescriptparse32-initnew.md)|初始化脚本引擎。|  
|[IActiveScriptParse32::ParseScriptText](../../winscript/reference/iactivescriptparse32-parsescripttext.md)|分析给定的代码 scriptlet，将声明添加到命名空间中，并根据需要对代码进行评估。|