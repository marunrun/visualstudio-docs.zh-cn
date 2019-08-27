---
title: 使用任务列表 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
f1_keywords:
- TaskListWindow
- VS.TaskList
- tasklist
helpviewer_keywords:
- task list
- Visual Studio, task list
ms.assetid: f46a75a8-47b3-4cb6-bb59-b72e3356a664
caps.latest.revision: 33
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 9c9526b2deaafb36e991afce6d29ace47f8564ba
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68179347"
---
# <a name="using-the-task-list"></a>使用任务列表
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

使用“任务列表”  跟踪使用 `TODO` 和 `HACK`或自定义令牌等令牌的代码注释，还能管理直接导向代码中的预定义位置的快捷方式。 单击列表中的项以转到其在源代码中的位置。  
  
 本主题内容：  
  
- [“任务列表”窗口](../ide/using-the-task-list.md#taskListWindow)  
  
- [用户任务](../ide/using-the-task-list.md#userTasks)  
  
- [令牌和注释](../ide/using-the-task-list.md#tokensComments)  
  
- [自定义令牌](../ide/using-the-task-list.md#customTokens)  
  
- [C++ TODO 注释](../ide/using-the-task-list.md#cppComments)  
  
- [快捷方式](../ide/using-the-task-list.md#shortcuts)  
  
## <a name="taskListWindow"></a> “任务列表”窗口  
 当“任务列表”  打开后，它将显示在应用程序窗口的底部。  
  
#### <a name="to-open-the-task-list"></a>打开“任务列表”  
  
- 在“视图”  菜单中，选择“任务列表”  （键盘：Ctrl+\\、T）。  
  
     ![“任务列表”窗口](../ide/media/vs2015-task-list.png "vs2015_task_list")  
  
#### <a name="to-change-the-sort-order-of-the-list"></a>更改列表的排序顺序  
  
- 单击任意列的标头。 若要进一步优化搜索结果，请按住 Shift 键单击另一个列标头。  
  
     另一种方法是，在快捷菜单上选择 **“排序方式”** ，然后选择一个标头。 若要进一步优化搜索结果，请按住 Shift 键选择另一个标头。  
  
#### <a name="to-show-or-hide-columns"></a>显示或隐藏列  
  
- 在快捷菜单上选择 **“显示列”** 。 选择你要显示或隐藏的列。  
  
#### <a name="to-change-the-order-of-the-columns"></a>更改列的顺序  
  
- 将任意列标头拖动到所需的位置。  
  
## <a name="userTasks"></a> 用户任务  
 已在 Visual Studio 2015 中删除用户任务功能。 当你打开的解决方案具有 Visual Studio 2013 和早期的 Visual Studio 2015 中的用户任务数据时，将不影响 .suo 文件中的用户任务数据，但用户任务不会显示在任务列表中。  
  
 如果想要继续访问和更新你的用户任务数据，应在 Visual Studio 2013 中打开项目，并将任何用户任务的内容复制到你的首选项目管理工具（如 Team Foundation Server）中。  
  
## <a name="tokensComments"></a> 令牌和注释  
 **“任务列表”** 窗口中还将显示注释标记后的代码注释和预定义的令牌。 例如，以下 C# 注释包含三个不同的部分：  
  
- 注释标记 (`//`)  
  
- 令牌，例如 (`TODO`)  
  
- 注释（其余文本）  
  
```  
// TODO: Load state from previously suspended application  
```  
  
 因为 `TODO` 是预定义令牌，该注释将在列表中显示为 `TODO` 任务。  
  
### <a name="customTokens"></a> 自定义令牌  
 默认情况下，Visual Studio 包含以下令牌：HACK、TODO、UNDONE、NOTE。 它们不区分大小写。  
  
 你也可以创建自己的自定义令牌。  
  
##### <a name="to-create-a-custom-token"></a>创建自定义令牌  
  
1. 在 **“工具”** 菜单上，选择 **“选项”** 。  
  
2. 打开 **“环境”** 文件夹，然后选择 **“任务列表”** 。  
  
     此时将显示[“选项”对话框 ->“环境”->“任务列表”](../ide/reference/task-list-environment-options-dialog-box.md)。  
  
     ![Visual Studio 任务列表](../ide/media/vs2015-task-list-options.png "vs2015_task_list_options")  
  
3. 在“令牌”  类别中的“名称”  文本框中，输入你的令牌名称，如“BUG”。  
  
4. 在 **“优先级别”** 下拉列表中，为新令牌选择默认优先级别。 选择 **“添加”** 按钮。  
  
### <a name="cppComments"></a> C++ TODO 注释  
 默认情况下，C++ TODO 注释显示在“任务列表”  窗口中。 你可以更改这一行为。  
  
##### <a name="to-turn-off-c-todo-comments"></a>关闭 C++ TODO 注释  
  
1. 在“工具”  菜单上，转到“选项”|“文本编辑器”|“C/C++”|“视图”|“枚举注释任务”  ，并将值设置为 false。  
  
2. 在 **“选项”** 对话框中，打开 **“文本编辑器”** 。  
  
3. 在“C/C++”  下，选择“查看”  ，然后将“枚举注释任务”  设置为“False”  。  
  
## <a name="shortcuts"></a> 快捷方式  
 “快捷方式”  是代码中的书签，在“任务列表”  中跟踪；它具有与常规书签不同的图标。 双击 **“任务列表”** 中的快捷方式可转到代码中的对应位置。  
  
 ![Visual Studio 任务列表快捷方式图标](../ide/media/vs2015-task-list-bookmark.png "vs2015_task_list_bookmark")  
  
#### <a name="to-create-a-shortcut"></a>创建快捷方式  
  
- 将指针插入到代码中你想要放置快捷方式的位置。 选择“编辑”|“书签”|“添加任务列表快捷方式”  或按（键盘：Ctrl+K、Ctrl+H）。  
  
     若要在代码中浏览快捷方式，在列表中选择一个快捷方式，然后从快捷菜单中选择“下一任务”  或“上一任务”  。  
  
## <a name="see-also"></a>另请参阅  
 [“选项”对话框 ->“环境”->“任务列表”](../ide/reference/task-list-environment-options-dialog-box.md)
