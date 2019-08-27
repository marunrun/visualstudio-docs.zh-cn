---
title: default 只能出现一次在 switch 语句 |Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: reference
f1_keywords:
- VS.WebClient.Help.SCRIPT1027
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: a94100f4-6ee5-4759-b635-9d309e47111e
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 24162efcc720d9c0073f8a5799c6278b8d3c8c62
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62946350"
---
# <a name="default-can-only-appear-once-in-a-switch-statement"></a>“default”在“switch”语句中只能出现一次
你尝试使用**默认**多次 switch 语句内的语句。 默认情况下始终是 switch 语句 （它是 fall-through 事例） 中的最后一个 case 语句。  
  
### <a name="to-correct-this-error"></a>更正此错误  
  
- 删除任何额外**默认**case 语句从你`switch`语句 （在大多数一个默认 case 语句，在 switch 语句中使用）。  
  
## <a name="see-also"></a>请参阅  
 [switch 语句](../../javascript/reference/switch-statement-javascript.md)   
 [控制程序流](../../javascript/controlling-program-flow-javascript.md)   
 [JavaScript 保留字](../../javascript/reference/javascript-reserved-words.md)