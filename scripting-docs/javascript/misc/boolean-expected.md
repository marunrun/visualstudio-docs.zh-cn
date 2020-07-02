---
title: 应为布尔值 |Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: error-reference
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
ms.openlocfilehash: 4dbb7e55f6afe6d3edfe4e98749807732ffa05ac
ms.sourcegitcommit: ca777040ca372014b9af5e188d9b60bf56e3e36f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85817666"
---
# <a name="boolean-expected"></a>缺少布尔值
您尝试对类型之外的对象调用**valueOf**方法，而不是**调用的方法** `Boolean` 。 此类调用的对象必须是类型 `Boolean` 。 例如：

```JavaScript
var o = new Object;
o.f = Boolean.prototype.toString;
o.f();
```

## <a name="to-correct-this-error"></a>更正此错误

- 仅对**布尔**类型的对象调用**valueOf** **方法或布尔**方法。

## <a name="see-also"></a>请参阅

- [Boolean 对象](../../javascript/reference/boolean-object-javascript.md)
- [数据类型](../../javascript/data-types-javascript.md)
- [控制程序流](../../javascript/controlling-program-flow-javascript.md)
- [复制、传递和比较数据](../../javascript/advanced/copying-passing-and-comparing-data-javascript.md)