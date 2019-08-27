---
title: 查看类型定义
ms.date: 01/10/2018
ms.topic: conceptual
helpviewer_keywords:
- code editor, view definition
- go to definition
- peek definition
- type definition [Visual Studio]
- member definition [Visual Studio]
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2c5235bc19c1b06ec2cae26e3fcffb6a7d061c9b
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62549744"
---
# <a name="view-type-and-member-definitions"></a>查看类型和成员定义

开发人员经常需要查看他们在代码中所使用的类型或类成员的源代码定义。 在 Visual Studio 中，“转到定义”和“速览定义”功能有助于轻松查看类型或成员的定义。 如果源代码不可用，则改为显示元数据。

## <a name="go-to-definition"></a>转到定义

“转到定义”功能可导航到类型或成员的源，并且在新选项卡中打开结果。如果使用键盘，请将文本游标放置在符号名称内部的某个位置，然后按 F12。 如果使用鼠标，请选择右键单击菜单中的“转到定义”，或使用以下部分中描述的“Ctrl + 单击”功能。

### <a name="ctrl-click-go-to-definition"></a>Ctrl + 单击转到定义

“Ctrl”+“单击”是鼠标用户快速访问“转到定义”的快捷方式。 按 Ctrl 并将鼠标悬停在类型或成员上，符号变为可单击。 要快速导航到某个符号的定义，按 Ctrl 键然后单击该符号。 就这么简单！

![鼠标单击转到定义动画](../ide/media/click_gotodef.gif)

转到“工具” > “选项” > “文本编辑器” > “常规”，然后从“使用修改键”下拉列表中选择“Alt”或“Ctrl”+“Alt”，可以更改鼠标单击“转到定义”的修改键+。 取消选中“启用鼠标单击以执行转到定义”复选框还可以禁用鼠标单击转到定义。

![启用鼠标单击转到定义](../ide/media/editor_options_mouse_click_gotodef.png)

## <a name="peek-definition"></a>查看定义

“速览定义”功能有助于预览类型的定义，无需离开编辑器中的当前位置。 如果使用键盘，请将文本游标放置在类型或成员名称内的某个地方，然后按 Alt + F12。 如果使用鼠标，可以选择右键单击菜单中的“速览定义”。

要启用“Ctrl”+“单击”功能，请转到“工具” > “选项” > “文本编辑器” > “常规”。 选择“在速览视图中打开定义”选项然后单击“确定”关闭“选项”对话框。

![设置鼠标单击速览定义选项](../ide/media/editor_options_peek_view.png)

然后，按 Ctrl（或在“选项”中选中的任意一个修改键），然后单击类型或成员。

![速览定义动画](../ide/media/peek_definition.gif)

如果在弹出式窗口中查看另一个定义，则启动痕迹路径，可以使用弹出式窗口上方显示的圆形菜单和箭头进行导航。

有关详细信息，请参阅[如何：使用“查看定义”(Alt+F12) 查看和编辑代码](how-to-view-and-edit-code-by-using-peek-definition-alt-plus-f12.md)。

## <a name="view-metadata-as-source-code-c"></a>查看作为源代码的元数据 (C#)

查看 C# 类型或源代码不可用的成员的定义时，将改为显示其元数据。 可以看到类型和成员的声明，但不能看到其实现。

对源代码不可用的项运行“转到定义” 或“查看定义”命令时，“代码编辑器”中将显示一个选项卡式文档，该文档包含该项的元数据（以源代码形式显示）的视图。 该文档的选项卡上将显示类型的名称，并且后跟“[from metadata]” 。

例如，如果对 <xref:System.Console> 运行“转到定义”命令，则 <xref:System.Console> 的元数据将在“代码编辑器”中显示为 C# 源代码。 该代码与其声明类似，但不会显示一个实现。

![作为源代码的元数据](../ide/media/metadatasource.png)

> [!NOTE]
> 尝试对标记为内部的类型或成员运行“转到定义”或“查看定义”命令时，Visual Studio 不会将其元数据显示为源代码，无论引用程序集是否友好均是如此。

### <a name="view-decompiled-source-definitions-instead-of-metadata-c"></a>查看反编译源定义，而不是元数据 (C#)

在查看 C# 类型或源代码不可用的成员的定义时，可以设置选项以查看反编译源代码。 若要开启此功能，请从菜单栏中选择“工具” > “选项”。 然后，展开“文本编辑器” > “C#” > “高级”，并选择“启用导航到反编译源代码”。

![查看反编译定义](media/go-to-definition-decompiled-sources.png)

> [!NOTE]
> Visual Studio 使用 ILSpy 反编译重建方法体。 第一次访问此功能时，必须同意有关软件授权以及版权和商标法律的法律免责声明。

## <a name="see-also"></a>请参阅

- [导航代码](../ide/navigating-code.md)
- [如何：使用“查看定义”(Alt+F12) 查看和编辑代码](how-to-view-and-edit-code-by-using-peek-definition-alt-plus-f12.md)