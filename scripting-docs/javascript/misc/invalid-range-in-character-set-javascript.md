---
title: 字符范围无效设置 (JavaScript) |Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: reference
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
ms.openlocfilehash: 1cbfa4de401c2a1dc0626f8f00dbb0bd1bf24408
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63007043"
---
# <a name="invalid-range-in-character-set-javascript"></a>字符集范围无效 (JavaScript)
你试图使用无效的字符设置范围创建正则表达式。 字符集的范围必须在单个字符，例如 a 到 z 或 0-9;中的字符，不能包含字符类，如 \w。 范围内的第一个字符还必须在范围内的第二个字符之前。 例如：  
  
```JavaScript  
var good = /[a-z]/;     // A valid character range - a comes before z.  
var notGood = /[z-a]/;  // An invalid character range - z does not come before a.  
```  
  
### <a name="to-correct-this-error"></a>更正此错误  
  
- 使用只将单个字符来撰写应用正则表达式的字符集，并确保它们是正确的顺序。  
  
## <a name="see-also"></a>请参阅  
 [正则表达式对象](../../javascript/reference/regular-expression-object-javascript.md)   
 [正则表达式语法 (JavaScript)](https://msdn.microsoft.com/library/1400241x)