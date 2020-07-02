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
ms.openlocfilehash: ca6f13620bb486cf1663bd5bef9a9a93b2c8a480
ms.sourcegitcommit: ca777040ca372014b9af5e188d9b60bf56e3e36f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85817354"
---
# <a name="function-does-not-have-a-valid-prototype-object"></a>函数没有有效的原型对象
您尝试使用**instanceof**来确定对象是否派生自特定函数类，但您将对象的属性重新定义 `prototype` 为 `null` 或外部对象类型（这两个对象都无效 [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] ）。 外部对象可以是宿主对象模型中的对象（例如，Internet Explorer 的文档或窗口对象），也可以是外部 COM 对象。  
  
### <a name="to-correct-this-error"></a>更正此错误  
  
- 确保函数的 `prototype` 属性引用有效的 [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] 对象。  
  
## <a name="see-also"></a>请参阅  
 [Function 对象](../../javascript/reference/function-object-javascript.md)   
 [prototype 属性 (Object)](../../javascript/reference/prototype-property-object-javascript.md)