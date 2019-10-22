---
title: IActiveScriptParse |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IActiveScriptParse interface
ms.assetid: 8c967d70-f582-4f64-9e79-49f40c4dcb7c
caps.latest.revision: 7
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 81f64352c15dce233058d49b70e35da7e2238688
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72561648"
---
# <a name="iactivescriptparse"></a>IActiveScriptParse
如果 Windows 脚本引擎允许将原始文本代码 scriptlet 添加到脚本中，或允许在运行时计算表达式文本，则它实现 `IActiveScriptParse` 接口。 对于没有独立创作环境的解释型脚本语言（如 VBScript），这提供了一种替代机制（而不是 `IPersist*`）以在脚本引擎中获取脚本代码，并将脚本片段附加到各种对象事件.  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
  
|方法|描述|  
|------------|-----------------|  
|[IActiveScriptParse::InitNew](../../winscript/reference/iactivescriptparse-initnew.md)|初始化脚本引擎。|  
|[IActiveScriptParse::AddScriptlet](../../winscript/reference/iactivescriptparse-addscriptlet.md)|向脚本中添加代码 scriptlet。|  
|[IActiveScriptParse::ParseScriptText](../../winscript/reference/iactivescriptparse-parsescripttext.md)|分析给定的代码 scriptlet，将声明添加到命名空间中，并根据需要对代码进行评估。|  
  
## <a name="see-also"></a>请参阅  
 [活动脚本接口](../../winscript/reference/active-script-interfaces.md)