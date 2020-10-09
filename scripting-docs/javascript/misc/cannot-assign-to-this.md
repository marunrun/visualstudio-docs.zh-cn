---
title: 无法分配给 "this" |Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: error-reference
f1_keywords:
- VS.WebClient.Help.SCRIPT5000
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: ba2b0a2b-f0f8-4698-b335-a4ab6c166671
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 8985c7201a8e315353dd89ab5e1f5a3ad3b403ea
ms.sourcegitcommit: e38419bb842d587fd9e37c24b6cf3fc5c2e74817
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/09/2020
ms.locfileid: "91862776"
---
# <a name="cannot-assign-to-this"></a>无法给“this”赋值
您尝试为 **此**分配一个值。 **这** 是一个 [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] 关键字，引用：

- 当前正在执行方法的对象。

- 如果当前没有 (方法，或者方法不属于任何其他对象) ，则为全局对象。

方法是 [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] 通过对象调用的函数。 在方法中， **this** 关键字是对对象的引用，方法是通过使用 **新** 的运算符) 调用类构造函数而创建的 (。

在方法中，你可以使用 **它** 来引用当前对象，但不能为 **此**分配新的值。

## <a name="to-correct-this-error"></a>更正此错误

- 不要尝试分配到 **此**。 若要访问实例化对象的属性或方法，请使用点运算符 (例如， **circle**) 。

  > [!NOTE]
  > 不能将用户创建 **的变量命名**为：它是 [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] 保留字。

## <a name="see-also"></a>请参阅

- [此语句](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Operators/this)
- [脚本疑难解答](https://developer.mozilla.org/docs/Learn/JavaScript/First_steps/What_went_wrong)