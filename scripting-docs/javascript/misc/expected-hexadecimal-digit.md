---
title: 预期的十六进制数字 |Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: reference
f1_keywords:
- VS.WebClient.Help.SCRIPT1023
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: 67a86df7-49f9-43cb-99c6-99b1a427827a
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 82f020b5f3b82ab2ce3545102be83a5cd41c6069
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63446521"
---
# <a name="expected-hexadecimal-digit"></a>应为十六进制数字
创建一个不正确的 Unicode 转义序列。 Unicode 转义序列开头 \u，跟 4 个十六进制数字 （没有更多且不小于）。 Unicode 十六进制数字可以包含数字 0-9、 大小写字母 A-F 和小写字母 a 到 f。 下面的示例演示一个格式正确的 Unicode 转义序列。  
  
```JavaScript  
z = "\u1A5F";  
```  
  
### <a name="to-correct-this-error"></a>更正此错误  
  
- 确保你 Unicode 十六进制数字开头 \u，仅包含数字 0-9、 大小写字母 A 到 F，小写字母 a 到 f;分为一到四位数字。  
  
    > [!NOTE]
    > 如果你想要在字符串内，使用 \u 文本，然后使用两个反斜杠 (\\\u)-一个用于第一个反斜杠转义。  
  
## <a name="see-also"></a>请参阅  
 [数据类型](../../javascript/data-types-javascript.md)