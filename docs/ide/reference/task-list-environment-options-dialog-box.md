---
title: “选项”对话框 ->“环境”->“任务列表”
ms.date: 03/28/2019
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Environment.Task_List
- VS.ToolsOptionsPages.Environment.TaskList
- VS.Environment.Task List
helpviewer_keywords:
- Token List
- tokens
- icons, in Task List
- Task List, customizing environment
- Options dialog box, Task List environment
- exclamation points
- comments, comment tasks in Task List
- tokens, and the Task List
- Task List, comment tasks
ms.assetid: 88327e04-fa3e-48db-995b-ad89e0dc4ed2
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e28b3b9c3fe4d6e89228dc18ba8b98aa5e0d2e76
ms.sourcegitcommit: eeff6f675e7850e718911647343c5df642063d5e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2020
ms.locfileid: "80233131"
---
# <a name="options-dialog-box-environment--task-list"></a>“选项”对话框：环境 \> 任务列表

该选项页允许添加、删除和更改生成“任务列表”提醒的注释标记  。 要显示这些设置，请从“工具”菜单选择“选项”，展开“环境”文件夹，然后选择“任务列表”     。

## <a name="task-list-tokens"></a>任务列表标记

将注释插入代码（其文本以“标记列表”  中的某个标记开头）中时，“任务列表”  会在该文件每次打开以进行编辑时，将注释显示为新项。 单击“任务列表”  项以直接跳转到代码中的注释行。 有关详细信息，请参阅[使用任务列表](../../ide/using-the-task-list.md)。

标记列表\
显示标记列表，并允许你添加或删除自定义标记。 注释标记在 C# 和 C++ 中要区分大小写，但在 Visual Basic 中不区分大小写。

> [!NOTE]
> 如果未按标记在“标记列表”中显示的样子键入所需标记，那么注释任务不会在“任务列表”  中显示。

优先级\
设置使用所选标记（低、正常或高）的任务的优先级。 将在“任务列表”  中为以此标记开头的任务注释自动分配指定的优先级。

名称\
在此处输入标记字符串，然后单击“添加”  将字符串添加到标记列表。

添加\
输入新名称时将启用  。 单击可使用在“名称”和“优先级”字段中输入的值添加新的标记字符串   。

删除\
单击可从标记列表中删除选定标记。 无法删除默认注释标记。

更改\
单击可使用在“名称”和“优先级”字段中输入的值更改现有标记   。

> [!NOTE]
> 无法重命名或删除默认注释标记，但可以更改其优先级别。

## <a name="see-also"></a>请参阅

- [使用任务列表](../../ide/using-the-task-list.md)
- [在代码中设置书签](../../ide/setting-bookmarks-in-code.md)
