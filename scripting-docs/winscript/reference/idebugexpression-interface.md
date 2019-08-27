---
title: IDebugExpression 接口 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IDebugExpression interface
ms.assetid: 36c00ffb-7160-4c30-a2c9-c9d70c8213cd
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 1757317e9ab148b508bfed95107b5c3b3369b598
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63430024"
---
# <a name="idebugexpression-interface"></a>IDebugExpression 接口
表示异步计算的表达式。 脚本引擎通常情况下实现此接口。 调试器 IDE 通常使用此接口来启用立即执行窗口或监视窗口。  
  
> [!NOTE]
> `IDebugExpression`接口是只能从堆栈帧。  
  
 除了继承的方法之外`IUnknown`，则`IDebugExpression`接口公开以下方法。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
  
|方法|描述|  
|------------|-----------------|  
|[IDebugExpression::Start](../../winscript/reference/idebugexpression-start.md)|开始表达式的计算。|  
|[IDebugExpression::Abort](../../winscript/reference/idebugexpression-abort.md)|中止该表达式。|  
|[IDebugExpression::QueryIsComplete](../../winscript/reference/idebugexpression-queryiscomplete.md)|确定操作已完成。|  
|[IDebugExpression::GetResultAsString](../../winscript/reference/idebugexpression-getresultasstring.md)|返回一个字符串和操作的返回值为表达式计算的结果。|  
|[IDebugExpression::GetResultAsDebugProperty](../../winscript/reference/idebugexpression-getresultasdebugproperty.md)|返回表达式计算作为一种调试属性和操作的返回值的结果。|