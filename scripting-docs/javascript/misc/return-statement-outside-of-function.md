---
title: 函数外部的 "return" 语句 |Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: error-reference
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
ms.openlocfilehash: 32eadcf5ae88dbe64c8ccdb3effbb85bc79f9b32
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "85816730"
---
# <a name="return-statement-outside-of-function"></a>“return”语句在函数之外
在 `return` 代码的全局范围内使用了语句。 `return`语句应仅出现在函数体中。  
  
 使用运算符调用函数 `()` 是一个表达式。 所有表达式都具有值; `return` 语句用于指定函数返回的值。 一般形式为：  
  
```js
  
return [ expression ];  
```  
  
 `return`执行语句时，将计算*表达式*并将其作为函数的值返回。 如果没有表达式，则返回 **undefined** 。  
  
 当 `return` 执行语句时，即使函数体中仍剩余其他语句，函数的执行也会停止。 此规则的例外情况是，如果 **return** 语句发生在 **try** 块中，并且存在相应的 **finally** 块，则 **finally** 块中的代码将在函数返回之前执行。  
  
 如果函数因到达函数体的末尾而不执行语句而返回，则 `return` 返回的值是 **未定义** 的值 (这意味着函数结果不能用作较大表达式) 的一部分。  
  
### <a name="to-correct-this-error"></a>更正此错误  
  
- `return`从代码主体 (全局范围) 中删除语句。  
  
## <a name="see-also"></a>另请参阅  
 [return 语句](../../javascript/reference/return-statement-javascript.md)   
 [Function 对象](../../javascript/reference/function-object-javascript.md)   
 [caller 属性 (Function)](../../javascript/reference/caller-property-function-javascript.md)