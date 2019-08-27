---
title: 数组长度必须赋值为有限正数 |Microsoft Docs
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
ms.openlocfilehash: 39f2720efbcd8defffb9d0c77047a50e57939e95
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62818038"
---
# <a name="array-length-must-be-assigned-a-finite-positive-number"></a>数组长度必须赋值为有限正数
设置时**长度**属性的现有**数组**对象，指定不是正数值或零的数组长度。 此错误发生时将值赋给**长度**的属性`Array`对象，它为负或不是数字 (`NaN`)。 请注意，[!INCLUDE[javascript](../../javascript/includes/javascript-md.md)]自动将小数数字转换为整数。  
  
### <a name="to-correct-this-error"></a>更正此错误  
  
- 将一个正整数分配给 length 属性。 没有任何大小的数组，最大整数值 （大约 40 亿个） 以外的值的上限。 下面的示例演示设置的正确方式**长度**的属性**数组**对象。  
  
    ```JavaScript  
    var my_array = new Array();  
    my_array.length = 99;  
    ```  
  
## <a name="see-also"></a>请参阅  
 [使用数组](../../javascript/advanced/using-arrays-javascript.md)