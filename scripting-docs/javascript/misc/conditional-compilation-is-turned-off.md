---
title: 条件编译已关闭 |Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: reference
f1_keywords:
- VS.WebClient.Help.SCRIPT1030
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: 59a030b0-a6c6-47f2-b90e-c0ed204d5116
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 8317121b840d82ab12d4a9e1ca50f6680eb1e21d
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62946571"
---
# <a name="conditional-compilation-is-turned-off"></a>条件编译已关闭
你尝试使用条件编译变量，但不将首次启用条件性编译上。 打开条件编译告知[!INCLUDE[javascript](../../javascript/includes/javascript-md.md)]编译器将解释为条件编译变量，开头的标识符。 为此，可开始使用该语句将条件代码：  
  
```js
/*@cc_on @*/  
```  
  
### <a name="to-correct-this-error"></a>更正此错误  
  
- 将以下语句添加到条件代码的开头：  
  
    ```JavaScript  
    /*@cc_on @*/  
    ```  
  
## <a name="see-also"></a>请参阅  
 [条件编译](../../javascript/advanced/conditional-compilation-javascript.md)   
 [条件编译变量](../../javascript/advanced/conditional-compilation-variables-javascript.md)   
 [@cc_on 语句](../../javascript/reference/at-cc-on-statement-javascript.md)   
 [@if 语句](../../javascript/reference/at-if-statement-javascript.md)   
 [@set 语句](../../javascript/reference/at-set-statement-javascript.md)