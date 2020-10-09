---
title: 不能在循环外使用 "continue" |Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: error-reference
f1_keywords:
- VS.WebClient.Help.SCRIPT1020
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: d2d95259-b2bc-4069-9876-60c30ad600a3
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 14745c5789fe6c0350f83e46ee0e918f92789d96
ms.sourcegitcommit: e38419bb842d587fd9e37c24b6cf3fc5c2e74817
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/09/2020
ms.locfileid: "91861982"
---
# <a name="cant-have-continue-outside-of-loop"></a>“continue”不能位于循环外
尝试在循环外使用 **continue** 语句。 **Continue**语句只能在的主体内使用：  
  
- `do-while` 圈  
  
- `while` 圈  
  
- **for** 循环，  
  
- **for/in** 循环。  
  
### <a name="to-correct-this-error"></a>更正此错误  
  
- 请确保在正文中出现 **continue** 语句：  
  
  - `do-while` 圈  

  - `while` 圈  

  - **for** 循环，  

  - **for/in** 循环。  
  
## <a name="see-also"></a>请参阅  
 [continue 语句](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/continue)   
 [控制程序流](https://developer.mozilla.org/docs/Web/JavaScript/Guide/Control_flow_and_error_handling)   
 [脚本疑难解答](https://developer.mozilla.org/docs/Learn/JavaScript/First_steps/What_went_wrong)