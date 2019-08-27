---
title: 缺少函数 |Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: reference
f1_keywords:
- VS.WebClient.Help.SCRIPT5002
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: f62ade94-9f6f-4832-9b9b-49a06a385bbe
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 4442143b2766ed3608a852d0f811a6b943fd19df
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63007101"
---
# <a name="function-expected"></a>缺少函数
要么你尝试调用之一**函数原型**不是对象上的方法`Function`对象，或者您的函数调用上下文中使用一个对象。 例如，下面的代码生成此错误，因为**示例**不是函数。  
  
```JavaScript  
var example = new Object();  // Create a new object called "example".  
var x = example();           // Try and call example as if it were a function.  
```  
  
### <a name="to-correct-this-error"></a>更正此错误  
  
- 只能调用**函数原型**上的方法`Function`对象。  
  
- 请确保使用的函数调用运算符`()`函数只能调用。  
  
## <a name="see-also"></a>请参阅  
 [函数对象](../../javascript/reference/function-object-javascript.md)   
 [prototype 属性 (Object)](../../javascript/reference/prototype-property-object-javascript.md)