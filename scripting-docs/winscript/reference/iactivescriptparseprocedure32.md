---
title: IActiveScriptParseProcedure32 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 387a856b-f5dc-4371-8620-bd574e046c2c
caps.latest.revision: 5
author: mikejo5000
ms.author: mikejo
ms.openlocfilehash: 71a22f422ff04e56a7aaa7a715641d190ade47bf
ms.sourcegitcommit: d281d2a04a5bc302650eebf369946d8f101e59dd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2020
ms.locfileid: "88144384"
---
# <a name="iactivescriptparseprocedure32"></a>IActiveScriptParseProcedure32
如果 Windows 脚本引擎允许将过程的源代码文本添加到脚本中，则它将实现 `IActiveScriptParseProcedure32` 接口。 对于没有独立创作环境的解释型脚本语言（如 VBScript），这提供了一种替代机制 (`IActiveScriptParse32` 或 `IPersist` * ) ，以将脚本过程添加到命名空间。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
  
|方法|说明|
|-|-|
|[IActiveScriptParseProcedure32::ParseProcedureText](../../winscript/reference/iactivescriptparseprocedure32-parseproceduretext.md)|分析给定的代码过程，并将过程添加到命名空间。|  
  
## <a name="see-also"></a>另请参阅  
 [活动脚本接口](../../winscript/reference/active-script-interfaces.md)