---
title: 不能在循环外使用 "continue" |Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: reference
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
ms.openlocfilehash: e19c85baf8576d1c1db411146c80a53c6a819cdb
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72572376"
---
# <a name="cant-have-continue-outside-of-loop"></a>“continue”不能位于循环外
尝试在循环外使用**continue**语句。 **Continue**语句只能在的主体内使用：  
  
- `do-while` 循环，  
  
- `while` 循环，  
  
- **for**循环，  
  
- **for/in**循环。  
  
### <a name="to-correct-this-error"></a>更正此错误  
  
- 请确保在正文中出现**continue**语句：  
  
  - `do-while` 循环，  

  - `while` 循环，  

  - **for**循环，  

  - **for/in**循环。  
  
## <a name="see-also"></a>请参阅  
 [Continue 语句](../../javascript/reference/continue-statement-javascript.md)   
 [控制程序流](../../javascript/controlling-program-flow-javascript.md)   
 [脚本疑难解答](../../javascript/advanced/troubleshooting-your-scripts-javascript.md)
