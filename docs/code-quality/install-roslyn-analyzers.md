---
title: 安装 Roslyn 分析器
ms.date: 08/03/2018
ms.topic: conceptual
helpviewer_keywords:
- code analysis, managed code
- analyzers
- Roslyn analyzers
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 9013d7be60a8091f7ce4fc4fe92fa4acaef43720
ms.sourcegitcommit: f9f389e72787de30eb869a55ef7725a10a4011f0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/06/2019
ms.locfileid: "73636526"
---
# <a name="install-net-compiler-platform-code-analyzers"></a>安装 .NET Compiler Platform 代码分析器

Visual Studio 包含一组核心的 .NET Compiler Platform （*Roslyn*）分析器。 这些分析器始终打开。 可以将其他分析器安装为 NuGet 包，或者安装为*VSIX*文件中的 Visual Studio 扩展。

## <a name="to-install-nuget-analyzer-packages"></a>安装 NuGet 分析器包

1. 查找要安装在 www.nuget.org 上的分析器包。

   例如，你可能需要[安装 Microsoft FxCop 分析器](install-fxcop-analyzers.md#nuget-package)来检查代码中是否存在安全问题和性能问题。 或者，安装[StyleCop](https://www.nuget.org/packages/stylecop.analyzers/)以在代码库中查找样式问题。

2. 使用[包管理器控制台](/nuget/quickstart/install-and-use-a-package-in-visual-studio#package-manager-console)或[包管理器 UI](/nuget/quickstart/install-and-use-a-package-in-visual-studio#package-manager-console)，在 Visual Studio 中安装包。

   > [!NOTE]
   > 每个分析器包的 "www.nuget.org" 页将显示要粘贴到**包管理器控制台**中的命令。 还有一个用于将文本复制到剪贴板的方便的按钮。

   分析器程序集安装并显示在 "**引用** > **分析器**" 下**解决方案资源管理器**中。

## <a name="to-install-vsix-analyzers"></a>安装 VSIX 分析器

::: moniker range="vs-2017"

1. 在 Visual Studio 中，选择 "**工具**" > "**扩展和更新**"。

   此时，“扩展和更新”对话框打开。

   > [!NOTE]
   > 另外，还可以从[Visual Studio Marketplace](https://marketplace.visualstudio.com)中直接查找并下载分析器扩展。

::: moniker-end

::: moniker range=">=vs-2019"

1. 在 Visual Studio 中，选择 "**扩展**" > "**管理扩展**"。

   此时将打开 "**管理扩展**" 对话框。

   > [!NOTE]
   > 另外，还可以从[Visual Studio Marketplace](https://marketplace.visualstudio.com)中直接查找并下载分析器扩展。

::: moniker-end

2. 在左窗格中展开 "**联机**"，然后选择 " **Visual Studio Marketplace**"。

3. 在 "搜索" 框中，键入要安装的分析器扩展的名称。 例如，你可能需要[安装 Microsoft FxCop 分析器](install-fxcop-analyzers.md#vsix)来检查代码中是否存在安全问题和性能问题。

4. 选择 "**下载**"。

   此扩展已下载。

5. 选择 **"确定"** 关闭对话框，然后关闭 Visual Studio 的所有实例以启动**VSIX 安装程序**。

   此时将打开 " **VSIX 安装程序**" 对话框。

   ![适用于 Microsoft 代码分析的 VSIX 安装程序](media/vsix-installer-code-analysis.png)

6. 选择 "**修改**" 以启动安装。

7. 一分钟或两分钟后，安装完成。 选择“关闭”。

8. 重新打开 Visual Studio。

::: moniker range="vs-2017"

如果要检查是否安装了该扩展，请选择 "**工具**"  >  "**扩展和更新**"。 在 "**扩展和更新**" 对话框中，选择左侧的 "**已安装**" 类别，然后按名称搜索扩展。

::: moniker-end

::: moniker range=">=vs-2019"

如果要检查是否安装了扩展，请选择 "**扩展**"  >  "**管理扩展**"。 在 "**管理扩展**" 对话框中，选择左侧的 "**已安装**" 类别，然后按名称搜索扩展。

::: moniker-end

## <a name="next-steps"></a>后续步骤

> [!div class="nextstepaction"]
> [在 Visual Studio 中使用代码分析器](../code-quality/use-roslyn-analyzers.md)

## <a name="see-also"></a>请参阅

- [Visual Studio 中的代码分析器概述](../code-quality/roslyn-analyzers-overview.md)
- [安装 FxCop 分析器](../code-quality/install-fxcop-analyzers.md)
