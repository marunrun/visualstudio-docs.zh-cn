---
title: IActiveScriptParseProcedureOld 接口 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptParseProcedureOld
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScriptParseProcedureOld interface
ms.assetid: d94b391e-4c24-46da-a01f-2c134ca4f041
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 4558a0cab2aea9b56db2759bb80b1287cd33ce87
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72571423"
---
# <a name="iactivescriptparseprocedureold-interface"></a>IActiveScriptParseProcedureOld 接口
允许将过程的源代码文本添加到脚本。 对于没有独立创作环境（如 VBScript）的解释脚本语言，这提供了一种替代机制（`IActiveScriptParse` 或 `IPersist*`）将脚本过程添加到命名空间。  
  
> [!NOTE]
> 此接口已弃用，以支持 `IActiveScriptParseProcedure` 接口。  
  
## <a name="methods"></a>方法  
 除了从 `IUnknown` 继承的方法之外，`IActiveScriptParseProcedureOld` 接口还公开以下方法。  
  
|方法|描述|  
|------------|-----------------|  
|[IActiveScriptParseProcedureOld::ParseProcedureText](../../winscript/reference/iactivescriptparseprocedureold-parseproceduretext.md)|分析给定的代码过程，并将过程添加到命名空间。|  
  
## <a name="see-also"></a>请参阅  
 [IActiveScriptParseProcedure](../../winscript/reference/iactivescriptparseprocedure.md)