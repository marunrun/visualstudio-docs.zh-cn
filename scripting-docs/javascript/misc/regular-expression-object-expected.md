---
title: 应为正则表达式对象 |Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: error-reference
f1_keywords:
- VS.WebClient.Help.SCRIPT5016
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: e226096c-c58f-4bcb-a71e-fa32ce474b67
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: d9f5816c0bf3ad7c8dbf7d394952c631923d89cf
ms.sourcegitcommit: ca777040ca372014b9af5e188d9b60bf56e3e36f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85814624"
---
# <a name="regular-expression-object-expected"></a>应为正则表达式对象
您试图对非类型的对象调用**valueOf** **方法，而**不是调用方法。 `RegExp` 此类调用的对象必须是类型 `RegExp` 。  
  
### <a name="to-correct-this-error"></a>更正此错误  
  
- 仅对类型为的对象调用**valueOf** **或方法** `RegExp` 方法。  
  
## <a name="see-also"></a>请参阅  
 [正则表达式对象](../../javascript/reference/regular-expression-object-javascript.md)   
 [正则表达式语法（JavaScript）](https://msdn.microsoft.com/library/1400241x)