---
title: 在项目中包括 NuGet 包
description: 本文档介绍如何在 Xamarin 项目中包括 NuGet 包。 文档将介绍如何查找和下载包，同时介绍 IDE 集成功能。
author: conceptdev
ms.author: crdun
ms.date: 04/14/2017
ms.assetid: 5C800815-0B13-4B27-B017-95FCEF1A0EA2
ms.custom: video
ms.openlocfilehash: 9e4699a1d4e2826cad205ce89ab46812cd5c4b2d
ms.sourcegitcommit: 7fbfb2a1d43ce72545096c635df2b04496b0be71
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/09/2019
ms.locfileid: "67692803"
---
# <a name="include-a-nuget-package-in-your-project"></a>在项目中包括 NuGet 包

NuGet 是用于 .NET 开发最常用的程序包管理器，内置在 Visual Studio for Mac 和 Visual Studio on Windows 中。 可以使用任一 IDE 搜索包并将包添加到 Xamarin.iOS 和 Xamarin.Android 项目。

本文介绍如何在项目中包括 NuGet 包并演示实现此流程无缝的工具链。

## <a name="nuget-in-visual-studio-for-mac"></a>Visual Studio for Mac 中的 NuGet

为了演示 NuGet 包的功能，我们将首先介绍如何创建新应用程序并向其添加一个包。 然后我们将讨论用于帮助管理包的 IDE 功能。

## <a name="create-a-new-project"></a>创建新项目

首先，创建一个名为 `HelloNuget` 的项目，如下所示。 虽然本示例演示的是 iOS 单一视图应用程序模板，但也可以使用任何支持的项目类型：

![新建 iOS 项目](media/nuget-walkthrough-NewProject.png)

## <a name="adding-a-package"></a>添加包

对于 Visual Studio for Mac 中打开的项目，右键单击“Solution Pad”中的“包”文件夹并选择“添加包”    ：

![添加新的 NuGet 包上下文操作](media/nuget-walkthrough-PackagesMenu.png)

此操作将启动“添加包”窗口  。 请确保将源下拉列表设置为 `nuget.org`：

![源下拉列表](media/nuget-walkthrough-Source.png)

打开窗口时，将从默认包源 nuget.org 中加载包列表。初始结果应如下所示：

![列出 NuGet 包](media/nuget-walkthrough-AddPackages1.png)

使用右上角的搜索框查找特定的包，如 `azure`。 找到希望使用的包时，请选择它并单击“添加包”按钮以开始安装  。

[添加 Azure NuGet 包](media/nuget-walkthrough-AddPackages2.png)

包下载完毕后会添加到项目中。 解决方案会发生以下更改：

* “引用”节点包含属于 NuGet 包的所有程序集列表  。
* “包”节点显示每个已下载的 NuGet 包  。 可以更新该列表中的包，或从列表中删除包。
* “packages.config”文件将添加到此项目  。 IDE 使用此 XML 文件跟踪该项目中引用的包版本。 不应手动编辑此文件，而是应将其保存在版本控制中。 请注意，可以使用 project.json 文件，而不是 packages.config 文件。 project.json 文件是通过 NuGet 3 引入的新的包文件格式，支持可传递还原。 有关 project.json 的详细信息，请参阅 [NuGet 文档](https://docs.microsoft.com/NuGet/Schema/Project-Json)。 需要手动添加 project.json 文件，关闭项目并重新打开后才能在 Visual Studio for Mac 中使用 project.json 文件。

## <a name="using-nuget-packages"></a>使用 NuGet 包

添加 NuGet 包并更新项目引用后，可以如针对任何项目引用一样根据 API 对其进行编程。

请确保将任何所需的 `using` 指令添加到文件顶部：

```csharp
using Newtonsoft.Json;
```

大多数 NuGet 提供其他信息，如“自述文件”或连接到 NuGet 源的“项目”页链接。 通常可以在“添加包”页面的包简介中找到连接到该内容的链接：

[查看项目页链接](media/nuget-walkthrough-project-page.png)

<a name="Package_Updates" class="injected"></a>

## <a name="package-updates"></a>包更新

通过右键单击“包”节点可以一次性完成所有包更新，也可以在每个组件上单独进行包更新  。

右键单击“包”以访问上下文菜单： 

![包菜单](media/nuget-walkthrough-PackagesMenu.png)

* 添加包  - 打开窗口，将更多包添加到项目。
* 更新  - 检查每个包的源服务器并下载任何更新版本。
* 还原  - 下载任何缺少的包（无需将现有包升级到更新版本）。

现在也提供解决方案级别的“更新”和“还原”选项，这些选项可影响该解决方案中的所有项目。

也可以右键单击单个包访问上下文菜单：

![包菜单](media/nuget-walkthrough-PackageMenu.png)

* 版本号  - 版本号是禁用的菜单项 - 仅用于提供信息。
* 更新  - 检查源服务器并下载更新版本（如果存在）。
* 删除  - 从此项目中删除包，并从项目引用中删除相关的程序集。

## <a name="adding-package-sources"></a>添加包源

最初从 nuget.org 检索安装包。然而，可以将其他包位置添加到 Visual Studio for Mac。 这有助于测试自己正在开发的 NuGet 包，或有助于使用公司或组织内的专用 NuGet 服务器。

在 Visual Studio for Mac 中，导航到“Visual Studio”>“首选项”>“NuGet”>“源”，查看和编辑包源的列表  。 请注意，源可以是（由 URL 指定的）远程服务器或本地目录。

![包源](media/nuget-walkthrough-PackageSource.png)

单击“添加”设置新源  。 向包源输入友好名称和 URL（或文件路径）。 如果源是安全的 Web 服务器，则同时输入用户名和密码，否则请将这些条目留空：

![添加包源](media/nuget-walkthrough-PackageSource2.png)

搜索包时可以选择不同的源：

![添加包源](media/nuget-walkthrough-PackageSource3.png)

## <a name="version-control"></a>版本控制

NuGet 文档讨论了[在不将包提交到源控件的情况下使用 NuGet](/nuget/consume-packages/packages-and-source-control)。 如果不希望将二进制文件和未使用信息存储到源代码管理中，可以将 Visual Studio for Mac 配置为自动从服务器还原包。 这意味着当开发人员首次从源代码管理检索项目时，Visual Studio for Mac 将自动下载安装所需的包。

![自动还原包](media/nuget-walkthrough-AutoRestore.png)

有关如何使 `packages` 目录不受跟踪的详细信息，请参阅特定的源控件文档。

## <a name="related-video"></a>相关视频

> [!Video https://channel9.msdn.com/Shows/Visual-Studio-Toolbox/Visual-Studio-for-Mac-Using-NuGet/player]

## <a name="see-also"></a>请参阅

* [在 Visual Studio 中安装和使用包 (Windows)](/nuget/quickstart/install-and-use-a-package-in-visual-studio)
