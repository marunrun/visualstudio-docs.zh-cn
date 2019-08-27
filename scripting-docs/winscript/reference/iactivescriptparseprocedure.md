---
title: IActiveScriptParseProcedure | Microsoft Docs
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
ms.openlocfilehash: 5ed07ce5ed48abfb377dde5fc4d5dc128d881b4a
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63009193"
---
# <a name="iactivescriptparseprocedure"></a>IActiveScriptParseProcedure
如果 Windows 脚本引擎允许添加到脚本中的过程的源代码文本，它实现`IActiveScriptParseProcedure`接口。 对于已解释的脚本语言具有任何独立的创作环境，例如 VBScript 中，这提供了其他机制 (而不`IActiveScriptParse`或`IPersist`*) 添加到命名空间的脚本过程。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
  
|||  
|-|-|  
|方法|描述|  
|[IActiveScriptParseProcedure::ParseProcedureText](../../winscript/reference/iactivescriptparseprocedure-parseproceduretext.md)|分析给定的代码过程并将该过程添加到命名空间。|  
  
## <a name="see-also"></a>请参阅  
 [活动脚本接口](../../winscript/reference/active-script-interfaces.md)