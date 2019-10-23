---
title: 更改启动体验
ms.date: 02/01/2017
ms.topic: conceptual
f1_keywords:
- vs.ToolsOptionsPages.Startup
helpviewer_keywords:
- Start Page [Visual Studio]
- customizing Start Page [Visual Studio]
- Visual Studio Start Page
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b0a415c8a61e360ed1bcc323214d4144b2875cc0
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72652541"
---
# <a name="customize-startup"></a>自定义启动

可以通过几种不同的方式自定义 Visual Studio 的启动体验，例如打开最新的解决方案或仅打开空的开发环境。

::: moniker range="vs-2017"

你也可以显示自定义起始页，此起始页是在工具窗口中运行的 Windows Presentation Foundation (WPF) XAML 页，并且可以运行 Visual Studio 的内部命令。

::: moniker-end

## <a name="to-change-the-startup-item"></a>更改启动项

1. 在菜单栏上，依次选择“工具” > “选项”   。

2. 展开“环境”  ，然后选择“启动”  。

::: moniker range="vs-2017"

3. 在“启动时”  列表中，选择在 Visual Studio 启动后要显示的项目。

::: moniker-end

::: moniker range=">=vs-2019"

3. 在“启动时打开”列表中，选择要在 Visual Studio 启动后执行的操作  。 可以从“开始窗口”（这允许打开新的或现有项目）、“最新解决方案”或“空环境”中选择    。

::: moniker-end

::: moniker range="vs-2017"

## <a name="to-show-a-custom-start-page"></a>显示自定义起始页

可以使用 Visual Studio SDK [创建自己的自定义起始页](../extensibility/creating-a-custom-start-page.md)，或使用其他人已创建的其中一个起始页。 例如，可以在 [Visual Studio Marketplace](https://marketplace.visualstudio.com/search?target=VS&category=Tools&vsVersion=&subCategory=Start%20Pages&sortBy=Downloads) 中查找自定义起始页。

若要安装自定义起始页，请打开 .vsix 文件，或复制起始页文件并将其粘贴到计算机上的 %USERPROFILE%\Documents\Visual Studio 2017\StartPages 文件夹   。

### <a name="to-select-which-custom-start-page-to-display"></a>选择要显示的自定义起始页

1. 在菜单栏上，依次选择“工具”>“选项”   。

1. 展开“环境”  ，然后选择“启动”  。

1. 在“自定义起始页”  列表中，选择所需的页。

> [!TIP]
> 如果自定义起始页中的错误导致 Visual Studio 崩溃，则可以在安全模式下打开 Visual Studio，然后将其设置为使用默认起始页。 请参阅 [/SafeMode (devenv.exe)](../ide/reference/safemode-devenv-exe.md)。

## <a name="see-also"></a>请参阅

- [个性化设置 Visual Studio IDE](../ide/personalizing-the-visual-studio-ide.md)

::: moniker-end