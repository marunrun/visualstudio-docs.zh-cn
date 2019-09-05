---
title: 使用任务列表
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- TaskListWindow
- VS.TaskList
- tasklist
helpviewer_keywords:
- task list
- Visual Studio, task list
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ffbe1b7f293bc525aa03a536c0fa4fa55ce3e82a
ms.sourcegitcommit: 3cda0d58c5cf1985122b8977b33a171c7359f324
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2019
ms.locfileid: "70154859"
---
# <a name="use-the-task-list"></a>使用任务列表

使用“任务列表”  跟踪使用 `TODO` 和 `HACK` 或自定义令牌等令牌的代码注释，还能管理直接导向代码中的预定义位置的快捷方式。 单击列表中的项以转到其在源代码中的位置。

> [!NOTE]
> 本主题适用于 Visual Studio  Windows 版。 对于 Visual Studio for Mac，请参阅[任务注释 (Visual Studio for Mac)](/visualstudio/mac/task-comments)。

## <a name="the-task-list-window"></a>“任务列表”窗口

当“任务列表”  打开后，它将显示在应用程序窗口的底部。

若要打开“任务列表”  ，请选择“视图”   > “任务列表”  ，或从键盘按 Ctrl  +\\  、T  。

![“任务列表”窗口](../ide/media/vs2015_task_list.png)

要更改列表的排序顺序，请选择任意列的标头。 若要进一步优化搜索结果，请按住 Shift  键单击另一个列标头。 另一种方法是，在快捷菜单上选择“排序方式”  ，然后选择一个标头。 若要进一步优化搜索结果，请按住 Shift  并选择另一个标头。

要显示或隐藏列，在快捷菜单上选择“显示列”  。 选择要显示或隐藏的列。

要更改列的顺序，请将任意列标头拖动到所需的位置。

## <a name="user-tasks"></a>用户任务

Visual Studio 2015 中已删除用户任务功能。 若打开的解决方案具有 Visual Studio 2013 和更早版本的用户任务数据，.suo  文件中的用户任务数据不会受到影响，但用户任务不会显示在任务列表中。

如果想要继续访问和更新用户任务数据，应在 Visual Studio 2013 中打开项目，并将任何用户任务的内容复制到首选项目管理工具（如 Team Foundation Server）中。

## <a name="tokens-and-comments"></a>令牌和注释

 “任务列表”中还将显示注释标记后的代码注释和预定义的令牌。 例如，以下 C# 注释包含三个不同的部分：

- 注释标记 (`//`)

- 令牌，例如 (`TODO`)

- 注释（其余文本）

```csharp
// TODO: Load state from previously suspended application
```

因为 `TODO` 是预定义令牌，该注释将在列表中显示为 `TODO` 任务。

> [!NOTE]
> 默认令牌仅适用于 C/C++、C# 和 VB 语言。 对于其他语言，请参阅**自定义令牌**部分。

### <a name="custom-tokens"></a>自定义令牌

默认情况下，Visual Studio 包含以下令牌：`HACK`、`TODO`、`UNDONE` 和 `UnresolvedMergeConflict`。 令牌不区分大小写。 你也可以创建自己的自定义令牌。

创建自定义令牌：

1. 在 **“工具”** 菜单上，选择 **“选项”** 。

2. 打开 **“环境”** 文件夹，然后选择 **“任务列表”** 。

   将显示[“任务列表”选项页](../ide/reference/task-list-environment-options-dialog-box.md)。

   ![Visual Studio 任务列表](../ide/media/vs2015_task_list_options.png)

3. 在  “名称”  文本框中，输入令牌名称，如“BUG”。

4. 在 **“优先级别”** 下拉列表中，为新令牌选择默认优先级别。

5. 选择“添加”  。

> [!TIP]
> 输入名称后将启用  “添加”按钮。 必须先输入名称，然后再单击“添加”  。

### <a name="c-todo-comments"></a>C++ TODO 注释

默认情况下，C++ TODO 注释显示在“任务列表”  中。

要关闭 C++ TODO 命令，在“工具”  菜单上，依次选择“选项”   > “文本编辑器”   > “C/C++”   > “视图”   > “枚举注释任务”  ，然后将值设置为 false  。

## <a name="shortcuts"></a>快捷方式

快捷方式  是在“任务列表”  中跟踪的代码中的书签。 它具有与常规书签不同的图标。 双击  “任务列表”中的快捷方式可转到代码中的对应位置。

![Visual Studio 任务列表快捷方式图标](../ide/media/vs2015_task_list_bookmark.png)

### <a name="create-a-shortcut"></a>创建快捷方式

若要创建快捷方式，请将指针插入到代码中你想要放置快捷方式的位置。 选择“编辑” > “书签” > “添加任务列表快捷方式”或按 Ctrl+K，Ctrl+H        。

若要在代码中浏览快捷方式，在列表中选择一个快捷方式，然后从快捷菜单中选择“下一任务”  或“上一任务”  。

## <a name="see-also"></a>请参阅

- [“选项”对话框 ->“环境”->“任务列表”](../ide/reference/task-list-environment-options-dialog-box.md)
- [任务注释 (Visual Studio for Mac)](/visualstudio/mac/task-comments)
