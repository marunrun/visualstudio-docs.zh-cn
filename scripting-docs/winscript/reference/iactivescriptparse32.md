---
title: IActiveScriptParse32 | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: c39c14aa-beb7-4eca-8b8c-2181da1c2e3e
caps.latest.revision: 6
author: mikejo5000
ms.author: mikejo
ms.openlocfilehash: 9f44239b4e423588b8455b93b87e4084a9c7d1c4
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63009309"
---
# <a name="iactivescriptparse32"></a>IActiveScriptParse32
如果 Windows 脚本引擎允许原始文本的代码 scriptlet，若要添加到脚本中，或允许要在运行时计算的表达式文本，它实现`IActiveScriptParse32`接口。 对于已解释的脚本语言具有任何独立的创作环境，例如 VBScript 中，这提供了其他机制 (而不`IPersist*`) 若要获取到脚本引擎的脚本代码，并将附加到各种对象的脚本片段事件。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
  
|方法|描述|  
|------------|-----------------|  
|[IActiveScriptParse32::AddScriptlet](../../winscript/reference/iactivescriptparse32-addscriptlet.md)|将代码 scriptlet 添加到该脚本。|  
|[IActiveScriptParse32::InitNew](../../winscript/reference/iactivescriptparse32-initnew.md)|初始化脚本引擎。|  
|[IActiveScriptParse32::ParseScriptText](../../winscript/reference/iactivescriptparse32-parsescripttext.md)|分析给定的代码 scriptlet，添加声明到命名空间和评估与相应的代码。|