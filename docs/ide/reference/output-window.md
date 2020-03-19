---
title: “输出”窗口
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.build.output
- vs.debug.output
- vs.output
helpviewer_keywords:
- Output window, about Output window
- Output window
- Toolbox, removing controls
ms.assetid: d8931d88-250e-4db4-963f-2c5b3e99b45f
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: be028af8ab9f458c1fadad6f8b2fcbd6aaa49a04
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "75567978"
---
# <a name="output-window"></a>“输出”窗口

“输出”  窗口在集成开发环境 (IDE) 中显示各种功能的状态消息。 若要打开“输出”  窗口，请选择“视图”   > “输出”  （或按 Ctrl  +Alt  +O  ）。

## <a name="toolbar"></a>ToolBar

以下控件显示在“输出”窗口的工具栏中  。

### <a name="show-output-from"></a>显示输出来源

显示一个或多个要查看的输出窗格。 可能有多个可用的信息窗格，具体取决于 IDE 中哪些工具使用了“输出”  窗口向用户传送消息。

### <a name="find-message-in-code"></a>在代码中查找消息

将代码编辑器中的插入点移动到包含选定生成错误的行。

### <a name="go-to-previous-message"></a>转到上一条消息

在“输出”  窗口中，将焦点更改到上一条生成错误，然后将代码编辑器中的插入点移动到包含该生成错误的行。

### <a name="go-to-next-message"></a>转到下一条消息

在“输出”  窗口中，将焦点更改到下一条生成错误，然后将代码编辑器中的插入点移动到包含该生成错误的行。

### <a name="clear-all"></a>全部清除

从“输出”  窗格清除所有文本。

### <a name="toggle-word-wrap"></a>切换自动换行

在“输出”  窗格中启用和禁用“自动换行”功能。 启用“自动换行”后，在下一行显示超出查看区域的较长条目中的文本。

## <a name="output-pane"></a>输出窗格

在“显示输出来源”  列表中选择的“输出”  窗格显示指定源的输出。

## <a name="route-messages-to-the-output-window"></a>将消息路由到“输出”窗口

若要在生成项目时显示“输出”  窗口，请在“选项”  对话框的“项目和解决方案”   > “常规”  页上，选择“在生成开始时显示输出窗口”  。 然后，打开要编辑的代码文件，在“输出”  窗口工具栏上选择“转到下一条消息”  和“转到上一条消息”  ，选择“输出”  窗格中的条目。 执行此操作时，代码编辑器中的插入点会跳转到出现所选问题的代码行。

在[命令窗口](../../ide/reference/command-window.md)中调用的某些 IDE 功能和命令会将其输出传送到“输出”  窗口。     在[管理外部工具中](../../ide/managing-external-tools.md)选择“使用输出窗口”选项时，外部工具的输出（如 .bat 和 .com 文件，通常显示在命令窗口中）会路由到“输出”窗格。 许多其他类型的消息也可以显示在“输出”  窗格中。 例如，根据目标数据库检查存储过程中的 Transact-SQL 语法时，检查结果将显示在“输出”  窗口中。

也可以编写自己的应用程序，使其在运行时向“输出”  窗格写入诊断消息。 要执行此操作，请在 .NET API 的 <xref:System.Diagnostics.Debug> 命名空间中使用 <xref:System.Diagnostics.Trace> 类或 <xref:System.Diagnostics> 类的成员。 生成解决方案或项目的“调试”配置时，<xref:System.Diagnostics.Debug> 类的成员显示输出；生成“调试”或“发布”配置时，<xref:System.Diagnostics.Trace> 类的成员显示输出。 有关详细信息，请参阅[“输出”窗口中的诊断消息](../../debugger/diagnostic-messages-in-the-output-window.md)。

在 C++ 中，可创建自定义生成步骤和生成事件，“输出”窗格中对其警告和错误在进行显示和计数  。 在输出行按 F1，可以显示相应的帮助主题  。 有关详细信息，请参阅[设置自定义生成步骤输出的格式](/cpp/build/formatting-the-output-of-a-custom-build-step-or-build-event)。

## <a name="scroll-behavior"></a>滚动行为

如果在“输出”窗口中使用自动滚动，随后使用鼠标或箭头键进行导航，则自动滚动停止  。 若要恢复自动滚动，请按 Ctrl  +End  。

## <a name="see-also"></a>另请参阅

- [“输出”窗口中的诊断消息](../../debugger/diagnostic-messages-in-the-output-window.md)
- [如何：控制“输出”窗口](https://msdn.microsoft.com/Library/91aebd15-8854-4a7a-9f7d-57376fb4e858)
- [编译和生成](../../ide/compiling-and-building-in-visual-studio.md)
- [了解生成配置](../../ide/understanding-build-configurations.md)
- [类库概述](/dotnet/standard/class-library-overview)
