---
title: 无效的替换器参数 |Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: reference
f1_keywords:
- VS.WebClient.Help.SCRIPT5035
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: 4727186f-facd-4aa6-9447-bbefbae83f07
caps.latest.revision: 12
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 9ba76a2121dfb3853e38bacbdf49c985103c2a35
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72573811"
---
# <a name="invalid-replacer-argument"></a>无效的替换器参数
尝试使用无效的自变量调用 `JSON.stringify`。 `replacer` 参数必须是函数或数组。  
  
### <a name="to-correct-this-error"></a>更正此错误  
  
- 将 `replacer` 参数更改为函数或数组。  
  
## <a name="example"></a>示例  
 此示例中的代码导致运行时错误，因为 `memberfilter` 是对象而不是函数或数组。  
  
```JavaScript  
var contact = new Object();  
contact.firstname = "Jesper";  
contact.surname = "Aaberg";  
contact.phone = ["555-0100", "555-0120"];  
  
var memberfilter = new Object();  
  
// This line will cause a runtime error.  
var jsontext = JSON.stringify(contact, memberfilter, "\t");  
```  
  
## <a name="see-also"></a>另请参阅  
 [JSON 对象](../../javascript/reference/json-object-javascript.md)   
 [JSON. Parse 函数](../../javascript/reference/json-parse-function-javascript.md)   
 [JavaScript 运行时错误](../../javascript/reference/javascript-run-time-errors.md)