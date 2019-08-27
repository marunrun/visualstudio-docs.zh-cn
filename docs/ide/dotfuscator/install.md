---
title: 安装 Dotfuscator Community
ms.date: 03/28/2019
ms.devlang: dotnet
ms.topic: conceptual
keywords: Dotfuscator, Dotfuscator Community, Dotfuscator CE, PreEmptive, PreEmptive Solutions, PreEmptive Protection, 保护, 社区版, 模糊处理, .NET, 免费, Visual Studio 2017, Visual Studio 2019, Visual Studio, 安装
helpviewer_keywords:
- PreEmptive Protection Dotfuscator
- Dotfuscator Community Edition
- Dotfuscator CE
- Dotfuscator Community
- Dotfuscator
- obfuscation
- protection
- Dotfuscator installer
- Dotfuscator setup
- install Dotfuscator
- installing Dotfuscator
- set up Dotfuscator
description: 了解如何安装 Visual Studio 中包含的免费 Dotfuscator Community 副本。
ms.assetid: f2146651-e24a-4e24-ade8-8ddee8ff4e43
author: Joe-Sewell-PreEmptive
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 0a6945713d86c510112992be3fefd2d41280ef14
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62557656"
---
# <a name="install-dotfuscator-community"></a>安装 Dotfuscator Community

Dotfuscator Community 现在是 Visual Studio 的可选组件。
这些说明解释了如何安装它。

> [!NOTE]
> 除了 Visual Studio 版本附带的 Dotfuscator Community 版本外，PreEmptive Solutions 还定期在其网站上提供更新的版本。
> 如果想要直接下载**最新版本**而非从 Visual Studio 中安装，请**[单击此处转到 Dotfuscator 下载页面][download]**。

## <a name="within-visual-studio"></a>在 Visual Studio 中

::: moniker range="vs-2019"

可从 Visual Studio IDE 中安装 Dotfuscator Community：

1. 在“搜索框” (Ctrl + Q) 中，键入 `dotfuscator`。 <br/> <br/> ![搜索框](media/install_in_vs19_12.png) <br/> <br/>

2. 在显示的搜索结果中的“组件”标题下，选择“安装 PreEmptive Protection - Dotfuscator”。
   * 如果“菜单”标题下显示的是“PreEmptive Protection - Dotfuscator Community”，则表示已经安装了 Dotfuscator Community。 选择该选项以[开始][get-started]。

3. “Visual Studio 安装程序”窗口将会启动，并为安装 Dotfuscator Community 进行预配置。
   > [!NOTE]
   > 可能需要提供管理员凭据才能继续。 

4. 在 Visual Studio 安装程序窗口中，单击“安装”。 <br/> <br/> ![单击“安装”](media/install_in_vs19_34.png) <br/> <br/>

::: moniker-end

::: moniker range="vs-2017"

可从 Visual Studio IDE 中安装 Dotfuscator Community：

1. 在“快速启动”(Ctrl+Q) 搜索栏中，键入 `dotfuscator`。 <br/> <br/> ![快速启动](media/install_from_vs_12.png) <br/> <br/>

2. 在显示的快速启动结果中的“安装”标题下，选择“PreEmptive Protection - Dotfuscator (各个组件)”。
   * 如果“菜单”标题下显示的是“工具”-“PreEmptive Protection - Dotfuscator”，则表示已经安装了 Dotfuscator CE。 选择该选项以[开始][get-started]。

3. “Visual Studio 安装程序”窗口将会启动，并为安装 Dotfuscator CE 进行预配置。
   > [!NOTE] 
   > 可能需要提供管理员凭据才能继续。

4. 在 Visual Studio 安装程序窗口中，单击“安装”。 <br/> <br/> ![单击“安装”](media/install_from_vs_345.png) <br/> <br/>

::: moniker-end

安装完成后即可[开始使用 Dotfuscator Community][get-started]。

## <a name="during-visual-studio-installation"></a>Visual Studio 安装过程

如果尚未安装 Visual Studio，可从 [Visual Studio 网站][vs-install]获取安装程序。
运行时，它会显示所选 Visual Studio 版本的安装选项。

::: moniker range="vs-2019"

![安装选项](media/install_ui.png)

::: moniker-end

::: moniker range="vs-2017"

![安装选项](media/install_ui_17.png)

::: moniker-end

然后可将 Dotfuscator Community 作为 Visual Studio 的单个组件进行安装：

1. 选择“各个组件”选项卡。
2. 在“代码工具”下，勾选“PreEmptive Protection - Dotfuscator”项。<br/> <br/> ![单个组件](media/install_individually_12.png) <br/> <br/>
3. “PreEmptive Protection - Dotfuscator”显示在“摘要”面板的“各个组件”部分下。 <br/> <br/> ![摘要窗格](media/install_individually_3.png) <br/> <br/>
4. 根据环境需要进一步配置任何安装设置。
5. 准备好安装 Visual Studio 后，单击“安装”按钮。

安装完成后即可开始使用 Dotfuscator Community。 有关详细信息，请参阅[完整 Dotfuscator Community 用户指南的“入门”页][get-started]。

## <a name="see-also"></a>请参阅

[完整 Dotfuscator Community 用户指南中的本主题](https://www.preemptive.com/dotfuscator/ce/docs/help/)

<!-- Copyright © 2019 PreEmptive Solutions, LLC -->

[vs-install]:  https://visualstudio.microsoft.com/downloads/
[get-started]:  https://www.preemptive.com/dotfuscator/ce/docs/help/gui_getstarted.html

[download]:  https://www.preemptive.com/products/dotfuscator/downloads

[full]:  https://www.preemptive.com/dotfuscator/ce/docs/help/intro_install.html