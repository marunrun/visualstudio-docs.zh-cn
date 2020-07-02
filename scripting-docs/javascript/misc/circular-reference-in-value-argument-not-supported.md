---
title: 不支持在值参数中进行循环引用 |Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: error-reference
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
ms.openlocfilehash: 633ed9c37e8ccde0844205910a8fa2dc12d91414
ms.sourcegitcommit: ca777040ca372014b9af5e188d9b60bf56e3e36f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85817614"
---
# <a name="circular-reference-in-value-argument-not-supported"></a>不支持在值自变量中进行循环引用
尝试使用无效的值进行调用 `JSON.stringify` 。 `value`参数（数组或对象）包含循环引用。  
  
### <a name="to-correct-this-error"></a>更正此错误  
  
- 从参数中删除循环引用。  
  
## <a name="example"></a>示例  
 此示例中的代码将导致运行时错误 `john` ，因为引用了 `mary` 并 `mary` 引用了 `john` 。 若要删除循环引用，请从 `brother` `mary` 对象或 `sister` 对象的属性中删除或取消设置该属性 `john` 。  
  
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
 [JSON。 parse 函数](../../javascript/reference/json-parse-function-javascript.md)   
 [JavaScript 运行时错误](../../javascript/reference/javascript-run-time-errors.md)