---
title: 引发了异常且未被捕获 |Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: error-reference
f1_keywords:
- VS.WebClient.Help.SCRIPT5022
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: b5235490-a8e7-42e3-804e-d85235bc6f05
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 6a0e3eb6d1275e5598ad44ea553e22f0b53eeb45
ms.sourcegitcommit: e38419bb842d587fd9e37c24b6cf3fc5c2e74817
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/09/2020
ms.locfileid: "91862767"
---
# <a name="exception-thrown-and-not-caught"></a>引发了异常且未被捕获
你在代码中包含了一个 `throw` 语句，但该语句未包含在 **try** 块中，或者没有关联的 **catch** 块捕获该错误。 使用**throw**语句从**try**块内部引发异常，并使用**catch**语句在**try**块外捕获异常。  
  
### <a name="to-correct-this-error"></a>更正此错误  
  
- 将可以在 **try** 块中引发异常的代码括起来，并确保存在相应的 **catch** 块。  
  
- 请确保 catch 语句需要正确的异常形式。  
  
- 如果重新引发异常，请确保有另一个相应的 catch 语句。  
  
## <a name="see-also"></a>请参阅  
 [Error 对象](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Error)   
 [throw 语句](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/throw)   
 [尝试 .。。catch .。。finally 语句](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/try...catch)