---
title: IDebugExpressionContext 接口 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugExpressionContext Interface
apilocation:
- jscript.dll
helpviewer_keywords:
- IDebugExpressionContext interface
ms.assetid: 52af82e8-0dec-49e2-a7f3-d00f66ca1401
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 5920d644922b15f193ee396ea0c6bddb8a574698
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62996873"
---
# <a name="idebugexpressioncontext-interface"></a>IDebugExpressionContext 接口
表示在其中计算表达式的上下文。 堆栈帧对象实现此接口。  
  
 除了继承的方法之外`IUnknown`，则`IDebugExpressionContext`接口公开以下方法。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
  
|方法|描述|  
|------------|-----------------|  
|[IDebugExpressionContext::ParseLanguageText](../../winscript/reference/idebugexpressioncontext-parselanguagetext.md)|创建指定的文本的调试表达式。|  
|[IDebugExpressionContext::GetLanguageInfo](../../winscript/reference/idebugexpressioncontext-getlanguageinfo.md)|返回拥有此上下文中的语言名称和 GUID。|