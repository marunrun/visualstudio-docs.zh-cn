---
title: Loop 外不能有 "break" |Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: reference
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
ms.openlocfilehash: 356e7022f940e696030b0cda4f71a599c147dd5a
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72576020"
---
# <a name="cant-have-break-outside-of-loop"></a>“break”不能位于循环外
尝试在循环外使用**break**关键字。 **Break**关键字用于终止循环或 `switch` 语句。 它必须嵌入到循环或 `switch` 语句的正文中。 但是，**标签**可以跟在 break 关键字之后。  
  
```js
break labelname;  
```  
  
 使用嵌套循环或 `switch` 语句时，只需要带有标记形式的**break**关键字，并需要中断非最内层的循环。  
  
### <a name="to-correct-this-error"></a>更正此错误  
  
- 请确保**break**关键字显示在封闭循环或 switch 语句内。  
  
## <a name="see-also"></a>另请参阅  
 [break 语句](../../javascript/reference/break-statement-javascript.md)   
 [控制程序流](../../javascript/controlling-program-flow-javascript.md)   
 [脚本疑难解答](../../javascript/advanced/troubleshooting-your-scripts-javascript.md)