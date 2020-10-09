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
ms.openlocfilehash: b6d88815a33187e209bcba248d3c363afdd91227
ms.sourcegitcommit: e38419bb842d587fd9e37c24b6cf3fc5c2e74817
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/09/2020
ms.locfileid: "91862662"
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

- [Boolean 对象](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Boolean)
- [数据类型](https://developer.mozilla.org/docs/Web/JavaScript/Data_structures)
- [控制程序流](https://developer.mozilla.org/docs/Web/JavaScript/Guide/Control_flow_and_error_handling)
- [复制、传递和比较数据](https://developer.mozilla.org/docs/Web/JavaScript/Guide/Functions)