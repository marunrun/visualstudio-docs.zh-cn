---
title: Throw 后面必须跟有相同源行的表达式 |Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: error-reference
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
ms.openlocfilehash: b7bc7ff09152cd0ce7b95c6de73ea98446529c44
ms.sourcegitcommit: ca777040ca372014b9af5e188d9b60bf56e3e36f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85815521"
---
# <a name="throw-must-be-followed-by-an-expression-on-the-same-source-line"></a>同一源行中 throw 之后必须有表达式
你使用了 `throw` 关键字，但没有在同一源行中使用表达式。 `throw`语句由两部分组成： `throw` 关键字，后跟要引发的表达式。 例如：  
  
```JavaScript  
if (denominator == 0) {  
 throw new DivideByZeroException();  
}  
```  
  
 不能向上拆分这两个组件。  
  
### <a name="to-correct-this-error"></a>更正此错误  
  
- 请确保 `throw` 关键字和要引发的表达式出现在同一行上。  
  
## <a name="see-also"></a>请参阅  
 [Error 对象](../../javascript/reference/error-object-javascript.md)   
 [throw 语句](../../javascript/reference/throw-statement-javascript.md)   
 [尝试 .。。catch .。。finally 语句](../../javascript/reference/try-dot-dot-dot-catch-dot-dot-dot-finally-statement-javascript.md)