---
title: 安装 FxCop 分析器
ms.date: 08/03/2018
ms.topic: conceptual
helpviewer_keywords:
- fxcop analyzers
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 1d734ea4d87dc5d1b8f2ca7f1a1891a4cf7d512b
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "79508766"
---
# <a name="install-fxcop-analyzers-in-visual-studio"></a>在视觉工作室安装 FxCop 分析仪

微软创建了一套分析器，称为[微软.CodeAnalysis.FxCopAnalyzers，](https://www.nuget.org/packages/Microsoft.CodeAnalysis.FxCopAnalyzers)其中包含传统分析中最重要的"FxCop"规则。 这些分析器检查代码的安全性、性能和设计问题等。

您可以将这些 FxCop 分析器作为 NuGet 软件包安装，也可以作为 Visual Studio 的 VSIX 扩展名安装。 要了解每个的优缺点，请参阅[NuGet 包与 VSIX 扩展](roslyn-analyzers-overview.md#nuget-package-versus-vsix-extension)。

## <a name="nuget-package"></a>NuGet 包

::: moniker range=">=vs-2019"

在 Visual Studio 2019 版本 16.3 及更高版本中，您可以直接从项目的代码分析属性页面安装[Microsoft.CodeAnalysis.FxCopAnalyzers](https://www.nuget.org/packages/Microsoft.CodeAnalysis.FxCopAnalyzers) NuGet 包：

1. 右键单击**解决方案资源管理器**中的项目节点，选择 **"属性**"，然后选择 **"代码分析**"选项卡。

   ![从 Visual Studio 中的属性页面安装 FxCop 分析仪包](media/install-fxcop-properties-page.png)

2. 选择**安装**。

   Visual Studio 安装最新版本的 Microsoft.CodeAnalysis.FxCopAnalyzers 软件包。 程序集显示在**参考** > **分析器**下**的解决方案资源管理器**中。

   ![解决方案资源管理器中的分析器节点](media/solution-explorer-analyzers-node.png)

如果您使用的是旧版本的 Visual Studio 2019，请使用[包管理器控制台](/nuget/quickstart/install-and-use-a-package-in-visual-studio#package-manager-console)或[包管理器 UI](/nuget/quickstart/install-and-use-a-package-in-visual-studio#package-manager-console)安装包。

::: moniker-end

::: moniker range="vs-2017"

1. 根据您的 Visual Studio 版本确定要安装[的分析器包版本](#fxcopanalyzers-package-versions)。

2. 使用[包管理器控制台](/nuget/quickstart/install-and-use-a-package-in-visual-studio#package-manager-console)或[包管理器 UI](/nuget/quickstart/install-and-use-a-package-in-visual-studio#package-manager-console)在 Visual Studio 中安装包。

   > [!NOTE]
   > 每个分析器包的nuget.org页显示要粘贴到**包管理器控制台**的命令。 甚至还有一个方便的按钮来将文本复制到剪贴板。
   >
   > ![显示包管理器控制台命令的NuGet.org页](media/nuget-package-manager-command.png)

   安装分析器程序集，它们显示在**参考**>**分析器**下**的解决方案资源管理器**中。

::: moniker-end

### <a name="custom-installation"></a>自定义安装

对于自定义安装（例如，要指定包的不同版本），请选择项目代码分析属性页上的省略号 （...） 按钮。 此按钮打开 NuGet 包管理器，其中"Microsoft.CodeAnalysis.FxCopAnalyzers"作为搜索字符串。

![从 Visual Studio 中的属性页面安装自定义 FxCop 分析仪包](media/install-fxcop-properties-page-ellipsis.png)

> [!TIP]
> 根据您的 Visual Studio 版本确定要安装[的分析器包版本](#fxcopanalyzers-package-versions)。 您还可以从[包管理器 UI](/nuget/quickstart/install-and-use-a-package-in-visual-studio#package-manager-console)安装包。

### <a name="fxcopanalyzers-package-versions"></a>FxCopAnalyzer 软件包版本

使用以下准则确定要为 Visual Studio 版本安装哪个版本的 FxCop 分析器包：

| Visual Studio 版本 | FxCop 分析仪包版本 |
| - | - |
| 视觉工作室 2019 （所有版本）<br />视觉工作室 2017 版本 15.8 及更高版本 | [最新](https://www.nuget.org/packages/Microsoft.CodeAnalysis.FxCopAnalyzers/) |
| 视觉工作室 2017 版本 15.5 到 15.7 | [2.6.3](https://www.nuget.org/packages/Microsoft.CodeAnalysis.FxCopAnalyzers/2.6.3) |
| 视觉工作室 2017 版本 15.3 到 15.4 | [2.3.0-贝塔1](https://www.nuget.org/packages/Microsoft.CodeAnalysis.FxCopAnalyzers/2.3.0-beta1) |
| Visual Studio 2017 版本 15.0 到 15.2 | [2.0.0-贝塔2](https://www.nuget.org/packages/Microsoft.CodeAnalysis.FxCopAnalyzers/2.0.0-beta2) |
| 视觉工作室 2015 更新 2 和 3 | [1.2.0-贝塔2](https://www.nuget.org/packages/Microsoft.CodeAnalysis.FxCopAnalyzers/1.2.0-beta2) |
| Visual Studio 2015 Update 1 | [1.1.0](https://www.nuget.org/packages/Microsoft.CodeAnalysis.FxCopAnalyzers/1.1.0) |
| Visual Studio 2015 RTW | [1.0.1](https://www.nuget.org/packages/Microsoft.CodeAnalysis.FxCopAnalyzers/1.0.1) |

## <a name="vsix"></a>VSIX

::: moniker range="vs-2017"

在 Visual Studio 2017 版本 15.5 及更高版本上，您可以安装[Microsoft 代码分析 2017](https://marketplace.visualstudio.com/items?itemName=VisualStudioPlatformTeam.MicrosoftCodeAnalysis2017)扩展，其中包含托管项目的所有 FxCop 分析器。

1. 在可视化工作室中，选择 **"工具**>**扩展和更新**"。

   此时，“扩展和更新”**** 对话框打开。

   > [!NOTE]
   > 或者，直接从[可视化工作室市场](https://marketplace.visualstudio.com/items?itemName=VisualStudioPlatformTeam.MicrosoftCodeAnalysis2017)下载扩展。

2. 在左侧窗格中展开**联机**，然后选择**可视化工作室市场**。

3. 在搜索框中，键入"代码分析"，并查找 Microsoft**代码分析 2017**扩展名。

   ![微软代码分析 2017 扩展](media/extensions-and-updates-code-analysis.png)

::: moniker-end

::: moniker range=">=vs-2019"

[Microsoft 代码分析 2019](https://marketplace.visualstudio.com/items?itemName=VisualStudioPlatformTeam.MicrosoftCodeAnalysis2019)扩展包含托管项目的所有 FxCop 分析器。 要安装此扩展：

1. 在可视化工作室中，选择**扩展**>**管理扩展**。

   将打开"**管理扩展"** 对话框。

   > [!NOTE]
   > 或者，直接从[可视化工作室市场](https://marketplace.visualstudio.com/items?itemName=VisualStudioPlatformTeam.MicrosoftCodeAnalysis2019)下载扩展。

2. 在左侧窗格中展开**联机**，然后选择**可视化工作室市场**。

3. 在搜索框中，键入"代码分析"，并查找 Microsoft**代码分析 2019**扩展名。

   ![微软代码分析 2019 扩展](media/manage-extensions-code-analysis.png)

::: moniker-end

4. 选择“下载”****。

   将下载扩展。

5. 选择 **"确定"** 以关闭对话框，然后关闭 Visual Studio 的所有实例以启动**VSIX 安装程序**。

   将打开**VSIX 安装程序**对话框。

   ::: moniker range="vs-2017"

   ![用于微软代码分析的 VSIX 安装程序](media/vsix-installer-code-analysis.png)

   ::: moniker-end

6. 选择 **"修改"** 以启动安装。

   一两分钟后，安装完成。

7. 选择 **"关闭**"，然后再次打开视觉工作室。

::: moniker range="vs-2017"

如果要检查是否安装了扩展，请选择 **"工具** > **扩展和更新**"。 在"**扩展和更新"** 对话框中，选择左侧的 **"已安装**"类别，然后按名称搜索扩展名。

::: moniker-end

::: moniker range=">=vs-2019"

如果要检查是否安装了扩展，请选择 **"扩展** > **管理扩展**"。 在"**管理扩展"** 对话框中，选择左侧的 **"已安装**"类别，然后按名称搜索扩展名。

::: moniker-end

## <a name="see-also"></a>另请参阅

- [可视化工作室中的代码分析器概述](../code-quality/roslyn-analyzers-overview.md)
- [在 Visual Studio 中使用代码分析器](../code-quality/use-roslyn-analyzers.md)
- [从旧分析迁移到代码分析器](../code-quality/migrate-from-legacy-analysis-to-fxcop-analyzers.md)
