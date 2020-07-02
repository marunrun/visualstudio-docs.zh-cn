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
ms.openlocfilehash: e1223b3cee7f0246d8d685260fb6ea9ad0045347
ms.sourcegitcommit: ca777040ca372014b9af5e188d9b60bf56e3e36f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85817640"
---
# <a name="cant-have-continue-outside-of-loop"></a>“continue”不能位于循环外
尝试在循环外使用**continue**语句。 **Continue**语句只能在的主体内使用：  
  
- `do-while`圈  
  
- `while`圈  
  
- **for**循环，  
  
- **for/in**循环。  
  
### <a name="to-correct-this-error"></a>更正此错误  
  
- 请确保在正文中出现**continue**语句：  
  
  - `do-while`圈  

  - `while`圈  

  - **for**循环，  

  - **for/in**循环。  
  
## <a name="see-also"></a>请参阅  
 [continue 语句](../../javascript/reference/continue-statement-javascript.md)   
 [控制程序流](../../javascript/controlling-program-flow-javascript.md)   
 [脚本疑难解答](../../javascript/advanced/troubleshooting-your-scripts-javascript.md)
