---
title: Loop 外不能有 "break" |Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: error-reference
f1_keywords:
- VS.WebClient.Help.SCRIPT1019
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: 11d02172-2a78-4705-a730-d21111db5f42
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: ee177c8070fc5af8123d7fd78e69b1f767a5b700
ms.sourcegitcommit: e38419bb842d587fd9e37c24b6cf3fc5c2e74817
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/09/2020
ms.locfileid: "91862795"
---
# <a name="cant-have-break-outside-of-loop"></a>“break”不能位于循环外
尝试在循环外使用 **break** 关键字。 **Break**关键字用于终止循环或 `switch` 语句。 它必须嵌入到循环或语句的主体中 `switch` 。 但是， **标签** 可以跟在 break 关键字之后。  
  
```js
break labelname;  
```  
  
 使用嵌套循环或语句时，只需要带有标记形式的 **break** 关键字 `switch` ，需要中断不是最内层的循环。  
  
### <a name="to-correct-this-error"></a>更正此错误  
  
- 请确保 **break** 关键字显示在封闭循环或 switch 语句内。  
  
## <a name="see-also"></a>请参阅  
 [break 语句](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/break)   
 [控制程序流](https://developer.mozilla.org/docs/Web/JavaScript/Guide/Control_flow_and_error_handling)   
 [脚本疑难解答](https://developer.mozilla.org/docs/Learn/JavaScript/First_steps/What_went_wrong)