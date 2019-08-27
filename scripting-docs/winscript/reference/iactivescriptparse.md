---
title: IActiveScriptParse | Microsoft Docs
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
ms.openlocfilehash: a987b4be3430f2ed8b0562f41b51a94797f96dc4
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63009333"
---
# <a name="iactivescriptparse"></a>IActiveScriptParse
如果 Windows 脚本引擎允许原始文本的代码 scriptlet，若要添加到脚本中，或允许要在运行时计算的表达式文本，它实现`IActiveScriptParse`接口。 对于已解释的脚本语言具有任何独立的创作环境，例如 VBScript 中，这提供了其他机制 (而不`IPersist*`) 若要获取到脚本引擎的脚本代码，并将附加到各种对象的脚本片段事件。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
  
|方法|描述|  
|------------|-----------------|  
|[IActiveScriptParse::InitNew](../../winscript/reference/iactivescriptparse-initnew.md)|初始化脚本引擎。|  
|[IActiveScriptParse::AddScriptlet](../../winscript/reference/iactivescriptparse-addscriptlet.md)|将代码 scriptlet 添加到该脚本。|  
|[IActiveScriptParse::ParseScriptText](../../winscript/reference/iactivescriptparse-parsescripttext.md)|分析给定的代码 scriptlet，添加声明到命名空间和评估与相应的代码。|  
  
## <a name="see-also"></a>请参阅  
 [活动脚本接口](../../winscript/reference/active-script-interfaces.md)