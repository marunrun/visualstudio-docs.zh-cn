---
title: 应为枚举器对象 |Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: reference
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
ms.openlocfilehash: d90b6b923f631c7785428a1b3879528e97c1bfd6
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72572875"
---
# <a name="enumerator-object-expected"></a>缺少枚举器对象
尝试在 `Enumerator` 以外的类型的对象上调用**atEnd、moveFirst、或**方法 **，则不**能调用。 "|" 此类调用的对象必须是 `Enumerator` 类型。 下面是中断此规则的代码示例：  
  
```JavaScript  
var o = new Object;  
o.f = Enumerator.prototype.atEnd;  
o.f();  
```  
  
### <a name="to-correct-this-error"></a>更正此错误  
  
- 仅在 `Enumerator`类型的对象上调用 AtEnd **、** moveFirst、**或**方法 **，即对**类方法进行调用。 若要确定对象是否为 `Enumerator` 对象，请使用：  
  
    ```js
    if(x instanceof Enumerator)  
    ```  
  
## <a name="see-also"></a>请参阅  
 [Enumerator 对象](../../javascript/reference/enumerator-object-javascript.md)