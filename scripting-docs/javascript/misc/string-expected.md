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
ms.openlocfilehash: 96c08b8b50b64ccfb7d770ade41510897ad0ff5a
ms.sourcegitcommit: ca777040ca372014b9af5e188d9b60bf56e3e36f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85817536"
---
# <a name="string-expected"></a>缺少字符串
您尝试对类型之外的对象调用**valueOf**方法，而不是**调用的方法** `String` 。 此类调用的对象必须是类型 `String` 。  
  
### <a name="to-correct-this-error"></a>更正此错误  
  
- 仅对类型为的对象调用 valueOf 或**String.prototype.valueOf** **方法。** `String`  
  
## <a name="see-also"></a>请参阅  
 [String 对象](../../javascript/reference/string-object-javascript.md)   
 [toString 方法 (Object)](../../javascript/reference/tostring-method-object-javascript.md)