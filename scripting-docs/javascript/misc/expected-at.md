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
ms.openlocfilehash: 98a35421054e4d2236fe509224ed146063b61a79
ms.sourcegitcommit: e38419bb842d587fd9e37c24b6cf3fc5c2e74817
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/09/2020
ms.locfileid: "91862311"
---
# <a name="expected-"></a>应有“\@”
您尝试使用语句创建一个与条件编译语句一起使用的变量 `@set` ，但没有在变量名称之前加上符号 " **@** "。  
  
### <a name="to-correct-this-error"></a>更正此错误  
  
- **@** 紧靠在变量名称之前添加 ""。 例如：  
  
    ```JavaScript  
    @set @myvar = 1  
    ```  
  
## <a name="see-also"></a>请参阅  
 [@set 损益](https://developer.mozilla.org/docs/Archive/Web/JavaScript/Microsoft_Extensions/at-set)   
 [条件编译](/previous-versions/windows/internet-explorer/ie-developer/scripting-articles/121hztk3(v=vs.84))   
 [条件编译变量](/previous-versions/windows/internet-explorer/ie-developer/scripting-articles/s59bkzce(v=vs.84))