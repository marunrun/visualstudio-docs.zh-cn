---
title: 如何：启用和禁用“编辑并继续” | Microsoft Docs
ms.custom: seodec18
ms.date: 10/04/2018
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- /INCREMENTAL linker option
- Apply Code Changes command
- Edit and Continue, disabling
- code changes, applying in break mode
- INCREMENTAL linker option
- Edit and Continue, enabling
- break mode, applying code changes
- Edit and Continue, applying code changes
- Step command
- Go command
ms.assetid: fd961a1c-76fa-420d-ad8f-c1a6c003b0db
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
- cplusplus
ms.openlocfilehash: 2c8486bdcd7bc737d3851eabd88734df4efd80b7
ms.sourcegitcommit: 485ffaedb1ade71490f11cf05962add1718945cc
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/16/2019
ms.locfileid: "72430531"
---
# <a name="how-to-enable-and-disable-edit-and-continue-c-vb-c"></a>如何：启用和禁用“编辑并继续”（C#、VB、C++）

设计时，可以在 Visual Studio“选项”对话框中禁用或启用“编辑并继续” 。 “编辑并继续”仅在调试版本中起作用。 有关详细信息，请参阅[编辑并继续](../debugger/edit-and-continue.md)。

对于本机 C++，“编辑并继续”需要使用 `/INCREMENTAL` 选项。 有关 C++ 中的功能要求的详细信息，请参阅此[博客文章](https://devblogs.microsoft.com/cppblog/c-edit-and-continue-in-visual-studio-2015-update-3/)和[编辑并继续 (C++)](../debugger/edit-and-continue-visual-cpp.md)。

**启用或禁用“编辑并继续”：**

1. 如果正在进行调试会话，请停止调试（“调试” > “停止调试”或按 Shift+F5）   。

1. 在“工具” > “选项” >（或“调试” > “选项”）>“调试” > “常规”中，选择右窗格中的“编辑并继续”。

    > [!NOTE]
    > 如果启用了 IntelliTrace 并且收集 IntelliTrace 事件和调用信息，则会禁用“编辑并继续”。 有关详细信息，请参阅 [IntelliTrace](../debugger/intellitrace.md)。

1. 对于 C++ 代码，请确保选择“启用本机‘编辑并继续’”，并设置其他选项：
    - **继续应用更改（仅限本机）**

      如果选择，则在从中断状态继续调试时，Visual Studio 会自动编译并应用代码更改。 否则，可以选择使用“调试” > “应用代码更改”来应用更改。

    - **警告过时代码（仅限本机）**

      如果选择，则提供有关陈旧代码的警告。

1. 单击 **“确定”** 。
