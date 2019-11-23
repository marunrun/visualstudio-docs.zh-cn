---
title: 不支持在值参数中进行循环引用 |Microsoft Docs
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
ms.openlocfilehash: 542fca58778a7b85b3044ce984b6ea049db12509
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72572332"
---
# <a name="circular-reference-in-value-argument-not-supported"></a>不支持在值自变量中进行循环引用
尝试使用无效的值调用 `JSON.stringify` 的。 `value` 参数（数组或对象）包含循环引用。  
  
### <a name="to-correct-this-error"></a>更正此错误  
  
- 从参数中删除循环引用。  
  
## <a name="example"></a>示例  
 此示例中的代码将导致运行时错误，因为 `john` 具有对 `mary` 的引用并且 `mary` 具有对 `john`的引用。 若要删除循环引用，请从 `mary` 对象或 `john` 对象的 `sister` 属性中删除或取消设置属性 `brother`。  
  
```JavaScript  
var john = new Object();  
var mary = new Object();  
john.sister = mary;  
mary.brother = john;  
  
// This line causes a runtime error.  
var error = JSON.stringify(john);  
```  
  
## <a name="see-also"></a>另请参阅  
 [JSON 对象](../../javascript/reference/json-object-javascript.md)   
 [JSON. Parse 函数](../../javascript/reference/json-parse-function-javascript.md)   
 [JavaScript 运行时错误](../../javascript/reference/javascript-run-time-errors.md)