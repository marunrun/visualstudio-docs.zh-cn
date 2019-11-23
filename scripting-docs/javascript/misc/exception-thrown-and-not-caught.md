---
title: 引发了异常且未被捕获 |Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: reference
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
ms.openlocfilehash: 05a9e4f51d5daf7a9e1b1153acbbe8b76b539b72
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72572853"
---
# <a name="exception-thrown-and-not-caught"></a>引发了异常且未被捕获
你在代码中包含了 `throw` 语句，但它未包含在**try**块中，或者没有关联的**catch**块捕获该错误。 使用**throw**语句从**try**块内部引发异常，并使用**catch**语句在**try**块外捕获异常。  
  
### <a name="to-correct-this-error"></a>更正此错误  
  
- 将可以在**try**块中引发异常的代码括起来，并确保存在相应的**catch**块。  
  
- 请确保 catch 语句需要正确的异常形式。  
  
- 如果重新引发异常，请确保有另一个相应的 catch 语句。  
  
## <a name="see-also"></a>另请参阅  
 [错误对象](../../javascript/reference/error-object-javascript.md)   
 [Throw 语句](../../javascript/reference/throw-statement-javascript.md)   
 [try...catch...finally 语句](../../javascript/reference/try-dot-dot-dot-catch-dot-dot-dot-finally-statement-javascript.md)