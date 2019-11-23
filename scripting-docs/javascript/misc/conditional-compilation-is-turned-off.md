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
ms.openlocfilehash: 56621d6f7fcc195a4ece7654adeafd1096c37e8b
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72572942"
---
# <a name="conditional-compilation-is-turned-off"></a>条件编译已关闭
您尝试在不先打开的条件编译的情况下使用条件编译变量。 启用条件编译会告知 [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] 编译器将以 @ 开头的标识符解释为条件编译变量。 为此，可通过在语句开头使用条件代码来执行此操作：  
  
```js
/*@cc_on @*/  
```  
  
### <a name="to-correct-this-error"></a>更正此错误  
  
- 在条件代码的开头添加以下语句：  
  
    ```JavaScript  
    /*@cc_on @*/  
    ```  
  
## <a name="see-also"></a>另请参阅  
 [条件编译](../../javascript/advanced/conditional-compilation-javascript.md)   
 [条件编译变量](../../javascript/advanced/conditional-compilation-variables-javascript.md)   
 [@cc_on 语句](../../javascript/reference/at-cc-on-statement-javascript.md)   
 [@if 语句](../../javascript/reference/at-if-statement-javascript.md)   
 [@set 语句](../../javascript/reference/at-set-statement-javascript.md)