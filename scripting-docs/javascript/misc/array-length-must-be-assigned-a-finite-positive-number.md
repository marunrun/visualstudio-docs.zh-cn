---
title: 数组长度必须分配有有限正数 |Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: reference
f1_keywords:
- VS.WebClient.Help.SCRIPT5030
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: c51c66a4-a543-4e95-b18d-2cfbcb3d1fdd
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: cff9c8c42199e106cca5f6f2808866e46a26afe2
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72576064"
---
# <a name="array-length-must-be-assigned-a-finite-positive-number"></a>数组长度必须赋值为有限正数
在设置现有**数组**对象的**length**属性时，指定的数组长度不是正数或零。 向负数或非数字（`NaN`）的 `Array` 对象的**length**属性赋值时，将发生此错误。 请注意，[!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] 会自动将小数值转换为整数。  
  
### <a name="to-correct-this-error"></a>更正此错误  
  
- 将正整数赋给 length 属性。 除最大整数值（大约4000000000）外，数组的大小没有上限。 下面的示例演示设置**数组**对象的**length**属性的正确方法。  
  
    ```JavaScript  
    var my_array = new Array();  
    my_array.length = 99;  
    ```  
  
## <a name="see-also"></a>请参阅  
 [使用数组](../../javascript/advanced/using-arrays-javascript.md)