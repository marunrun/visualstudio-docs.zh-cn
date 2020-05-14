---
title: 在 Visual Studio 和 Blend for Visual Studio 中设计 XAML
titleSuffix: ''
ms.date: 02/28/2020
ms.topic: conceptual
ms.assetid: 288e2415-9fcf-408e-bc35-9848315e14fd
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.openlocfilehash: eb18a2face5d9f1831bec35379a423f272c3e6ce
ms.sourcegitcommit: ade07bd1cf69b8b494d171ae648cfdd54f7800d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "82921363"
---
# <a name="design-xaml-in-visual-studio-and-blend-for-visual-studio"></a>在 Visual Studio 和 Blend for Visual Studio 中设计 XAML

Visual Studio 和 Blend for Visual Studio 两者都是可视化工具，用于使用 XAML 针对各种应用类型构建具有吸引力的用户界面和丰富的媒体体验。 两个集成开发环境 (IDE) 共享一组常见功能，包括 Visual XAML 编辑器（设计器）。 支持 WPF 和 UWP 平台的 Blend for Visual Studio 提供用于设计可视状态和创建动画的其他工具。

可以在 Visual Studio 与 Blend for Visual Studio 之间来回切换，甚至可以同时在两个 IDE 中打开同一个项目。 在一个 IDE 中保存到 XAML 文件的更改可以在你切换到另一个 IDE 时，通过自动重载进行应用。 可以通过在任一 IDE 中导航到 "**工具** > " "**选项** > " "**环境** > **文档**" 来控制重载行为。

## <a name="installation"></a>安装

- 若要创建 WPF 应用，请安装 Visual Studio 中的“.NET 桌面开发”工作负载****。 还会安装 Blend for Visual Studio。

     ![Visual Studio 安装程序中的 .NET 桌面开发工作负载的屏幕截图](../xaml-tools/media/dotnet-desktop-dev-workload.png)

- 若要创建 UWP 应用，请安装 Visual Studio 中的“通用 Windows 平台开发”工作负载****。 还会安装 Blend for Visual Studio。

     ![Visual Studio 安装程序的通用 Windows 平台开发工作负载的屏幕截图](../xaml-tools/media/uwp-workload.png)

- 若要创建 Xamarin.Forms 应用，请安装 Visual Studio 中的“使用 .NET 的移动开发”**** 工作负载。 ** 未安装 Blend for Visual Studio；Blend 不支持 Xamarin.Forms 应用。

     ![Visual Studio 安装程序中的 .NET 工作负载的移动开发屏幕截图](../xaml-tools/media/mobile-dev-dotnet-workload.png)

## <a name="shared-capabilities"></a>共享功能

对于最基本的开发任务，Visual Studio 和 Blend for Visual Studio 共享一组相同的窗口和功能（其中有一些细微的差异）。 部分亮点包括：

- **IntelliSense：** 这两个 Ide 都支持 IntelliSense 功能，如语句完成。

- **调试：** 你可以在[Visual Studio](inspect-xaml-properties-while-debugging.md)中进行调试并[Blend for Visual Studio](../xaml-tools/debug-xaml-in-blend.md)，包括在代码中设置断点以调试正在运行的应用程序，并在应用程序运行时使用[热重载](../xaml-tools/xaml-hot-reload.md)来更改 XAML 代码。 为了保持与 Visual Studio 一致的调试体验，Blend for Visual Studio 包含 Visual Studio 的大多数调试窗口和工具栏。

- **文件重新加载：** 可在 Visual Studio 或 Blend for Visual Studio 中编辑 XAML 文件。 在 IDE 之间切换时，将自动重载已保存的编辑文件。 可以通过在任一 IDE 中导航到 "**工具** > " "**选项** > " "**环境** > **文档**" 来控制重载行为。

- **同步的布局和设置：** 当你用同一个性化帐户登录时，将在你的设备和版本中为 Visual Studio 或 Blend for Visual Studio 设计自定义工具窗口布局和设置首选项。 请参见[跨多台计算机同步设置](../ide/synchronized-settings-in-visual-studio.md)。

## <a name="advanced-capabilities-in-blend-for-visual-studio"></a>Blend for Visual Studio 中的高级功能

若要提高工作效率，请考虑对以下任务使用 Blend for Visual Studio。 Blend for Visual Studio 在这些领域中可提供比单独 Visual Studio 设计器或代码更多的功能。

| 任务 | Visual Studio | Blend for Visual Studio | 更多信息 |
| - | - | - | - |
| **设计可视状态** | 没有可帮助你设计可视状态的工具；必须以编程方式创建它们。 | 使用设计工具可基于其状态更改控件的外观。 | [可视状态](modify-the-style-of-objects-in-blend.md#visual-states) |
| **创建动画** |没有用于动画的设计工具；必须以编程方式创建它们。 这需要对 WPF 中的动画和时间系统的了解以及丰富的编码专业知识。|可直观地创建动画，并且可以在 Blend for Visual Studio 中预览它们。 这比采用代码构建动画更快且更精确。 可以添加触发器以处理用户交互，并且可以切换到代码以添加事件处理程序和其他功能。|[动态显示对象](../xaml-tools/animate-objects-in-xaml-designer.md)|
|**将形状和文本转换为路径以便更容易地操作**|不支持。|可以通过将形状（如矩形和椭圆）转换为路径（这样可提供更好的编辑控制）来对形状进行细微或显著的更改。 可以重新调整路径形状或合并路径，以及从多个形状创建复合路径。<br /><br />还可以将文本块转换为路径以便将它们作为矢量图像进行操作。|[绘制形状和路径](../xaml-tools/draw-shapes-and-paths.md)|
|**编辑控件、模板和样式**|需要 WPF 样式和模板方面的编码和知识。|将任何图像转换为控件。<br /><br />使用模板编辑工具，只需少量鼠标单击便可对控件、样式和模板进行更改。<br /><br />例如，可以使用 Blend for Visual Studio 样式资源实现常用 WPF 控件（如按钮、列表框、滚动条、菜单等）并直接在 Blend for Visual Studio 中更改其颜色、样式或基础模板。 如果需要，随后可以切换到代码以完成收尾工作。|[修改对象样式](modify-the-style-of-objects-in-blend.md)|
|**将 UI 界面连接到数据**|可以从资源（如 SQL Server 数据库、WCF 或 Web 服务、对象或 SharePoint 列表）创建数据源，然后将数据源绑定到 UI 控件。<br /><br />必须手动创建设计时数据来获得交互设计体验。|对于 .NET Framework 应用，可轻松地为原型制作和测试创建示例数据。 在准备就绪时切换到实时数据。<br /><br />Blend for Visual Studio 的数据生成功能十分出色（可以轻松地动态添加名称、数字、URL 和照片），可以节省大量时间。<br /><br />对于实时数据，可以将 UI 控件绑定到 XML 文件或任何 CLR 数据源。|[显示数据](display-data-in-blend.md)|

有关高级 XAML 设计的详细信息，请参阅[使用 Blend for Visual Studio 创建 UI](../xaml-tools/creating-a-ui-by-using-blend-for-visual-studio.md)。

## <a name="see-also"></a>另请参阅

- [XAML 概述](xaml-overview.md)
- [Blend for Visual Studio 概述](creating-a-ui-by-using-blend-for-visual-studio.md)
