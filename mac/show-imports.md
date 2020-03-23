---
title: 显示导入项
description: 使用“显示导入项”展开 Visual Studio for Mac 中的 IntelliSense。
author: cobey
ms.author: cobey
ms.date: 03/29/2019
ms.assetid: C7782BF3-016F-4B41-8A81-85FC540A1A8F
ms.custom: video
ms.openlocfilehash: 964fbbf2f46e2495184b01c47cba888a93f24ea8
ms.sourcegitcommit: 2975d722a6d6e45f7887b05e9b526e91cffb0bcf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/20/2020
ms.locfileid: "75439102"
---
# <a name="show-import-items"></a>显示导入项

Visual Studio for Mac 会在 IntelliSense 完成列表中显示所有可用类型，即使它们未导入到项目中也是如此。 通过选择未导入的项，将向源文件添加正确的 `using` 语句。

![“显示导入项”概述](media/importitems-overview.gif)

## <a name="how-to-enable"></a>如何启用

若要启用此功能，请通过“Visual Studio”  **“首选项”**  > 打开“首选项”  并导航到“文本编辑器”   > “IntelliSense”  。 选中“显示导入项”  复选框，以在 IntelliSense 中启用其他项。

![“显示导入项”选项](media/show-import-items.png)

## <a name="usage"></a>使用情况

一旦启用“显示导入项”  ，使用该功能导入项目的过程与 IntelliSense 内的正常操作类似。 键入代码时，有效项将填充完成列表。 这包括尚未导入的项。 未导入的项将在项右侧显示其完整的命名空间，从而使你能够查看要传入到项目中的导入。

![“显示导入项”列表](media/show-import-items-list.png)

在 IntelliSense 列表中，命名空间显示在 `using` 语句当前未引用的成员的旁边。 如果从列表中选择其中一个项，则会将该成员添加到你的代码，并  将 `using` 语句添加到文件的顶部。 编码中已引用的类型成员将不会在 IntelliSense 中显示其命名空间。

## <a name="see-also"></a>另请参阅

- [快速操作（Windows 上的 Visual Studio）](/visualstudio/ide/quick-actions)
- [重构代码（Windows 上的 Visual Studio）](/visualstudio/ide/refactoring-in-visual-studio)
