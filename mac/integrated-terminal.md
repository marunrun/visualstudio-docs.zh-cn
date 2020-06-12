---
title: Visual Studio for Mac - 集成终端
description: Visual Studio for Mac 提供用于在 macOS 上生成 .NET 应用程序的集成开发环境，包括 ASP.NET Core 网站和适用于 iOS、Android、Mac 和 Xamarin.Forms 的 Xamarin 项目。
author: jmatthiesen
ms.author: jomatthi
ms.date: 05/14/2020
ms.assetid: EFD53CE9-8174-4FE4-8863-2984D22FD921
ms.openlocfilehash: d362938e8f0075591ea5d4ed8461d11395680b5c
ms.sourcegitcommit: d20ce855461c240ac5eee0fcfe373f166b4a04a9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2020
ms.locfileid: "84185673"
---
# <a name="integrated-terminal"></a>集成终端
在 Visual Studio for Mac 中，可以打开一个集成终端窗口，该终端最初从解决方案的根目录启动。 终端适用于不同类型的情况，包括运行前端任务（例如：npm、ng 或 vue）、管理容器、运行高级 git 命令、执行实体框架命令、查看 dotnet CLI 输出、添加 NuGet 包等。 

打开终端：
- 使用 Ctrl+` 键盘快捷方式显示或隐藏终端窗口。
- 使用“视图”\>“板”\>“终端”菜单  。
- 使用搜索栏中的“终端”命令。

![Visual Studio for Mac 集成终端在启动后立即运行。](media/integrated-terminal-intro.png)

默认情况下，终端启动后会执行以下操作：
- 将工作目录设置为当前解决方案的路径。
- 加载默认的系统 shell。

## <a name="search"></a>搜索
可以使用“搜索”>“查找…”菜单来搜索终端窗口的内容。

![Visual Studio for Mac 集成终端中的搜索体验](media/integrated-terminal-search.png)

## <a name="terminal-keyboard-shortcuts"></a>终端键盘快捷方式
|命令|键盘快捷键|
|-|-|
|显示/隐藏终端窗口|**Ctrl+`**|
|创建新的终端实例|**Ctrl+'**|
|向上滚动页面|PgUp|
|向下滚动页面|PgDn|
|浏览之前使用的命令|**↑**、**↓**|
|增大字号|**⌘+**|
|减小字号|**⌘-**|

## <a name="multiple-instances"></a>多个实例
可能会随时运行多个终端实例。 你可以使用 Ctrl+' 键盘快捷方式创建新的实例。 可以切换实例，操作方法是：单击每个实例的选项卡，或者使用 Ctrl+tab 快捷方式打开窗口选取器对话框。

![Visual Studio for Mac 中的多个终端实例](media/integrated-terminal-multiple-instances.png) 

## <a name="customizing-the-terminal-window"></a>自定义终端窗口
### <a name="configuring-the-terminal-font"></a>配置终端字体
可以在“首选项”>“环境”>“字体”窗格中更改终端内容的字体和字号。 默认情况下，终端内容的字体将与输出板内容相同，都为 Menlo Regular，字号为 11。 可以将其设置为与编辑器字体不同的任何字体。

![自定义集成终端的字体设置](media/integrated-terminal-change-font.png)

### <a name="reusing-system-terminal-customizations"></a>重复使用系统终端自定义项
集成终端使用与 macOS 系统终端相同的默认值和配置。 这意味着，你的终端自定义项（zsh、oh-my-zsh 等）也可在集成终端使用。
