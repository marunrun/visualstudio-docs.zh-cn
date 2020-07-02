---
title: 应为 "@" |Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: error-reference
f1_keywords:
- VS.WebClient.Help.SCRIPT1032
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: 82ff8b74-1710-4358-9a26-dc92ab29c53b
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 209a8793c0940511b7ecb2abb32f537a614ebf8b
ms.sourcegitcommit: ca777040ca372014b9af5e188d9b60bf56e3e36f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85814819"
---
# <a name="expected-"></a>应输入 " \@ "
您尝试使用语句创建一个与条件编译语句一起使用的变量 `@set` ，但没有在变量名称之前加上符号 " **@** "。  
  
### <a name="to-correct-this-error"></a>更正此错误  
  
- **@** 紧靠在变量名称之前添加 ""。 例如：  
  
    ```JavaScript  
    @set @myvar = 1  
    ```  
  
## <a name="see-also"></a>请参阅  
 [@set损益](../../javascript/reference/at-set-statement-javascript.md)   
 [条件编译](../../javascript/advanced/conditional-compilation-javascript.md)   
 [条件编译变量](../../javascript/advanced/conditional-compilation-variables-javascript.md)
