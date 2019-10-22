---
title: 未终止的注释 |Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: reference
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
ms.openlocfilehash: 22bda5d6baabe8874d7514c137ddbcb3e11eb23b
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72572520"
---
# <a name="unterminated-comment"></a>未终止的注释
您开始了一个多行注释块，但未正确终止它。 多行注释以 "/*" 组合开头，以反向 "\*/" 组合结束。 下面是一个示例：  
  
```JavaScript  
/* This is a comment  
This is another part of the same comment.*/  
```  
  
### <a name="to-correct-this-error"></a>更正此错误  
  
- 请确保用 "*/" 终止多行注释。  
  
## <a name="see-also"></a>请参阅  
 [Comment 语句](../../javascript/reference/comment-statements-javascript.md)