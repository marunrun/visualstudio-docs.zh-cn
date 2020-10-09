---
title: 函数没有有效的原型对象 |Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: error-reference
f1_keywords:
- VS.WebClient.Help.SCRIPT5023
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: b9e34652-190f-4b57-b253-df2e8c4d09c6
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 15b00087cd66b873044b7bafb1bfecf4fc91f8d9
ms.sourcegitcommit: e38419bb842d587fd9e37c24b6cf3fc5c2e74817
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/09/2020
ms.locfileid: "91862401"
---
# <a name="function-does-not-have-a-valid-prototype-object"></a>函数没有有效的原型对象
您尝试使用 **instanceof** 来确定对象是否派生自特定函数类，但您将对象的属性重新定义 `prototype` 为 `null` 或外部对象类型 (不是有效的 [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] 对象) 。 外部对象可以是宿主对象模型中的对象 (例如，Internet Explorer 的文档或窗口对象) 或外部 COM 对象。  
  
### <a name="to-correct-this-error"></a>更正此错误  
  
- 确保函数的 `prototype` 属性引用有效的 [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] 对象。  
  
## <a name="see-also"></a>请参阅  
 [Function 对象](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Function)   
 [prototype 属性 (Object)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object)