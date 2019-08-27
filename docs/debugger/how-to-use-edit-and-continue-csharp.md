---
title: 如何：使用编辑并继续 (C#) |Microsoft Docs
ms.date: 10/04/2018
ms.topic: conceptual
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
ms.openlocfilehash: 515068f29045ef92ee7d2323f752ba2185f28cac
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62906266"
---
# <a name="how-to-use-edit-and-continue-c"></a>如何：使用“编辑并继续”(C#)
编辑并继续，可以建立并调试，而无需停止和重新启动调试会话时将更改应用到你的代码在中断模式下。

编辑并继续的C#当你在中断模式下进行代码更改，然后继续进行调试，通过使用自动发生**继续**，**步骤**，或**设置下一语句**，或计算在调试器窗口函数。

有关详细信息，请参阅[编辑并继续 (Visual C#)](../debugger/edit-and-continue-visual-csharp.md)。

>[!NOTE]
>编辑并继续的优化，不支持混合使用，或 SQL Server 公共语言运行时 (CLR) 集成代码。 有关其他不受支持方案的信息，请参阅[支持的代码更改 (C#和 Visual Basic)](../debugger/supported-code-changes-csharp.md)。 如果你尝试编辑并继续使用其中一种情形，出现一个消息框，指出，不支持编辑并继续。

**若要启用或禁用编辑并继续：**

1. 如果您在调试会话中，停止调试 (**调试** > **停止调试**或**Shift**+**F5**).

1. 在中**工具** > **选项**(或**调试** > **选项**) >**调试** > **常规**，选中或清除**启用编辑并继续**复选框。

启动或重新启动调试会话时，该设置将生效。

**若要使用编辑并继续：**

1. 在中断模式中调试时对源代码进行更改。

1. 从**调试**菜单上，单击**继续**，**步骤**，或者**设置下一语句**，或计算在调试器窗口函数。

   调试时，将继续使用新的、 已编译代码。

编辑并继续不支持某些类型的代码更改。 有关详细信息，请参阅[支持的代码更改（C# 和 Visual Basic）](../debugger/supported-code-changes-csharp.md)。
