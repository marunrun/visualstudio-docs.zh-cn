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
ms.openlocfilehash: d6c821c63354ec1b7cc83e302a3c2682982696e2
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387680"
---
# <a name="how-to-apply-edits-in-break-mode-with-edit-and-continue-visual-basic"></a>如何：应用编辑在中断模式下使用编辑并继续 (Visual Basic)
可以在中断模式下使用“编辑并继续”编辑代码，然后不必停止和重新启动执行即可继续。

有关在调试时使用“编辑并继续”的限制，请参阅[受支持的代码更改（C# 和 Visual Basic）](../debugger/supported-code-changes-csharp.md)。

### <a name="to-edit-code-in-break-mode"></a>在中断模式下编辑代码

1. 执行下列操作之一进入中断模式：

    - 在代码中设置断点，从“调试”菜单选择“开始调试”，然后等待应用程序命中断点。

         或

    - 开始调试，然后从“调试”菜单中选择“全部中断”。

         或

    - 异常发生时，选择**启用编辑**上**异常助手**。

2. 进行任何所需和受支持的代码更改。

     有关详细信息，请参阅[受支持的代码更改（C# 和 Visual Basic）](../debugger/supported-code-changes-csharp.md)。

    > [!NOTE]
    > 如果尝试进行“编辑并继续”所不允许的代码更改，你的编辑将被加上紫色波浪线，并且“任务列表”中会出现一项任务。 除非撤消非法的代码更改，否则将无法继续执行代码。

3. 在 “调试” 菜单上，单击 “继续” 继续执行。

     现在将继续执行你的代码，并且已应用的编辑将并入项目中。

## <a name="see-also"></a>请参阅
- [支持的代码更改（C# 和 Visual Basic）](../debugger/supported-code-changes-csharp.md)
- [编辑并继续 (Visual Basic)](../debugger/edit-and-continue-visual-basic.md)
