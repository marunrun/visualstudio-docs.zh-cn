---
title: IEnumDebugExpressionContexts Interface | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IEnumDebugExpressionContexts interface
ms.assetid: 1c11f9ff-c5a6-48b8-a287-0d782513ba55
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 0c257fe12f27bb5e6ffd5835986d0c7cac6193a8
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62807369"
---
# <a name="ienumdebugexpressioncontexts-interface"></a>IEnumDebugExpressionContexts 接口
枚举 `IDebugExpressionContexts` 对象的集合。  
  
 除了继承的方法之外`IUnknown`，则`IEnumDebugExpressionContexts`接口公开以下方法。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
  
|方法|描述|  
|------------|-----------------|  
|[IEnumDebugExpressionContexts::Next](../../winscript/reference/ienumdebugexpressioncontexts-next.md)|检索指定的数目的枚举序列中的段。|  
|[IEnumDebugExpressionContexts::Skip](../../winscript/reference/ienumdebugexpressioncontexts-skip.md)|将跳过枚举序列中的指定的段数。|  
|[IEnumDebugExpressionContexts::Reset](../../winscript/reference/ienumdebugexpressioncontexts-reset.md)|将枚举序列重置到开头。|  
|[IEnumDebugExpressionContexts::Clone](../../winscript/reference/ienumdebugexpressioncontexts-clone.md)|创建一个包含与当前枚举数相同的状态的枚举器。|