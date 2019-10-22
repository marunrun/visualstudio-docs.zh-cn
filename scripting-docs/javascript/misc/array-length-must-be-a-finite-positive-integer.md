---
title: 数组长度必须为有限正整数 |Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: reference
f1_keywords:
- VS.WebClient.Help.SCRIPT5029
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: 1a467040-4702-4178-848f-418a5974e907
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 69494f1485a97ff4f2c98cf2493e5d0bc5b8aa9f
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72576083"
---
# <a name="array-length-must-be-a-finite-positive-integer"></a>数组长度必须为有限正整数
使用不是整数的参数调用**数组**构造函数（整数由零加正整数的集合）。  
  
### <a name="to-correct-this-error"></a>更正此错误  
  
- 仅当创建新的 `Array` 对象时，才使用正整数。 如果要创建一个数组，该数组包含不是整数的单个元素，请在两个步骤中执行此操作。 首先创建一个具有一个元素的数组，然后将该值放在第一个元素（array [0]）中。 下面是生成此错误的示例。  
  
    ```JavaScript  
    var piArray = new Array(3.14159);  
    ```  
  
     下面的示例演示了使用单个数值元素指定数组的正确方法。  
  
    ```JavaScript  
    var piArray = new Array(1);  
    piArray [0] = 3.14159;  
    ```  
  
     除最大整数值（大约4000000000）外，数组的大小没有上限。  
  
## <a name="see-also"></a>请参阅  
 [使用数组](../../javascript/advanced/using-arrays-javascript.md)