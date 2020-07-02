---
title: 应输入日期对象 |Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: error-reference
f1_keywords:
- VS.WebClient.Help.SCRIPT5006
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: d6ab82e6-ca64-46b4-a06c-5c6b0aa057cb
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 969f2bcb578d74ac02a7bdaa6984de5948e49e27
ms.sourcegitcommit: ca777040ca372014b9af5e188d9b60bf56e3e36f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85817601"
---
# <a name="date-object-expected"></a>缺少日期对象
您尝试对类型之外的对象调用**valueOf** **方法，而**不是对该对象调用 `Date` 。 此类调用的对象必须是类型 `Date` 。 例如：  
  
```JavaScript  
var o = new Object;  
o.f = Date.prototype.toString;  
o.f();  
```  
  
### <a name="to-correct-this-error"></a>更正此错误  
  
- 仅**对类型**为的对象调用 valueOf 或**Date.prototype.valueOf** `Date` 方法。  
  
## <a name="see-also"></a>请参阅  
 [Date 对象](../../javascript/reference/date-object-javascript.md)   
 [getDate 方法（Date）](../../javascript/reference/getdate-method-date-javascript.md)   
 [内部对象](../../javascript/intrinsic-objects-javascript.md)