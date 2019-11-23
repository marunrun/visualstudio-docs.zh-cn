---
title: 正则表达式中需要 "]" （JavaScript） |Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: reference
f1_keywords:
- VS.WebClient.Help.SCRIPT5019
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: 1ca2079a-44dd-479f-a1e3-e04a14d0739e
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 9af38a5fa754a811416f1a998b90946345f3e4a2
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72576479"
---
# <a name="expected--in-regular-expression-javascript"></a>正则表达式中应有“]”(JavaScript)
试图为正则表达式匹配创建字符类，但未包含右大括号。 可以通过将各个文本字符组合放在方括号中来将它们组合到字符类中。 字符类与它所包含的任何一个字符匹配。 例如，/[abc]/匹配任何字母 "a"、"b" 或 "c"。  
  
### <a name="to-correct-this-error"></a>更正此错误  
  
- 向正则表达式添加右括号。  
  
    > [!NOTE]
    > 如果要匹配单个方括号，请使用反斜杠 \\[-进行转义，以便 [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)]不将其解释为特殊字符。  
  
## <a name="see-also"></a>另请参阅  
 [正则表达式对象](../../javascript/reference/regular-expression-object-javascript.md)   
 [正则表达式语法（JavaScript）](https://msdn.microsoft.com/library/1400241x)