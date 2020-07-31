---
title: 针对未导入类型和扩展方法的 IntelliSense 完成
description: 如何使用 `using` 指令将 IntelliSense 完成用于尚未导入的类型和扩展方法。
ms.date: 07/27/2020
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- dotnet
ms.openlocfilehash: d6112bc3894424b9dfd3d060ed390960243b0f98
ms.sourcegitcommit: 4a77403b6bd33c5a6e66a3eefd42c81c39fb67ca
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/28/2020
ms.locfileid: "87330994"
---
# <a name="intellisense-completion-for-unimported-types-and-extension-methods"></a>针对未导入类型和扩展方法的 IntelliSense 完成

此重构适用于：

- C#

- Visual Basic

**功能：** IntelliSense 提供针对未导入类型和扩展方法的完成功能。

**使用时机：** 想要使用已在项目中有依赖项的类型或扩展方法，但尚未将 using 语句添加到文件。 

操作原因：无需手动将 using 语句添加到文件。

## <a name="how-to"></a>操作说明

1. 开始键入在项目中有依赖项的类型或扩展方法的名称后，IntelliSense 将为你提供建议。 来自未导入的命名空间的项会将其包含的命名空间显示为后缀。

   > [!TIP]
   > 你可以根据需要使用显示在完成列表左下角的“扩展器按钮(Alt + A)”来显示/隐藏来自未导入的命名空间的项。 要更改默认行为，请转到“工具” > “选项” > “文本编辑器” > “C#” / “Basic” > “IntelliSense”，并查找“显示来自未导入的命名空间的项”      。

2. 选择并提交未导入的项。 

   Using 语句将自动添加到文件中。

   ![针对未导入类型的 IntelliSense 完成](media/intellisense-completion-unimported-types.png)

## <a name="see-also"></a>请参阅

- [IntelliSense](../using-intellisense.md)
- [重构](../refactoring-in-visual-studio.md)
