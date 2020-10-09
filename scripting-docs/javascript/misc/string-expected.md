---
title: 应为字符串 |Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: error-reference
f1_keywords:
- VS.WebClient.Help.SCRIPT5005
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: 4c214c4b-9cd7-473b-8d90-2344c0375c25
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 5c56acfd14ceebf2cb4ff582363ece558b189e14
ms.sourcegitcommit: e38419bb842d587fd9e37c24b6cf3fc5c2e74817
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/09/2020
ms.locfileid: "91862750"
---
# <a name="string-expected"></a>缺少字符串
您尝试对类型之外的对象调用**valueOf**方法，而不是**调用的方法** `String` 。 此类调用的对象必须是类型 `String` 。  
  
### <a name="to-correct-this-error"></a>更正此错误  
  
- 仅对类型为的对象调用 valueOf 或**String.prototype.valueOf** **方法。** `String`  
  
## <a name="see-also"></a>请参阅  
 [String 对象](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)   
 [toString 方法 (Object)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object/tostring)