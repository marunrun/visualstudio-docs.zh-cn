---
title: 无法将分配给 this |Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: reference
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
ms.openlocfilehash: 4a4ba5d852a7d131a88930dd66931c026074549b
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62946584"
---
# <a name="cannot-assign-to-this"></a>无法给“this”赋值
尝试将一个值赋给**这**。 **这**是[!INCLUDE[javascript](../../javascript/includes/javascript-md.md)]关键字是指：

- 当前正在执行的一种方法，该对象

- 如果没有当前方法 （或该方法不属于任何其他对象） 全局对象。

一种方法是[!INCLUDE[javascript](../../javascript/includes/javascript-md.md)]通过对象调用的函数。 在方法中，**这**关键字是通过调用该方法的对象的引用 (正好是通过调用类构造函数创建的对象**新**运算符)。

在方法中，可以使用**这**来指代当前对象，但您不能将新值赋给**这**。

## <a name="to-correct-this-error"></a>更正此错误

- 不要尝试将分配给**这**。 若要访问的属性或方法实例化的对象，请使用点运算符 (例如， **circle.radius**)。

  > [!NOTE]
  > 不能将命名用户创建的变量**这**; 它是[!INCLUDE[javascript](../../javascript/includes/javascript-md.md)]保留字。

## <a name="see-also"></a>请参阅

- [this 语句](../../javascript/reference/this-statement-javascript.md)
- [脚本疑难解答](../../javascript/advanced/troubleshooting-your-scripts-javascript.md)