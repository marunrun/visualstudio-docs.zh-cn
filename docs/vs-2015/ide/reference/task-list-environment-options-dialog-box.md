---
title: “选项”对话框 ->“环境”->“任务列表” | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Environment.Task_List
- VS.ToolsOptionsPag.Environment.Task_List
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
caps.latest.revision: 20
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 72e5f82fa3ca4b7ca909ee07e5b77a31b3e20879
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "72650965"
---
# <a name="task-list-environment-options-dialog-box"></a>“选项”对话框 ->“环境”->“任务列表”
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

该选项页允许添加、删除和更改生成“任务列表”提醒的注释标记  。 要显示这些设置，请从“工具”菜单选择“选项”，展开“环境”文件夹，然后选择“任务列表”     。

## <a name="task-list-options"></a>任务列表选项
 确认在选中时删除任务时，每当从 **任务列表**中删除用户任务时都会显示一个消息框，从而允许您确认删除。 默认情况下选择此选项。

> [!NOTE]
> 若要删除任务注释，使用该链接查找注释，然后将其从你的代码中删除。

 仅显示文件名在选中后，**任务列表**的**文件**列只显示要编辑的文件的名称，而不是其完整路径。

## <a name="tokens"></a>令牌
 将注释插入代码（其文本以“标记列表”中的某个标记开头）中时，“任务列表”会在该文件每次打开以进行编辑时，将注释显示为新项********。 可以单击此“任务列表”项以直接跳转到代码中的注释行****。 有关详细信息，请参阅[使用任务列表](../../ide/using-the-task-list.md)。

 令牌列表显示令牌列表，并允许您添加或删除自定义令牌。 注释标记在 Visual C# 和 Visual C++ 中要区分大小写，但在 Visual Basic 中不区分大小写。

> [!NOTE]
> 如果未按标记在“标记列表”中显示的样子键入所需标记，那么注释任务不会在“任务列表”中显示********。

 优先级设置使用所选标记的任务的优先级。 将在“任务列表”中为以此标记开头的任务注释自动分配指定的优先级****。

 名称输入令牌字符串。 这一操作会启用“添加”按钮****。 在“添加”按钮上，此字符串包含在“标记列表”中，而以此名称开头的注释将显示在“任务列表”中************。

 输入新 **名称**时，添加 "已启用"。 单击可使用在“名称”和“优先级”字段中输入的值添加新的标记字符串   。

 删除单击此选项可从 **令牌列表**中删除所选令牌。 无法删除默认注释标记。

 更改单击此项可使用在 " **名称** " 和 " **优先级** " 字段中输入的值更改现有标记。

> [!NOTE]
> 无法重命名或删除默认注释标记，但可以更改其优先级别。

## <a name="see-also"></a>另请参阅
 [使用](../../ide/using-the-task-list.md)在 "代码[环境选项" 对话框](../../ide/reference/environment-options-dialog-box.md)[中设置书签](../../ide/setting-bookmarks-in-code.md)任务列表
