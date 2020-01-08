---
title: 优化启动时间
ms.date: 11/15/2017
ms.topic: conceptual
helpviewer_keywords:
- startup time [Visual Studio]
- optimizing performance [Visual Studio]
- speed up start time [Visual Studio]
ms.assetid: d1508121-8499-4084-8eb5-fa89fa7b17d3
author: TerryGLee
ms.author: tglee
manager: jillfra
f1_keywords:
- vs.performancecenter
ms.workload:
- multiple
ms.openlocfilehash: 4824939b4ef3ed1bc7fa48b2508fc891c984a3c5
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75585777"
---
# <a name="optimize-visual-studio-startup-time"></a>优化 Visual Studio 启动时间

Visual Studio 可快速高效地启动。 但是，某些 Visual Studio 扩展和工具窗口加载时会对启动时间产生不利影响。 可在“管理 Visual Studio 性能”对话框中控制慢速扩展和工具窗口的行为  。 有关提升性能的更多提示，请参阅 [Visual Studio 性能提示和技巧](../ide/visual-studio-performance-tips-and-tricks.md)。

## <a name="startup-behavior"></a>启动行为

为了避免启动时间延长，Visual Studio 使用按需方法加载扩展  。 该行为意味着不会在 Visual Studio 启动后立即打开扩展，而是根据需要打开。 此外，由于在之前的 Visual Studio 会话中保持工具窗口的打开状态会使启动时间变慢，因此 Visual Studio 以更智能的方式打开工具窗口，从而避免影响启动时间。

如果 Visual Studio 检测到启动速度较慢，则会弹出一条消息，提示你导致速度变慢的扩展或工具窗口。 此消息提供了指向“管理 Visual Studio 性能”对话框的链接  。 还可以通过在菜单栏中选择“帮助” > “管理 Visual Studio 性能”，访问此对话框   。

![“管理 Visual Studio 性能”- 弹出窗口显示“我们注意到扩展 ... 正在拖慢 Visual Studio”](../ide/media/vside_perfdialog_popup.png)

该对话框会列出影响启动性能的扩展和工具窗口。 可更改扩展和工具窗口的设置以提高启动性能。

## <a name="a-nameextensions-to-change-extension-settings-to-improve-startup-solution-load-and-typing-performance"></a><a name="extensions" />更改扩展设置以改善启动、解决方案加载和键入性能

1. 通过在菜单栏上选择“帮助” > “管理 Visual Studio 性能”，打开“管理 Visual Studio 性能”对话框    。

    如果某个扩展使 Visual Studio 的启动、解决方案加载或键入变慢，此扩展将显示在“扩展” > “启动”（或“解决方案加载”或“键入”）下的“管理 Visual Studio 性能”对话框中      。

    ![管理 Visual Studio 性能 - 扩展视图](../ide/media/vside_perfdialog_extensions.png)

2. 选择想要禁用的扩展，然后选择“禁用”按钮  。

可以始终使用“扩展管理器”  或“管理 Visual Studio 性能”  对话框重新启用扩展，以用于以后的会话。

## <a name="a-nametool-windows-to-change-tool-window-settings-to-improve-startup-time"></a><a name="tool-windows" />更改工具窗口设置以改善启动时间

1. 通过在菜单栏上选择“帮助” > “管理 Visual Studio 性能”，打开“管理 Visual Studio 性能”对话框    。

    如果某个工具窗口使 Visual Studio 启动变慢，此工具窗口将显示在“工具窗口” > “启动”下的“管理 Visual Studio 性能”对话框中    。

2. 选择想要更改其行为的工具窗口。

3. 选择下列三个选项的其中一个：

   - **使用默认行为：** 工具窗口默认行为。 选中此项将不会提升启动性能。

   - **启动时不显示窗口：** 打开 Visual Studio 时，指定的工具窗口将始终关闭，即使它在上一个会话中保留打开状态。 需要时可以从相应的菜单中打开工具窗口。

   - **启动时自动隐藏窗口：** 如果工具窗口在上一个会话中保留打开状态，则此选项将在启动时折叠工具窗口组，以避免初始化工具窗口。 如果经常使用工具窗口，那么这是一个不错的选择。 因为工具窗口仍然可用，但不会再对 Visual Studio 启动时间产生负面影响。

     ![管理 Visual Studio 性能 - 工具窗口视图](../ide/media/vside_perfdialog_toolwindows.png)

> [!NOTE]
> Visual Studio 2017 的某些早期版本中提供一种名为“轻型解决方案加载”  的功能。 在当前版本中，包含托管代码的大型解决方案的加载速度比以前快许多，即使在不具备轻型解决方案加载功能的情况下亦如此。

## <a name="see-also"></a>请参阅

- [优化 Visual Studio 性能](../ide/optimize-visual-studio-performance.md)
- [Visual Studio 性能提示和技巧](../ide/visual-studio-performance-tips-and-tricks.md)
- [Visual Studio blog - Load solutions faster with Visual Studio 2017 version 15.6](https://devblogs.microsoft.com/visualstudio/load-solutions-faster-with-visual-studio-2017-version-15-6/)（Visual Studio 博客 - 使用 Visual Studio 2017 版本 15.6 更快地加载解决方案）
