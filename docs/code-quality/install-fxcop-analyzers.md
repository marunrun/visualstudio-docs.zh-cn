---
title: 安装 FxCop 分析器
ms.date: 08/03/2018
ms.topic: conceptual
helpviewer_keywords:
- fxcop analyzers
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: b5cb0fa5985cbc923713330289d7f83ed1fd954e
ms.sourcegitcommit: 209ed0fcbb8daa1685e8d6b9a97f3857a4ce1152
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2019
ms.locfileid: "69551102"
---
# <a name="install-fxcop-analyzers-in-visual-studio"></a>在 Visual Studio 中安装 FxCop 分析器

Microsoft 创建了一组名为[CodeAnalysis](https://www.nuget.org/packages/Microsoft.CodeAnalysis.FxCopAnalyzers)的分析器, 其中包含来自旧分析的最重要的 "FxCop" 规则。 这些分析器检查代码中的安全性、性能和设计问题, 等等。

您可以将这些 FxCop 分析器作为 NuGet 包或 VSIX 扩展安装到 Visual Studio。 若要了解每个的优缺点, 请参阅[NuGet 包与VSIX 扩展](roslyn-analyzers-overview.md#nuget-package-versus-vsix-extension)。

## <a name="to-install-fxcop-analyzers-as-a-nuget-package"></a>将 FxCop 分析器安装为 NuGet 包

1. 根据你的 Visual Studio 版本确定要安装[的分析器包版本](#fxcopanalyzers-package-versions)。

2. 使用[包管理器控制台](/nuget/quickstart/install-and-use-a-package-in-visual-studio#package-manager-console)或[包管理器 UI](/nuget/quickstart/install-and-use-a-package-in-visual-studio#package-manager-console), 在 Visual Studio 中安装包。

   > [!NOTE]
   > 每个分析器包的 "nuget.org" 页将显示要粘贴到**包管理器控制台**中的命令。 还有一个用于将文本复制到剪贴板的方便的按钮。
   >
   > ![显示包管理器控制台命令的 NuGet.org 页面](media/nuget-package-manager-command.png)

   分析器程序集已安装, 它们显示在**引用** > **分析器**下**解决方案资源管理器**中。

   ![解决方案资源管理器中的分析器节点](media/solution-explorer-analyzers-node.png)

### <a name="fxcopanalyzers-package-versions"></a>FxCopAnalyzers 包版本

使用以下准则来确定要为你的 Visual Studio 版本安装的 FxCop 分析器包的版本:

| Visual Studio 版本 | FxCop 分析器包版本 |
| - | - |
| Visual Studio 2019 (所有版本)<br />Visual Studio 2017 版本15.8 及更高版本 | [2.9.3](https://www.nuget.org/packages/Microsoft.CodeAnalysis.FxCopAnalyzers/2.9.3) |
| Visual Studio 2017 版本15.5 到15。7 | [2.6.3](https://www.nuget.org/packages/Microsoft.CodeAnalysis.FxCopAnalyzers/2.6.3) |
| Visual Studio 2017 版本15.3 到15。4 | [2.3.0-beta1](https://www.nuget.org/packages/Microsoft.CodeAnalysis.FxCopAnalyzers/2.3.0-beta1) |
| Visual Studio 2017 版本15.0 到15。2 | [2.0.0-beta2](https://www.nuget.org/packages/Microsoft.CodeAnalysis.FxCopAnalyzers/2.0.0-beta2) |
| Visual Studio 2015 update 2 和3 | [1.2.0-beta2](https://www.nuget.org/packages/Microsoft.CodeAnalysis.FxCopAnalyzers/1.2.0-beta2) |
| Visual Studio 2015 Update 1 | [1.1.0](https://www.nuget.org/packages/Microsoft.CodeAnalysis.FxCopAnalyzers/1.1.0) |
| Visual Studio 2015 RTW | [1.0.1](https://www.nuget.org/packages/Microsoft.CodeAnalysis.FxCopAnalyzers/1.0.1) |

## <a name="to-install-fxcop-analyzers-as-a-vsix"></a>将 FxCop 分析器安装为 VSIX

::: moniker range="vs-2017"

在 Visual Studio 2017 版本15.5 及更高版本上, 你可以安装[Microsoft 代码分析 2017](https://marketplace.visualstudio.com/items?itemName=VisualStudioPlatformTeam.MicrosoftCodeAnalysis2017)扩展, 其中包含托管项目的所有 FxCop 分析器。

1. 在 Visual Studio 中, 选择 "**工具** > " "**扩展和更新**"。

   此时，“扩展和更新”对话框打开。

   > [!NOTE]
   > 或者, 直接从[Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=VisualStudioPlatformTeam.MicrosoftCodeAnalysis2017)下载扩展。

2. 在左窗格中展开 "**联机**", 然后选择 " **Visual Studio Marketplace**"。

3. 在搜索框中键入 "代码分析", 并查找**Microsoft 代码分析 2017**扩展。

   ![Microsoft 代码分析2017扩展](media/extensions-and-updates-code-analysis.png)

::: moniker-end

::: moniker range=">=vs-2019"

[Microsoft 代码分析 2019](https://marketplace.visualstudio.com/items?itemName=VisualStudioPlatformTeam.MicrosoftCodeAnalysis2019)扩展包含托管项目的所有 FxCop 分析器。 若要安装此扩展:

1. 在 Visual Studio 中, 选择 "**扩展** > " "**管理扩展**"。

   此时将打开 "**管理扩展**" 对话框。

   > [!NOTE]
   > 或者, 直接从[Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=VisualStudioPlatformTeam.MicrosoftCodeAnalysis2019)下载扩展。

2. 在左窗格中展开 "**联机**", 然后选择 " **Visual Studio Marketplace**"。

3. 在搜索框中键入 "代码分析", 并查找**Microsoft 代码分析 2019**扩展。

   ![Microsoft 代码分析2019扩展](media/manage-extensions-code-analysis.png)

::: moniker-end

4. 选择 "**下载**"。

   此扩展已下载。

5. 选择 **"确定"** 关闭对话框, 然后关闭 Visual Studio 的所有实例以启动**VSIX 安装程序**。

   此时将打开 " **VSIX 安装程序**" 对话框。

   ::: moniker range="vs-2017"

   ![适用于 Microsoft 代码分析的 VSIX 安装程序](media/vsix-installer-code-analysis.png)

   ::: moniker-end

6. 选择 "**修改**" 以启动安装。

   一分钟或两分钟后, 安装完成。

7. 选择 "**关闭**", 然后重新打开 Visual Studio。

::: moniker range="vs-2017"

如果要检查是否安装了扩展, 请选择 "**工具** > " "**扩展和更新**"。 在 "**扩展和更新**" 对话框中, 选择左侧的 "**已安装**" 类别, 然后按名称搜索扩展。

::: moniker-end

::: moniker range=">=vs-2019"

如果要检查是否安装了扩展, 请选择 "**扩展** > " "**管理扩展**"。 在 "**管理扩展**" 对话框中, 选择左侧的 "**已安装**" 类别, 然后按名称搜索扩展。

::: moniker-end

## <a name="see-also"></a>请参阅

- [Visual Studio 中的代码分析器概述](../code-quality/roslyn-analyzers-overview.md)
- [在 Visual Studio 中使用代码分析器](../code-quality/use-roslyn-analyzers.md)
- [从旧分析迁移到代码分析器](../code-quality/fxcop-analyzers.yml)
