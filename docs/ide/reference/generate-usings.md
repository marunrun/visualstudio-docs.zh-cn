---
title: 生成 using
ms.date: 03/10/2020
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- dotnet
helpviewer_keywords:
- add missing usings
ms.openlocfilehash: 903b160bac0e8096062e09fd78ff4c92c46cf8ee
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "79094319"
---
# <a name="add-missing-usings-in-visual-studio"></a>在 Visual Studio 中添加缺少的 usings

此代码生成适用于：

- C#

- Visual Basic

**功能：** 可以立即添加复制和粘贴代码的必要导入或 [using 指令](/dotnet/csharp/language-reference/keywords/using-directive)。

**使用时机：** 通常的做法是从项目或其他源中的不同位置复制代码并将其粘贴到新代码中。 此快速操作找到复制和粘贴代码的缺少导入指令，然后提示添加它们。 此代码修补程序还可以添加从项目到项目的引用。

操作原因：  由于此快速操作自动添加必要导入，因此不必手动复制代码所需的 `using` 语句。

## <a name="add-missing-usings-refactoring"></a>添加缺少的 usings 重构

1. 复制来自文件的代码并将其粘贴到新代码中，无需包括必要的 `using` 指令。 生成的错误会伴随一个代码修补程序出现，该修补程序可添加缺少的 `using` 指令。

    > [!NOTE]
    > 需要在“工具”>“选项”>“文本编辑器”>“C#”>“高级”>“使用指令”  中启用此建议。

2. 选择 Ctrl+。 打开“快速操作和重构”菜单  。

    ![生成 using](media/generate-using-codefix.png)

3. 选择 **using \<your reference\>;** 以添加缺少的引用。

    ![生成 using 结果](media/generate-using-result.png)

## <a name="see-also"></a>请参阅

- [代码生成](../code-generation-in-visual-studio.md)
- [预览更改](../../ide/preview-changes.md)
- [针对 .NET 开发人员的提示](../csharp-developer-productivity.md)
