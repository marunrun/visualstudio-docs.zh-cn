---
title: 应为枚举器对象 |Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: error-reference
f1_keywords:
- VS.WebClient.Help.SCRIPT5015
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: dc6e32c1-a6e6-4e12-ac99-e3f65f91c8d7
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: ff61894ce808cd33876e876c596e791a3347ab72
ms.sourcegitcommit: ca777040ca372014b9af5e188d9b60bf56e3e36f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85817588"
---
# <a name="enumerator-object-expected"></a>缺少枚举器对象
您试图对非类型的对象调用**atEnd、moveFirst、或**方法的调用程序，则不能调用该方法的**方法。** `Enumerator` 此类调用的对象必须是类型 `Enumerator` 。 下面是中断此规则的代码示例：  
  
```JavaScript  
var o = new Object;  
o.f = Enumerator.prototype.atEnd;  
o.f();  
```  
  
### <a name="to-correct-this-error"></a>更正此错误  
  
- 仅对类型为的对象调用**atEnd**、 **Enumerator.prototype.item**moveFirst、**或**方法，然后**调用枚举器** `Enumerator` 方法。 若要确定对象是否为 `Enumerator` 对象，请使用：  
  
    ```js
    if(x instanceof Enumerator)  
    ```  
  
## <a name="see-also"></a>请参阅  
 [Enumerator 对象](../../javascript/reference/enumerator-object-javascript.md)