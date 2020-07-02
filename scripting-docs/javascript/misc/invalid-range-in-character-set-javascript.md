---
title: 字符集范围无效（JavaScript） |Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: error-reference
f1_keywords:
- VS.WebClient.Help.SCRIPT5021
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: 971e9d5a-f88a-47a8-af94-f3c7c4aed5ab
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: a81634a96fb85584c9176db8c72bfc5c3468dc2c
ms.sourcegitcommit: ca777040ca372014b9af5e188d9b60bf56e3e36f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85816873"
---
# <a name="invalid-range-in-character-set-javascript"></a>字符集范围无效 (JavaScript)
尝试使用无效的字符集范围创建正则表达式。 字符集的范围必须仅为单字符，如 a-z 或 0-9;不能将字符类（如 \w）包含在字符集中。 范围中的第一个字符还必须位于范围内的第二个字符之前。 例如：  
  
```JavaScript  
var good = /[a-z]/;     // A valid character range - a comes before z.  
var notGood = /[z-a]/;  // An invalid character range - z does not come before a.  
```  
  
### <a name="to-correct-this-error"></a>更正此错误  
  
- 仅使用单个字符编写正则表达式字符集，并确保它们的顺序正确。  
  
## <a name="see-also"></a>请参阅  
 [正则表达式对象](../../javascript/reference/regular-expression-object-javascript.md)   
 [正则表达式语法（JavaScript）](https://msdn.microsoft.com/library/1400241x)