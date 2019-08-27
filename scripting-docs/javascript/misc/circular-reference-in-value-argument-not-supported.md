---
title: 在不受支持的值参数中的循环引用 |Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: reference
f1_keywords:
- VS.WebClient.Help.SCRIPT5034
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: 5d06f0fa-86f5-49d1-8d50-af1759990f43
caps.latest.revision: 13
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: a31b56b4b2d568b3bc3fd59f876f5052b9f6faff
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62946363"
---
# <a name="circular-reference-in-value-argument-not-supported"></a>不支持在值自变量中进行循环引用
尝试调用`JSON.stringify`不是有效的值。 `value`参数、 数组或对象，包含循环引用。  
  
### <a name="to-correct-this-error"></a>更正此错误  
  
- 从参数中删除循环引用。  
  
## <a name="example"></a>示例  
 在此示例代码会导致运行时错误，因为`john`引用`mary`并`mary`引用`john`。 若要删除循环引用，或者删除或取消设置该属性`brother`从`mary`对象或`sister`属性从`john`对象。  
  
```JavaScript  
var john = new Object();  
var mary = new Object();  
john.sister = mary;  
mary.brother = john;  
  
// This line causes a runtime error.  
var error = JSON.stringify(john);  
```  
  
## <a name="see-also"></a>请参阅  
 [JSON 对象](../../javascript/reference/json-object-javascript.md)   
 [JSON.parse 函数](../../javascript/reference/json-parse-function-javascript.md)   
 [JavaScript 运行时错误](../../javascript/reference/javascript-run-time-errors.md)