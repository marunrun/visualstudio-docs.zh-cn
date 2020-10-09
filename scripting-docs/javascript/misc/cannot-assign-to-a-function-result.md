---
title: 不能分配给函数结果 |Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: error-reference
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
ms.openlocfilehash: 6aab43ec6a547982cf670d64c8ad8b752160839f
ms.sourcegitcommit: e38419bb842d587fd9e37c24b6cf3fc5c2e74817
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/09/2020
ms.locfileid: "91862351"
---
# <a name="cannot-assign-to-a-function-result"></a>无法给函数结果赋值
您尝试为函数结果赋值。 可以将函数的结果赋给变量，但不能将其用作变量。 如果要向函数本身分配一个新值，请省略函数调用运算符)  (括号。 下面的示例演示了生成此错误的一种情况。  
  
```js
myFunction() = 42;  // Attempting to assign the value 42 to the result of the function call.  
```  
  
### <a name="to-correct-this-error"></a>更正此错误  
  
- 不要将函数调用结果的值用作可以 *分配给*的内容。 不过，您可以将函数调用的结果分配 *给一个变量* 。  
  
    ```JavaScript  
    myVar = myFunction(42);  
    ```  
  
- 或者，您可以将函数本身 (而不是其返回值) 赋给变量。  
  
    ```JavaScript  
    myFunction = new Function("return 42;");  
    ```  
  
## <a name="see-also"></a>请参阅  
 [Function 对象](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Function)   
 [编写 JavaScript 代码](https://developer.mozilla.org/docs/Learn/Getting_started_with_the_web/JavaScript_basics)   
 [函数](https://developer.mozilla.org/docs/Learn/JavaScript/Building_blocks/Functions)