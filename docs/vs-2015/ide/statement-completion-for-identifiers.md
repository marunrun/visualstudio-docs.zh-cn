---
title: 标识符的语句结束 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- IntelliSense [JavaScript], statement completion
- statement completion, JavaScript IntelliSense
ms.assetid: c2cd4945-c67e-471b-8057-96cfd25f7fb2
caps.latest.revision: 17
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: f5e52bf174e5a41d79fa23bfca39121db668e40e
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72643862"
---
# <a name="statement-completion-for-identifiers"></a>适用于标识符的语句结束
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

JavaScript 不允许显式键入变量声明。 因此，IntelliSense 不能始终为对象提供完成列表。 在各种情况下可能会发生这种情况。 下面是一些常见的例子。

- 声明了一个参数，但该参数尚未在活动文档中的其他位置调用，如下面的示例中所示。

  ```javascript
  function illuminate(light) {
           light.  // Accurate statement completion is not available
                   // unless illuminate is called elsewhere with a
                   // parameter that has a value. If it is called only
                   // in a function that is a sibling to
                   // illuminate(light) in the call hierarchy, the
                   // IntelliSense engine also cannot determine the
                   // parameter type.
       }

  // Sibling function. No statement completion for light
  // object in preceding code.
  function lightLamp() {
      var x = illuminate(1);
  }

  // Uncomment the next line to obtain statement completion for
  // light object in preceding code.
  // var x = illuminate(1);
  ```

- 对象位于为响应事件而调用的函数中。 在设计时，IntelliSense 引擎无法确定此情况下使用的对象的类型。

   如果 IntelliSense 引擎可以确定应调用事件（通常通过使用 `addEventListener` 活动文档中的事件），则提供更准确的 IntelliSense 信息。

  当 IntelliSense 无法标识对象时，IntelliSense 引擎将使用活动文档中的命名实体或标识符填充完成列表。 当完成列表包含这些标识符时，它们旁边会出现信息图标。 此外，每个标识符的工具提示将指示该表达式是未知的。 下图显示了无法标识的对象类型 `light` 的语句完成选项，因为未定义对象及其属性。 但是，`intensity` 属性在标识符列表中可用，因为它已在 `illuminate` 函数中使用。

  **无法识别的对象的完成选项**

  ![适用于标识符的 JavaScript IntelliSense](../ide/media/js-intellisense-identifiers.png "|::ref1::|")

  可以通过使用 XML 文档注释或 JavaScript IntelliSense 扩展性功能，替代对象的完成列表。 使用这些功能时，可以提供类型信息，并提供更具描述性的 IntelliSense 信息，在其他情况下可能无法使用。 有关详细信息，请参阅[扩展 JavaScript IntelliSense](../ide/extending-javascript-intellisense.md)和[创建 XML 文档注释](../ide/create-xml-documentation-comments-for-javascript-intellisense.md)。

## <a name="see-also"></a>另请参阅
 [JavaScript IntelliSense](../ide/javascript-intellisense.md)
