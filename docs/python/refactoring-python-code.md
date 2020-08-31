---
title: 重构 Python 代码
description: Visual Studio 通过重命名标识符、提取方法、添加导入和移除未使用的导入使重构 Python 代码变得容易。
ms.date: 03/13/2019
ms.topic: how-to
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.custom: seodec18
ms.workload:
- python
- data-science
ms.openlocfilehash: be93ac7b8bc0659da522abcf6000d97ec05d46b9
ms.sourcegitcommit: a801ca3269274ce1de4f6b2c3f40b58bbaa3f460
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "88801329"
---
# <a name="refactor-python-code"></a>重构 Python 代码

Visual Studio 提供用于自动转换和清理 Python 源代码的多个命令：

- [重命名](#rename)：可重命名所选类、方法或变量名称
- [提取方法](#extract-method)：根据所选代码创建新的方法
- [添加导入](#add-import)：提供添加缺少导入的智能标记
- [删除未使用的导入](#remove-unused-imports)：删除未使用的导入

## <a name="rename"></a>重命名

1. 右键单击想要重命名的标识符，然后选择“重命名”  ，或将光标置于标识符上，然后选择“编辑”   > “重构”   > “重命名”  菜单命令 (F2  )。
2. 在出现的“重命名”  对话框中，为标识符输入新名并选择“确定”  ：

   ![新标识符名称的重命名提示](media/code-refactor-rename-1.png)

3. 在下一个对话框中，选择代码中想要向其应用重命名的文件和实例；选择任何单个实例可预览特定更改：

   ![用于选择应用更改位置的重命名对话框](media/code-refactor-rename-2.png)

4. 选择“应用”  对源代码文件进行更改。 （此操作无法撤消。）

## <a name="extract-method"></a>提取方法

1. 选择多行代码或表达式以提取到单独的方法中。
2. 选择“编辑”   > “重构”   > “提取方法”  菜单命令或键入 Ctrl  +R   > M  。
3. 在出现的对话框中，输入新的方法名称，指示将其提取到的位置，然后选择任何闭包变量。 闭包未选择的变量将返回到方法参数中：

   ![“提取方法”对话框](media/code-refactor-extract-method-1.png)

4. 选择“确定”  ，然后代码将进行相应修改：

   ![提取方法的影响](media/code-refactor-extract-method-2.png)

## <a name="add-import"></a>添加导入

将光标放在缺少类型信息的标识符上时，Visual Studio 将提供一个智能标记（代码左侧的灯泡图标），该标记的命令将添加必需的 `import` 或 `from ... import` 语句：

![添加导入智能标记](media/code-refactor-add-import-1.png)

Visual Studio 为当前项目和标准库中的顶级包和模块提供 `import` 完成。 Visual Studio 还为子模块和子包及模块成员提供 `from ... import` 完成。 此完成包括函数、类或导出的数据。 选择任一选项将在其他导入后向文件顶部添加语句，或者在已导入相同模块时，向现有 `from ... import` 语句添加语句。

![添加导入的结果](media/code-refactor-add-import-2.png)

Visual Studio 尝试筛选出实际未在模块中定义的成员，例如导入其他模块但不属于执行导入操作的模块的子级的模块。 例如，许多模块使用 `import sys` 而不是 `from xyz import sys`，因此不会看到从其他模块导入 `sys` 的完成，即使模块缺少可排除 `sys` 的 `__all__` 成员。

同样，Visual Studio 将筛选从其他模块或内置命名空间导入的函数。 例如，如果某个模块从 `sys` 模块导入 `settrace` 函数，从理论上讲，可以从该模块导入它。 但最好直接使用 `import settrace from sys`，以便 Visual Studio 专门提供该语句。

最后，如果按常规排除某些内容，但该内容具有将包括的其他值（例如，由于名称分配有模块中的值），Visual Studio 仍将排除该导入。 此行为假定不应导出该值，因为它在其他模块重定义，因此其他分配也可能为不会导出的虚拟值。

## <a name="remove-unused-imports"></a>删除未使用的导入

编写代码时，可对根本未使用的模块使用 `import` 语句结尾。 因为 Visual Studio 可对代码进行分析，因此它可自动确定是否需要 `import` 语句，方法是查看所导入名称在出现语句的位置下方是否被使用。

在编辑器中右键单击任意位置，然后选择“删除导入”，这将为你提供从“所有范围”或仅“当前范围”中删除的选项：

![删除导入菜单](media/code-refactor-remove-imports-1.png)

Visual Studio 然后将对代码进行相应更改：

![删除导入的影响](media/code-refactor-remove-imports-2.png)

请注意，Visual Studio 不考虑控制流；在 `import` 语句前使用某个名称，该名称将被视为实际已使用。 Visual Studio 还会忽略所有 `from __future__` 导入、在类定义中执行的导入以及来自 `from ... import *` 语句中的导入。
