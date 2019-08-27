---
title: 应有 catch |Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: reference
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
ms.openlocfilehash: 941d49a530b14e2af64ddcb599dd775feb347de0
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62935394"
---
# <a name="expected-catch"></a>应有“catch”
使用异常处理**尝试**阻止，但没有编写关联**捕获**语句。 异常处理机制要求可能会失败，以及在发生异常时，不应执行的代码的代码将被封装在**尝试**块。 内引发的异常**尝试**阻止使用**引发**语句，并捕获外部**重**块包含一个或多个**捕获**语句。  
  
### <a name="to-correct-this-error"></a>更正此错误  
  
- 添加关联**捕获**块。  
  
- 请尝试使用**最后**而不是阻止**捕获**块。  
  
## <a name="see-also"></a>请参阅  
 [try...catch...最后语句](../../javascript/reference/try-dot-dot-dot-catch-dot-dot-dot-finally-statement-javascript.md)   
 [错误对象](../../javascript/reference/error-object-javascript.md)