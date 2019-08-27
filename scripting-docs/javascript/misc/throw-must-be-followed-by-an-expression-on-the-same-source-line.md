---
title: Throw 表达式之后必须在同一源行上有 |Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: reference
f1_keywords:
- VS.WebClient.Help.SCRIPT1035
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: b03b7747-01a1-40c6-af80-a1dd70bc5781
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 4c8ed951fb30b84f114f8f44a60e94b88f0f1d0f
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63005931"
---
# <a name="throw-must-be-followed-by-an-expression-on-the-same-source-line"></a>同一源行中 throw 之后必须有表达式
您使用`throw`关键字，但不是遵循它使用的表达式在相同的源行上。 一个`throw`语句由两部分组成：`throw`关键字后, 跟要引发的表达式。 例如：  
  
```JavaScript  
if (denominator == 0) {  
 throw new DivideByZeroException();  
}  
```  
  
 您不能拆分这两个组件。  
  
### <a name="to-correct-this-error"></a>更正此错误  
  
- 请确保`throw`关键字和要引发的表达式将显示在同一行上。  
  
## <a name="see-also"></a>请参阅  
 [错误对象](../../javascript/reference/error-object-javascript.md)   
 [Throw 语句](../../javascript/reference/throw-statement-javascript.md)   
 [try...catch...finally 语句](../../javascript/reference/try-dot-dot-dot-catch-dot-dot-dot-finally-statement-javascript.md)