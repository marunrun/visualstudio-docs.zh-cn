---
title: 如何：还原隐藏的调试器命令 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
helpviewer_keywords:
- debugger, restoring commands
- debugging [Visual Studio], restoring commands
- commands, debugger
ms.assetid: 76ac9b77-f536-43b5-a9fc-984854b1c566
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a45791843abe3051bacb9655c773ac9dfc6b9045
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72732915"
---
# <a name="how-to-restore-hidden-debugger-commands"></a>如何：还原隐藏的调试器命令
安装 Visual Studio 时，系统会要求您为主要的编程语言选择一组默认的 IDE 设置。 某些语言的默认 IDE 设置可能会隐藏某些调试器命令。

 如果要使用由默认 IDE 设置隐藏的调试器功能，可以使用以下过程将相应的命令重新添加到菜单中。

### <a name="to-restore-hidden-debugger-commands"></a>还原隐藏的调试器命令

1. 在项目处于打开的状态下，在“工具”菜单上单击“自定义”。

2. 在“自定义”对话框中，单击“命令”选项卡。

3. 在“菜单栏:”下拉列表中，选择要包含已还原命令的“调试”菜单。

4. 单击“添加命令…”按钮。

5. 在“添加命令”框中，选择要添加的命令，然后单击“确定”。

6. 重复上面的步骤以添加其他命令。

7. 完成将命令添加到菜单后，单击“关闭”。

    > [!WARNING]
    > 某些菜单项仅在调试器处于特定模式（如运行模式或中断模式）下才显示。 因此，在完成这些步骤后，您所添加的项可能不会立即显示出来。

## <a name="restoring-commands-not-available-from-the-customize-dialog-box"></a>还原“自定义”对话框中不可用的命令
 某些命令（特别是分层菜单中的命令）无法从“自定义”对话框中还原。 要还原这些命令，必须导入一组新的 IDE 设置。

#### <a name="to-import-new-ide-settings"></a>导入新的 IDE 设置

1. 在“工具”菜单上，单击“导入和导出设置”。

2. 在“欢迎使用‘导入和导出设置向导’”页面上，单击“导入选定的环境设置”，然后单击“下一步”。

3. 在“保存当前设置”页面上，确定是否保存现有的设置，然后单击“下一步”。

4. 在“选择要导入的设置集合”页面上的“默认设置”文件夹下，选择一个包含要使用的命令的开发设置集合。 如果不知道应选择哪个集合，请尝试“常规开发设置”或“Visual C++ 开发设置”，这两个集合提供了大部分的调试器命令。

5. 单击 **“下一步”** 。

6. 在“选择要导入的设置”页面上的“选项”下，确保选中了“调试”。 清除其他复选框，除非还要导入这些复选框对应的设置。

7. 单击 **“完成”** 。

8. 在“导入完成”页面上，检查“详细信息”部分，查看是否有任何与重置您的设置相关联的错误。

9. 单击 **“关闭”** 。

## <a name="see-also"></a>请参阅
- [调试器安全](../debugger/debugger-security.md)
- [初探调试器](../debugger/debugger-feature-tour.md)