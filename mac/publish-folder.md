---
title: 发布到文件夹
ms.date: 04/02/2019
helpviewer_keywords:
- deployment, website, console, publish
ms.assetid: e963fb4b-6d32-4d45-86bb-ef7e4d3028b0
author: sayedihashimi
ms.author: sayedha
manager: unniravindranathan
ms.prod: visual-studio-mac
ms.topic: how-to
ms.openlocfilehash: ab461327a0af5d072689e4a5cb357525b42018ba
ms.sourcegitcommit: 5335a9864d5747bc917ed28d4ebeade3076b10e7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2020
ms.locfileid: "85950481"
---
# <a name="publish-to-a-folder-using-visual-studio-for-mac"></a>使用 Visual Studio for Mac 发布到文件夹

可使用“发布”工具将 .NET Core 控制台或 ASP.NET Core 应用发布到文件夹。

## <a name="prerequisites"></a>先决条件

- 已安装 [Visual Studio 2019 for Mac](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs4mac2019)，并启用了 .NET Core。
- .NET Core 控制台或 ASP.NET Core 项目。 如果还没有项目，则可以[创建一个新的项目](/visualstudio/mac/create-new-projects?view=vsmac-2019)。

## <a name="publish-to-folder"></a>发布到文件夹

使用 Visual Studio for Mac 通过“发布”工具可以将 .NET Core 项目发布到文件夹。 将文件发布到文件夹后，可以将它们传输到其他环境。 若要发布到文件夹，请执行以下步骤。

 1. 在 Solution Pad 中，右键单击项目，选择“发布”  。

    ![“发布”上下文菜单](media/publish-context-menu.png)

 2. 如果之前已发布此项目，则在菜单中将看到发布配置文件。 选择该发布配置文件以启动发布过程。

 3. 若要首次将此项目发布到文件夹，请选择“发布到文件夹” 

    ![“发布到文件夹”上下文菜单](media/publish-to-folder-context-menu.png)

 4. “发布到文件夹”对话框出现  。 在此对话框可以自定义将在其中发布项目的文件夹。 可以使用“浏览”按钮执行此操作，也可以粘贴某个路径  。

 5. 单击“发布”后，系统会发生一些事件  。 首先是创建发布配置文件。 发布配置文件是在发布过程中导入项目的 MSBuild 文件。 它包含在发布过程中使用的属性。 这些文件存储在 `Properties/PublishProfiles` 中并具有扩展名 `.pubxml`。 接下来是启动发布过程。 你可以通过查看 Visual Studio for Mac 中的状态栏监视进度。

    ![显示发布状态的 IDE 状态栏](media/publish-to-folder-status-bar.png)

 6. 发布成功完成后，查找器窗口将打开进入发布文件夹。 现在已创建发布配置文件，它将显示在“发布”上下文菜单中。

    ![具有文件夹配置文件的“发布”上下文菜单](media/publish-context-menu-with-folder-profile.png)

 7. 若要再次使用相同的设置发布项目，则可以单击“发布”上下文菜单中的配置文件。

## <a name="customize-publish-options"></a>自定义发布选项

若要更改发布配置文件的名称（显示在“发布”上下文菜单中），请重命名发布配置文件。 切勿更改文件扩展名 (`.pubxml`)。

若要更改发布文件夹路径，请打开发布配置文件并编辑 `publishUrl` 值。

若要更改使用的生成配置，请更改发布配置文件中的 `LastUsedBuildConfiguration` 属性。
