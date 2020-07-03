---
title: 如何 - 使用“编辑并继续”(C#) | Microsoft Docs
ms.date: 10/04/2018
ms.topic: how-to
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- Edit and Continue [C#], about Edit and Continue
ms.assetid: 40e136d8-a08c-43bd-b313-fb821c55eb3c
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: a88cff54679ac0deae32bfeeff1dd96526f19ea7
ms.sourcegitcommit: c076fe12e459f0dbe2cd508e1294af14cb53119f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2020
ms.locfileid: "85348855"
---
# <a name="how-to-use-edit-and-continue-c"></a>如何：使用“编辑并继续”(C#)
使用“编辑并继续”，可以在调试时以中断模式对代码进行更改并应用，而无需停止并重新启动调试会话。

当你在中断模式下更改代码时，“编辑并继续”(C#) 将自动发生，然后使用“继续”、“步骤”或“设置下一个语句”继续调试，或在调试器窗口中计算函数  。

有关详细信息，请参阅[编辑并继续 (Visual C#)](../debugger/edit-and-continue-visual-csharp.md)。

>[!NOTE]
>优化、混合或 SQL Server 公共语言运行时 (CLR) 集成代码不支持“编辑并继续”。 有关其他不受支持的方案的信息，请参阅[支持的代码更改（C# 和 Visual Basic）](../debugger/supported-code-changes-csharp.md)。 如果尝试使用这些方案之一进行“编辑并继续”，则会出现一个消息框，指出不支持“编辑并继续”。

**启用或禁用“编辑并继续”：**

1. 如果正在进行调试会话，请停止调试（“调试” > “停止调试”或按 Shift+F5）   。

1. 在“工具” > “选项”>（或“调试” > “选项”）>“调试” > “常规”中，选择或清除“启用编辑并继续”复选框      。

该设置在启动或重新启动调试会话时生效。

**使用“编辑并继续”：**

1. 进行调试时，在中断模式下对源代码进行更改。

1. 在“调试”菜单中，单击“继续”、“步骤”或“设置下一个语句”，或在调试器窗口中计算函数   。

   调试将使用新的已编译代码继续进行。

“编辑并继续”不支持某些类型的代码更改。 有关详细信息，请参阅[支持的代码更改（C# 和 Visual Basic）](../debugger/supported-code-changes-csharp.md)。
