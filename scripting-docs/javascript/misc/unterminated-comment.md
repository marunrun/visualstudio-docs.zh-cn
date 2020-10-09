---
title: 未终止的注释 |Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: error-reference
f1_keywords:
- VS.WebClient.Help.SCRIPT1016
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: d4286315-814b-4966-b4c4-1ee19d796eff
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 8453b05d2d09537f381bd2947dccb6b0a19a6263
ms.sourcegitcommit: e38419bb842d587fd9e37c24b6cf3fc5c2e74817
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/09/2020
ms.locfileid: "91861840"
---
# <a name="unterminated-comment"></a>未终止的注释
您开始了一个多行注释块，但未正确终止它。 多行注释以 "/*" 组合开头，以反向 " \* /" 组合结束。 以下是一个示例：  
  
```JavaScript  
/* This is a comment  
This is another part of the same comment.*/  
```  
  
### <a name="to-correct-this-error"></a>更正此错误  
  
- 请确保用 "*/" 终止多行注释。  
  
## <a name="see-also"></a>请参阅  
 [Comment 语句](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Lexical_grammar)