---
title: 应为正则表达式对象 |Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: reference
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
ms.openlocfilehash: bf9e2e99c6a539f450afcfe9eef1f5588d5b84f6
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72573706"
---
# <a name="regular-expression-object-expected"></a>应为正则表达式对象
试图对 `RegExp`以外的类型的对象调用**RegExp. toString**或**valueOf**方法的方法。 此类调用的对象必须是 `RegExp`类型。  
  
### <a name="to-correct-this-error"></a>更正此错误  
  
- 在 `RegExp`类型的对象上只调用**RegExp**或**valueOf**方法。  
  
## <a name="see-also"></a>另请参阅  
 [正则表达式对象](../../javascript/reference/regular-expression-object-javascript.md)   
 [正则表达式语法（JavaScript）](https://msdn.microsoft.com/library/1400241x)