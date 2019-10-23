---
title: "\"无法更改值\" 对话框 |Microsoft Docs"
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.debug.variables.failededit
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- Cannot Change Value dialog box
- variables [debugger], editing
ms.assetid: 19e930c2-5fbf-4c83-aae8-a1dc3f8fcae8
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 97f057edefefd590c37b49d709ecf8a6e029b905
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72745743"
---
# <a name="cannot-change-value-dialog-box"></a>“无法更改值”对话框
## <a name="error"></a>Error
 `The value of this variable cannot be changed` &#124; `The name` *name* `does not exist in the current context` &#124; *various other messages*

 在调试器窗口（“自动”、“监视”或“局部变量”窗口）或“快速监视”对话框中，当尝试将变量内容更改为无效值时，会出现该消息框。 例如，如果尝试将整数变量的值设置为字符串，则将出现此消息框。

## <a name="solution"></a>解决方案
 确保键入到调试器窗口或“快速监视”对话框中的输入表示要尝试设置的变量的合法值。

## <a name="see-also"></a>请参阅

- [调试器中的表达式](../debugger/expressions-in-the-debugger.md)