---
title: 适用于标识符的语句结束 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- IntelliSense [JavaScript], statement completion
- statement completion, JavaScript IntelliSense
ms.assetid: c2cd4945-c67e-471b-8057-96cfd25f7fb2
caps.latest.revision: 17
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 89f507c2f4d01cf5e3e1e983cfcb5bafd9d9a7dd
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68152898"
---
# <a name="statement-completion-for-identifiers"></a>适用于标识符的语句结束
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

JavaScript 不允许显式类型的变量声明。 因此，IntelliSense 始终不能为对象提供完成列表。 这可能在不同情况下。 以下是几个常见的。  
  
- 声明的参数，但它尚未调用其他位置在活动文档中，如下面的示例中所示。  
  
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
  
- 对象是在响应事件中调用的函数中。 在设计时 IntelliSense 引擎无法确定在此情况下使用的对象的类型。  
  
   如果 IntelliSense 引擎可以确定应调用该事件，这通常是通过使用`addEventListener`活动文档中的事件，提供更准确的 IntelliSense 信息。  
  
  IntelliSense 无法确定一个对象时，IntelliSense 引擎将填充与命名的实体或标识符，活动文档中存在的完成列表。 当完成列表中包含这些标识符时，旁边显示信息图标。 此外，每个标识符的工具提示指示表达式是未知。 下图显示了语句完成选项的类型的对象`light`对象和其属性是不确定因为无法识别的。 但是，`intensity`属性是出现在标识符列表中，因为中使用`illuminate`函数。  
  
  **无法识别的对象的完成选项**  
  
  ![适用于标识符 JavaScript IntelliSense](../ide/media/js-intellisense-identifiers.png "js_intellisense_identifiers")  
  
  使用 XML 文档注释或 JavaScript IntelliSense 扩展性功能，可以重写对象的完成列表。 使用这些功能，您可以提供类型信息和更具描述性的 IntelliSense 信息时它可能否则不可用。 有关详细信息，请参阅[扩展 JavaScript IntelliSense](../ide/extending-javascript-intellisense.md)并[创建 XML 文档注释](../ide/create-xml-documentation-comments-for-javascript-intellisense.md)。  
  
## <a name="see-also"></a>另请参阅  
 [JavaScript IntelliSense](../ide/javascript-intellisense.md)
