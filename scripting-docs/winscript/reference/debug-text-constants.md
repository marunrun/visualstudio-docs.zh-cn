---
title: DEBUG_TEXT 常量 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 5dde10c3-7040-46b1-a328-959c6ce5cd9f
caps.latest.revision: 4
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: facbdc1258b3fca72a239d9d5cc41772cf577f13
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72577368"
---
# <a name="debug_text-constants"></a>DEBUG_TEXT 常量
在 IDebugExpressionContext 期间使用[：:P arselanguagetext](../../winscript/reference/idebugexpressioncontext-parselanguagetext.md)。  
  
## <a name="syntax"></a>语法  
  
```cpp
typedef DWORD DEBUG_TEXT;  
```  
  
## <a name="constants"></a>常量  
  
|返回的常量|“值”|描述|  
|--------------|-----------|-----------------|  
|DWORD DEBUG_TEXT_ISEXPRESSION|0x00000001|指示文本是一个表达式，而不是语句。 此标志可能会影响某些语言分析文本的方式。|  
|DEBUG_TEXT_RETURNVALUE|0x00000002|如果返回值可用，则调用方将使用该返回值。|  
|DEBUG_TEXT_NOSIDEEFFECTS|0x00000004|不允许副作用。 如果设置了此标志，则表达式的计算应更改为 "无运行时状态"。|  
|DEBUG_TEXT_ALLOWBREAKPOINTS|0x00000008|允许在文本的计算期间发生断点。 如果未设置此标志，则在对文本进行计算的过程中将忽略断点。|  
|DEBUG_TEXT_ALLOWERRORREPORT|0x00000010|允许在对文本进行计算的过程中报告错误。 如果未设置此标志，则不会在评估过程中将错误报告给主机。|  
|DEBUG_TEXT_EVALUATETOCODECONTEXT|0x00000020|指示将表达式计算为代码上下文而不是运行表达式本身。|  
  
## <a name="see-also"></a>请参阅  
 [活动脚本调试器常量、枚举和结构](../../winscript/reference/active-script-debugger-constants-enumerations-and-structures.md)