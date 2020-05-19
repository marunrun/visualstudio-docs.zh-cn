---
title: 如何：使用“编辑并继续”在中断模式下应用编辑 |Microsoft Docs
ms.custom: seodec18
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.debug.variables.failededit
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- Edit and Continue [Visual Basic], applying edits in break mode
- break mode, applying code changes
- Edit and Continue, applying edits in break mode
- editing, break mode
- coding, editing in break mode
- code, editing in break mode
ms.assetid: 1eef7498-6a1f-4fba-8146-510adc6375c9
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 05340b4922262eb134aca8fef4bf215342e5a997
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72734023"
---
# <a name="how-to-apply-edits-in-break-mode-with-edit-and-continue-visual-basic"></a>如何：使用“编辑并继续”在中断模式下应用编辑 (Visual Basic)
可以在中断模式下使用“编辑并继续”编辑代码，然后不必停止和重新启动执行即可继续。

有关在调试时使用“编辑并继续”的限制，请参阅[受支持的代码更改（C# 和 Visual Basic）](../debugger/supported-code-changes-csharp.md)。

### <a name="to-edit-code-in-break-mode"></a>在中断模式下编辑代码

1. 执行下列操作之一进入中断模式：

    - 在代码中设置断点，从“调试”菜单选择“开始调试”，然后等待应用程序命中断点 。

         \- 或 -

    - 开始调试，然后从“调试”菜单中选择“全部中断” 。

         \- 或 -

    - 当发生异常时，从“异常情况助手”选择“启用编辑” 。

2. 进行任何所需的且受支持的代码更改。

     有关详细信息，请参阅[受支持的代码更改（C# 和 Visual Basic）](../debugger/supported-code-changes-csharp.md)。

    > [!NOTE]
    > 如果尝试进行“编辑并继续”所不允许的代码更改，你的编辑将被加上紫色波浪线，并且“任务列表”中会出现一项任务。 除非撤消非法的代码更改，否则将无法继续执行代码。

3. 在 “调试” 菜单上，单击 “继续” 继续执行 。

     在你所做的编辑已并入项目并已应用的情况下，你的代码继续执行。

## <a name="see-also"></a>请参阅
- [支持的代码更改（C# 和 Visual Basic）](../debugger/supported-code-changes-csharp.md)
- [编辑并继续 (Visual Basic)](../debugger/edit-and-continue-visual-basic.md)
