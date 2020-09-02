---
title: 应为 "catch" |Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: error-reference
f1_keywords:
- VS.WebClient.Help.SCRIPT1033
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: f1cd947f-eba2-411e-8e84-8ca86f608643
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 1d9950573e7bbeefe3594d77df2ae41c12f77ed3
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "85816679"
---
# <a name="expected-catch"></a>应有“catch”
你使用了异常处理 **try** 块，但未写入关联的 **catch** 语句。 异常处理机制要求在 **try** 块中包装可能会失败的代码，以及在发生异常时不应执行的代码。 使用**throw**语句从**try**块内部引发异常，并使用一个或多个**catch**语句在**try**块外部捕获异常。  
  
### <a name="to-correct-this-error"></a>更正此错误  
  
- 添加关联的 **catch** 块。  
  
- 尝试使用 **finally** 块，而不是 **catch** 块。  
  
## <a name="see-also"></a>另请参阅  
 [尝试 .。。catch .。。finally 语句](../../javascript/reference/try-dot-dot-dot-catch-dot-dot-dot-finally-statement-javascript.md)   
 [错误对象](../../javascript/reference/error-object-javascript.md)