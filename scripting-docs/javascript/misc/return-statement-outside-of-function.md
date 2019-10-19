---
title: 函数外部的 "return" 语句 |Microsoft Docs
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
ms.openlocfilehash: a90af6de8e2c238e3660111b19d13c1eaf628c9e
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72573690"
---
# <a name="return-statement-outside-of-function"></a>“return”语句在函数之外
在代码的全局范围内使用了 `return` 语句。 @No__t_0 语句应仅出现在函数体中。  
  
 使用 `()` 运算符调用函数是一个表达式。 所有表达式都具有值;`return` 语句用于指定函数返回的值。 一般形式为：  
  
```js
  
return [ expression ];  
```  
  
 执行 `return` 语句时，将计算*表达式*并将其作为函数的值返回。 如果没有表达式，则返回**undefined** 。  
  
 当执行 `return` 语句时，即使函数体中仍存在其他语句，函数的执行也会停止。 此规则的例外情况是，如果**return**语句发生在**try**块中，并且存在相应的**finally**块，则**finally**块中的代码将在函数返回之前执行。  
  
 如果函数因到达函数体的末尾而不执行 `return` 语句而返回，则返回的值是**未定义**的值（这意味着函数结果不能用作更大的表达式的一部分）。  
  
### <a name="to-correct-this-error"></a>更正此错误  
  
- 从代码的主体（全局范围）中删除 `return` 语句。  
  
## <a name="see-also"></a>请参阅  
 [return 语句](../../javascript/reference/return-statement-javascript.md)   
 [函数对象](../../javascript/reference/function-object-javascript.md)   
 [caller 属性 (Function)](../../javascript/reference/caller-property-function-javascript.md)