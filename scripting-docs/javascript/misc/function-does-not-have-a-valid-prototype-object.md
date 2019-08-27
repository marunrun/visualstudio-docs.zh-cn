---
title: 函数没有有效的原型对象 |Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: reference
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
ms.openlocfilehash: 413f73a53a6d4f698219139a87c449be4c155831
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63007498"
---
# <a name="function-does-not-have-a-valid-prototype-object"></a>函数没有有效的原型对象
你尝试使用**instanceof**若要确定是否已从特定函数类派生的对象，但重新定义对象的`prototype`属性为`null`，或外部的对象类型 (这两个不是有效[!INCLUDE[javascript](../../javascript/includes/javascript-md.md)]对象)。 外部对象可以是主机对象模型 （例如，Internet Explorer 的文档或窗口对象） 中的对象或一个外部 COM 对象。  
  
### <a name="to-correct-this-error"></a>更正此错误  
  
- 请确保该函数的`prototype`属性是指一个有效[!INCLUDE[javascript](../../javascript/includes/javascript-md.md)]对象。  
  
## <a name="see-also"></a>请参阅  
 [函数对象](../../javascript/reference/function-object-javascript.md)   
 [prototype 属性 (Object)](../../javascript/reference/prototype-property-object-javascript.md)