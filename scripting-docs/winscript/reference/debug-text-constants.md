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
ms.openlocfilehash: 2342555c4ee92b403aa01cc0ca15bb805f2b002e
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62955245"
---
# <a name="debugtext-constants"></a>DEBUG_TEXT 常量
过程中使用[IDebugExpressionContext::ParseLanguageText](../../winscript/reference/idebugexpressioncontext-parselanguagetext.md)。  
  
## <a name="syntax"></a>语法  
  
```cpp
typedef DWORD DEBUG_TEXT;  
```  
  
## <a name="constants"></a>常量  
  
|返回的常量|“值”|描述|  
|--------------|-----------|-----------------|  
|DWORD DEBUG_TEXT_ISEXPRESSION|0x00000001|指示该文本是而不是语句表达式。 此标志可能会影响在其中的一些语言分析文本的方式。|  
|DEBUG_TEXT_RETURNVALUE|0x00000002|如果返回值不可用，调用方将使用它。|  
|DEBUG_TEXT_NOSIDEEFFECTS|0x00000004|不允许副作用。 如果设置此标志，该表达式的计算应更改任何运行时状态。|  
|DEBUG_TEXT_ALLOWBREAKPOINTS|0x00000008|允许文本求值时的断点。 如果未设置此标志，断点将被忽略的文本求值时。|  
|DEBUG_TEXT_ALLOWERRORREPORT|0x00000010|允许文本求值时的错误报告。 如果未设置此标志，然后将不报告错误到该主机在计算过程。|  
|DEBUG_TEXT_EVALUATETOCODECONTEXT|0x00000020|指示该表达式将计算结果为代码上下文，而不是运行该表达式本身。|  
  
## <a name="see-also"></a>请参阅  
 [活动脚本调试器常量、枚举和结构](../../winscript/reference/active-script-debugger-constants-enumerations-and-structures.md)