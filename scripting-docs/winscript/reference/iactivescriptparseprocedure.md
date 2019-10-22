---
title: IActiveScriptParseProcedure |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IActiveScriptParseProcedure interface
ms.assetid: 741a35bb-5b92-489e-ba8a-a406b42125fc
caps.latest.revision: 7
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: c20947a125766547565d99c5762c20e23652da1a
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72561666"
---
# <a name="iactivescriptparseprocedure"></a>IActiveScriptParseProcedure
如果 Windows 脚本引擎允许将过程的源代码文本添加到脚本中，则它将实现 `IActiveScriptParseProcedure` 接口。 对于没有独立创作环境的解释脚本语言（如 VBScript），这提供了一种替代机制（`IActiveScriptParse` 或 `IPersist` *），以将脚本过程添加到命名空间。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
  
|||  
|-|-|  
|方法|描述|  
|[IActiveScriptParseProcedure::ParseProcedureText](../../winscript/reference/iactivescriptparseprocedure-parseproceduretext.md)|分析给定的代码过程，并将过程添加到命名空间。|  
  
## <a name="see-also"></a>请参阅  
 [活动脚本接口](../../winscript/reference/active-script-interfaces.md)