---
title: 自定义 IDE
description: 可以通过多种方式自定义 Visual Studio for Mac，因此用户可以在满足效率和美观需求的环境中开发应用。 本文将探讨调整 Visual Studio for Mac 的各种方式以满足你的需要。
author: heiligerdankgesang
ms.author: dominicn
ms.date: 11/06/2020
ms.assetid: F7C2A28C-0759-4E0D-A28E-B72D5AB73DB6
ms.custom: video
ms.openlocfilehash: 05fd1091a279a085c2a727eb36cbc56fcb201057
ms.sourcegitcommit: 2cf3a03044592367191b836b9d19028768141470
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/11/2020
ms.locfileid: "94493281"
---
# <a name="customizing-the-ide"></a>自定义 IDE

可以自定义 Visual Studio for Mac，因此用户可以在同时满足效率和美观需求的环境中开发应用。 本文将探讨调整 Visual Studio for Mac 的各种方式以满足你的需要。

## <a name="dark-theme"></a>深色主题

![深色主题视图](media/customizing-the-ide-image7a.png)

通过浏览到“Visual Studio”>“首选项”>“环境”>“视觉样式”并从“用户界面主题”下拉列表中选择所需主题，可以切换 Visual Studio for Mac 的主题，如下图中所示   ：

![深色主题选择](media/customizing-the-ide-image7b.png)

## <a name="localization"></a>本地化

Visual Studio for Mac 已采用以下 14 种语言进行本地化，便于更多开发人员使用：

* 简体中文 - 中国
* 繁体中文 - 中国台湾
* 捷克语
* 法语
* 德语
* 英语
* 意大利语
* 日语
* 韩语
* 波兰语
* 葡萄牙语 - 巴西
* 俄语
* 西班牙语
* 土耳其语

若要更改 Visual Studio for Mac 显示的语言，请浏览到“Visual Studio”>“首选项”>“环境”>“视觉样式”并从“用户界面语言”下拉列表中选择所需语言，如下图中所示   ：

![语言选择](media/customizing-the-ide-image11a.png)

## <a name="author-information"></a>创建者信息

在创建者信息面板中，可以添加你的相关信息，例如名字、电子邮件地址、作品的版权所有者、所在公司和商标：

![“编辑创建者信息”部分](media/customizing-the-ide-image9a.png)

此信息用于填充标准文件标头（如许可证），这些标头可能会添加到新文件中：

![“标准标头”选项](media/customizing-the-ide-image8a.png)

填充的“名称”  和“电子邮件”  字段用于通过 Visual Studio for Mac 的版本控制完成的任何提交。 若尚未填充这些字段，Visual Studio for Mac 将在你尝试使用版本控制时提示你进行此操作。

## <a name="key-bindings"></a>键绑定

通过键绑定或键盘快捷方式，可以调整开发环境，使得在 Visual Studio for Mac 中的移动更高效。 它为许多常用 IDE（如 Visual Studio (on Windows)、ReSharper、Visual Studio Code 和 Xcode）提供熟悉的键绑定。

通过浏览到“Visual Studio”>“首选项”>“环境”>“键绑定”可以设置键绑定，如下图中所示  ：

![设置键绑定](media/customizing-the-ide-image10a.png)

从此处可以搜索键绑定组合、查看冲突绑定、添加新绑定和编辑现有绑定。

也可以在 Visual Studio for Mac 的初始设置过程中通过“键盘选择”屏幕来设置这些绑定：

![第一次运行时设置键绑定](media/ide-tour-2019-keyboard-shortcut.png)

## <a name="workspace-layout"></a>工作区布局

Visual Studio for Mac 的工作区由主要文档区域（通常是编辑器、设计器图面或选项文件）组成，周围是包含用于访问和管理应用程序文件、测试和调试的有用信息的免费工具窗口。

 ![工作区布局](media/customizing-the-ide-image1a.png)

### <a name="viewing-and-arranging-tool-windows"></a>查看和排列工具窗口

在 Visual Studio for Mac 中打开任何新解决方案或文件时，应注意工作区中的一些工具窗口，包括解决方案窗口、文档大纲和错误：

![工具窗口](media/customizing-the-ide-image2a.png)

Visual Studio for Mac 提供包含其他信息、工具和导航帮助的工具窗口，通过浏览“视图”菜单项并选择一个工具窗口进行添加，可以访问所有这些窗口：

![选择新工具窗口](media/customizing-the-ide-image3a.png)

也可以通过各种命令自动打开工具窗口，例如“在文件中查找”(Shift + Cmd + F) 命令会打开搜索结果的独立窗口。

可以最有用的任何方式在工作流中移动和排列工具窗口。 例如，它们可以停靠在文档编辑器的任意一侧，可以与另一个工具窗口相邻，也可以在另一个窗口的上方或下方，或者作为一组选项卡式窗口，能够在窗口之间快速切换。

对于频繁使用的工具窗口，也可以将其从 Visual Studio for Mac 窗口完全拆离，并纳入到其自己的新窗口中。

工具窗口可通过每个窗口右上角的控件进行固定和关闭：

:::image type="content" source="media/customizing-the-ide-image5a.png" alt-text="使用控件固定或关闭工具窗口":::

固定的窗口会停靠在工作区侧面，并保持打开状态，以便在需要时可更快地进行访问。 取消固定的窗口会停靠但不会显示，直到使用鼠标将鼠标指针悬停在窗口的选项卡上方或使用键盘设置焦点；当鼠标和键盘焦点离开它们时，它们可以隐藏。

### <a name="organizing-layouts"></a>组织布局

随时都可以显示的工具窗口依赖于当前的上下文。 例如，当使用可视化设计器时，工具箱和属性网格窗口是最重要的；在调试时，能够使用调试器窗口查看堆栈和局部变量将十分有用。

打开工具窗口的状态由“布局”表示。 可以通过“视图”菜单手动切换布局，如下图中所示，或执行调试或打开 Storyboard 等操作时会自动切换布局：

![选择新的布局](media/customizing-the-ide-image6b.png)

可以使用“视图”>“布局”>“保存当前布局...”菜单项来创建新布局。 此命令会将当前布局添加到菜单，以供随时选择：

![保存当前布局](media/customizing-the-ide-image6a.png)

### <a name="side-by-side-editing-support"></a>并行编辑支持

通过 Visual Studio for Mac，可以并行打开文本编辑器，或让一个编辑器作为独立的浮动窗口。

通过选择“视图”>“编辑器列”>“2 列”，用“视图”菜单项启用 2 列模式，或通过将编辑器选项卡拖动到编辑器区域的一个边缘来启用该模式：

![2 列并行模式](media/customizing-the-ide-sbs.png)

可以将编辑器选项卡拖动到文档区域外，从而创建浮动编辑器窗口。 该浮动窗口也支持并行编辑器，并可以包含多个编辑器选项卡：

![创建新的窗口](media/customizing-the-ide-sbs1.png)

![与其他选项卡并行的 2 列](media/customizing-the-ide-sbs2.png)

若要还原单一的打开编辑器，请选择“视图”>“编辑器列”>“1 列”。

## <a name="related-video"></a>相关视频

> [!Video https://channel9.msdn.com/Shows/Visual-Studio-Toolbox/Visual-Studio-for-Mac-Customize-the-Look-and-Feel/player]

## <a name="see-also"></a>请参阅

- [个性化设置 Visual Studio IDE (Windows)](/visualstudio/ide/personalizing-the-visual-studio-ide)