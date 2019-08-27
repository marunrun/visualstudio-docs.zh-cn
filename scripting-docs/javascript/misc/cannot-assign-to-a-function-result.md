---
title: 无法给函数结果赋值 |Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: reference
f1_keywords:
- VS.WebClient.Help.SCRIPT5003
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: ee8ffb3a-1451-4cb3-99bf-5e9cf8b77d79
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 226056f139e45f432d757aff8f8774b013742de3
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62946597"
---
# <a name="cannot-assign-to-a-function-result"></a>无法给函数结果赋值
你试图将值分配给函数结果。 可以将函数的结果赋给一个变量，但不能用作变量。 如果你想要将新值分配给该函数本身，则省略括号 （函数调用运算符）。 下面的示例演示的情况下，会生成此错误。  
  
```js
myFunction() = 42;  // Attempting to assign the value 42 to the result of the function call.  
```  
  
### <a name="to-correct-this-error"></a>更正此错误  
  
- 不使用函数调用结果的值用作可以*将分配给*。 您可以将函数调用的结果的分配*给一个变量*尽管。  
  
    ```JavaScript  
    myVar = myFunction(42);  
    ```  
  
- 或者，可以将该函数本身 （而不是其返回值） 分配给一个变量。  
  
    ```JavaScript  
    myFunction = new Function("return 42;");  
    ```  
  
## <a name="see-also"></a>请参阅  
 [函数对象](../../javascript/reference/function-object-javascript.md)   
 [编写 JavaScript 代码](../../javascript/writing-javascript-code.md)   
 [函数](../../javascript/functions-javascript.md)