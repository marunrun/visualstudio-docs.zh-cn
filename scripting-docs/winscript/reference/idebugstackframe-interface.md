---
title: IDebugStackFrame 接口 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IDebugStackFrame interface
ms.assetid: e95c1b4f-17c1-490c-a56b-c25fa45d4822
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: d8f645d6460ff15734348267b5138b1b6edea071
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63005873"
---
# <a name="idebugstackframe-interface"></a>IDebugStackFrame 接口
表示线程堆栈上的逻辑堆栈帧。 调用`IDebugStackFrame::QueryInterface`方法来获取`IDebugExpressionContext`接口，这允许表达式计算和监视窗口。  
  
 除了继承的方法之外`IUnknown`，则`IDebugStackFrame`接口公开以下方法。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
  
|方法|描述|  
|------------|-----------------|  
|[IDebugStackFrame::GetCodeContext](../../winscript/reference/idebugstackframe-getcodecontext.md)|返回与此堆栈帧关联的当前代码上下文。|  
|[IDebugStackFrame::GetDescriptionString](../../winscript/reference/idebugstackframe-getdescriptionstring.md)|返回的堆栈帧的短期或长文本描述。|  
|[IDebugStackFrame::GetLanguageString](../../winscript/reference/idebugstackframe-getlanguagestring.md)|返回语言的短或长文本描述。|  
|[IDebugStackFrame::GetThread](../../winscript/reference/idebugstackframe-getthread.md)|返回与此堆栈帧关联的线程。|  
|[IDebugStackFrame::GetDebugProperty](../../winscript/reference/idebugstackframe-getdebugproperty.md)|返回当前帧的属性浏览器。|