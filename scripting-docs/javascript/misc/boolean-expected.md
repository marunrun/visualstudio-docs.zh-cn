---
title: 缺少布尔值 |Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: reference
f1_keywords:
- VS.WebClient.Help.SCRIPT5010
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: 35d71b7f-53fd-44c4-a7c7-b1550c65cfd4
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 261cf0ad93208c0eac09e42dcd68853352318e88
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62817895"
---
# <a name="boolean-expected"></a>缺少布尔值
你尝试调用**Boolean.prototype.toString**或**Boolean.prototype.valueOf**方法以外的类型的对象上`Boolean`。 调用此类型的对象的类型必须是`Boolean`。 例如：

```JavaScript
var o = new Object;
o.f = Boolean.prototype.toString;
o.f();
```

## <a name="to-correct-this-error"></a>更正此错误

- 仅调用**Boolean.prototype.toString**或**Boolean.prototype.valueOf**类型的对象上的方法**布尔值。**

## <a name="see-also"></a>请参阅

- [Boolean 对象](../../javascript/reference/boolean-object-javascript.md)
- [数据类型](../../javascript/data-types-javascript.md)
- [控制程序流](../../javascript/controlling-program-flow-javascript.md)
- [复制、传递和比较数据](../../javascript/advanced/copying-passing-and-comparing-data-javascript.md)