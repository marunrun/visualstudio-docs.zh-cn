---
title: 数组长度必须分配有有限正数 |Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: error-reference
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
ms.openlocfilehash: 30e02f4f90300e2c05076553419cda5f8c353ab0
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "85817679"
---
# <a name="array-length-must-be-assigned-a-finite-positive-number"></a>数组长度必须赋值为有限正数
在设置现有**数组**对象的**length**属性时，指定的数组长度不是正数或零。 将值分配给对象的 **length** 属性时，如果该 `Array` 对象为负数 () ，则会发生此错误 `NaN` 。 请注意， [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] 会自动将小数值转换为整数。  
  
### <a name="to-correct-this-error"></a>更正此错误  
  
- 将正整数赋给 length 属性。 除了最大整数值 (大约 4000000000) 以外，数组大小没有上限。 下面的示例演示设置**数组**对象的**length**属性的正确方法。  
  
    ```JavaScript  
    var my_array = new Array();  
    my_array.length = 99;  
    ```  
  
## <a name="see-also"></a>另请参阅  
 [使用数组](../../javascript/advanced/using-arrays-javascript.md)