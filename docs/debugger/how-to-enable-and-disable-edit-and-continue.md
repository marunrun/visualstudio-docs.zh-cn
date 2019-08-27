---
title: 如何：启用和禁用编辑并继续 |Microsoft Docs
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
ms.openlocfilehash: 3bee60a54576ab816c63cf60f2226ebbbaf50c44
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63388483"
---
# <a name="how-to-enable-and-disable-edit-and-continue-c-vb-c"></a>如何：启用和禁用编辑并继续 (C#，VB， C++)

您可以禁用或启用**编辑并继续**在 Visual Studio**选项**在设计时对话框。 “编辑并继续”仅在调试版本中起作用。 有关详细信息，请参阅[编辑并继续](../debugger/edit-and-continue.md)。

有关本机C++，**编辑并继续**需要使用`/INCREMENTAL`选项。 有关详细信息中的功能要求C++，请参阅此[博客文章](https://devblogs.microsoft.com/cppblog/c-edit-and-continue-in-visual-studio-2015-update-3/)并[编辑并继续 (Visual C++)](../debugger/edit-and-continue-visual-cpp.md)。

**若要启用或禁用编辑并继续：**

1. 如果您在调试会话中，停止调试 (**调试** > **停止调试**或**Shift**+**F5**).

1. 在中**工具** > **选项**> (或**调试** > **选项**) >**调试** > **常规**，选择**编辑并继续**右窗格中。

    > [!NOTE]
    > 如果启用了 IntelliTrace 并且收集 IntelliTrace 事件和调用信息，则会禁用“编辑并继续”。 有关详细信息，请参阅[IntelliTrace](../debugger/intellitrace.md)。

1. 有关C++代码，请确保**启用本机编辑并继续**选择，并设置其他选项：
    - **继续应用更改（仅限本机）**

      如果选中，Visual Studio 将自动编译并继续调试从中断状态时应用代码更改。 否则，你可以选择将应用使用的更改**调试** > **应用代码更改**。

    - **警告过时代码（仅限本机）**

      如果选择，提供了关于陈旧代码警告。

1. 单击 **“确定”**。
