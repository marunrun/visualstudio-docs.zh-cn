---
title: return 语句在函数外的 |Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: reference
f1_keywords:
- VS.WebClient.Help.SCRIPT1018
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: 03568f9f-5f4f-4a10-a738-9a73f3832b9e
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 01ef96385d5fe3dccf14a7491e67983d39913280
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63006401"
---
# <a name="return-statement-outside-of-function"></a>“return”语句在函数之外
您使用`return`全局作用域中的代码的语句。 `return`语句应仅出现在函数体。  
  
 调用的函数`()`运算符是一个表达式。 所有表达式都具有值;`return`语句用于指定函数返回的值。 常规形式为：  
  
```js
  
return [ expression ];  
```  
  
 当`return`执行语句时，*表达式*是评估并作为函数值返回。 如果没有任何表达式**未定义**返回。  
  
 函数的执行停止时`return`即使还有其他语句仍在函数体中执行语句。 此规则的例外是如果**返回**语句出现在**尝试**块中，且相应**最后**阻止，请在代码**最后**块将执行该函数返回之前。  
  
 如果函数返回，因为无需执行到达函数体的终点`return`语句，返回的值是**未定义**值 （这就意味着函数结果不能用作较大表达式的一部分).  
  
### <a name="to-correct-this-error"></a>更正此错误  
  
- 删除`return`语句从你的代码 （全局范围） 的主要部分。  
  
## <a name="see-also"></a>请参阅  
 [return 语句](../../javascript/reference/return-statement-javascript.md)   
 [函数对象](../../javascript/reference/function-object-javascript.md)   
 [caller 属性 (Function)](../../javascript/reference/caller-property-function-javascript.md)