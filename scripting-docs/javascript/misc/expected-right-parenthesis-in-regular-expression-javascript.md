---
title: 正则表达式中缺少 "）" （JavaScript） |Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: error-reference
f1_keywords:
- VS.WebClient.Help.SCRIPT5020
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: 2087ba1d-9783-4d40-b609-e8542f579f7f
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: af32127476c83100c0340021428e3abc572ef2f7
ms.sourcegitcommit: ca777040ca372014b9af5e188d9b60bf56e3e36f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85815633"
---
# <a name="expected--in-regular-expression-javascript"></a>正则表达式中应有“)”(JavaScript)
您尝试创建正则表达式捕获、断言或组，但不包含右括号。 圆括号在正则表达式中有几个用途。 它们主要用于捕获子表达式、指定断言或将模式组合在一起，以便可以按 *、+、？等将项视为单个单元。  
  
### <a name="to-correct-this-error"></a>更正此错误  
  
- 添加最右边的右括号。  
  
    > [!NOTE]
    > 如果要匹配单个括号，请使用反斜杠（）对其进行转义， \\ 以便它不会被解释为特殊字符 [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] 。  
  
## <a name="see-also"></a>请参阅  
 [正则表达式对象](../../javascript/reference/regular-expression-object-javascript.md)   
 [正则表达式语法（JavaScript）](https://msdn.microsoft.com/library/1400241x)