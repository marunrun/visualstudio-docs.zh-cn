---
title: 从 IDE 或命令行生成代码度量值
ms.date: 11/02/2018
ms.topic: how-to
helpviewer_keywords:
- code metrics data
- code metrics results
- code metrics [Visual Studio]
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 145525dc12070d98dae83d592ae86a675bb605d2
ms.sourcegitcommit: 4d7c883ea3eedd795eeb4a9d3bd3dee82c8e093e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2020
ms.locfileid: "88893406"
---
# <a name="how-to-generate-code-metrics-data"></a>如何：生成代码度量数据

可以通过以下三种方式生成代码度量数据：

- 通过启用 [.net 代码质量分析器](#net-code-quality-analyzers-code-metrics-rules) 并启用四个代码度量值 (可维护性) 其包含的规则。

- 选择 Visual Studio 中的 " [**分析**  >  **计算代码度量值**](#calculate-code-metrics-menu-command) " 菜单命令。

- 在 c # 和 Visual Basic 项目的 [命令行](#command-line-code-metrics) 中。

## <a name="net-code-quality-analyzers-code-metrics-rules"></a>.NET 代码质量分析器代码度量规则

.NET 代码质量分析器包含多个代码度量 [分析器](roslyn-analyzers-overview.md) 规则：

- [CA1501](ca1501-avoid-excessive-inheritance.md)
- [CA1502](ca1502.md)
- [CA1505](ca1505.md)
- [CA1506](ca1506.md)

默认情况下，这些规则是禁用的，但你可以从 [**解决方案资源管理器**](use-roslyn-analyzers.md#set-rule-severity-from-solution-explorer) 或 [规则集](using-rule-sets-to-group-code-analysis-rules.md) 文件中启用它们。 例如，若要启用规则 CA1502 作为警告，你的文件将包含以下条目：

```xml
<?xml version="1.0" encoding="utf-8"?>
<RuleSet Name="Rules" Description="Rules" ToolsVersion="16.0">
  <Rules AnalyzerId="Microsoft.CodeQuality.Analyzers" RuleNamespace="Microsoft.CodeQuality.Analyzers">
    <Rule Id="CA1502" Action="Warning" />
  </Rules>
</RuleSet>
```

### <a name="configuration"></a>配置

你可以配置触发代码度量规则的阈值。

1. 创建文本文件。 例如，你可以将其命名为 *CodeMetricsConfig.txt*。

2. 将所需阈值添加到文本文件，格式如下：

   ```txt
   CA1502: 10
   ```

   在此示例中，规则 [CA1502](ca1502.md) 配置为在方法的圈复杂度大于10时激发。

3. 在 Visual Studio 的 " **属性** " 窗口中，或者在项目文件中，将配置文件的生成操作标记为 " [**AdditionalFiles**](../ide/build-actions.md#build-action-values)"。 例如：

   ```xml
   <ItemGroup>
     <AdditionalFiles Include="CodeMetricsConfig.txt" />
   </ItemGroup>
   ```

## <a name="calculate-code-metrics-menu-command"></a>"计算代码度量值" 菜单命令

使用 "**分析**  >  **计算代码度量值**" 菜单为 IDE 中的一个或所有打开的项目生成代码度量值。

### <a name="generate-code-metrics-results-for-an-entire-solution"></a>为整个解决方案生成代码度量结果

可以通过以下任一方式生成整个解决方案的代码度量结果：

- 从菜单栏中，选择 "**分析**  >  为解决方案**计算代码度量值**"  >  **For Solution**。

- 在 **解决方案资源管理器**中，右键单击解决方案，然后选择 " **计算代码度量值**"。

- 在 " **代码度量值结果** " 窗口中，选择 " **计算解决方案的代码度量值** " 按钮。

将生成结果，并显示 " **代码度量结果** " 窗口。 若要查看结果详细信息，请展开 " **层次结构** " 列中的树。

### <a name="generate-code-metrics-results-for-one-or-more-projects"></a>为一个或多个项目生成代码度量结果

1. 在 **解决方案资源管理器**中，选择一个或多个项目。

1. 从菜单栏中，选择 "**分析**  >  计算**Calculate Code Metrics**  >  **所选项目 (的**代码度量值") 。

将生成结果，并显示 " **代码度量结果** " 窗口。 若要查看结果详细信息，请在 **层次结构**中展开树。

::: moniker range="vs-2017"

> [!NOTE]
> " **计算代码度量值** " 命令对于 .net Core 和 .NET Standard 项目不起作用。 若要为 .NET Core 或 .NET Standard 项目计算代码度量值，可以执行以下操作：
>
> - 改为从 [命令行](#command-line-code-metrics) 计算代码度量值
>
> - 升级到 [Visual Studio 2019](https://visualstudio.microsoft.com/downloads)

::: moniker-end

## <a name="command-line-code-metrics"></a>命令行代码度量值

你可以从 c # 的命令行生成代码度量数据，并 Visual Basic .NET Framework、.NET Core 和 .NET Standard 应用程序的项目。 若要从命令行运行代码度量值，请安装 [CodeAnalysis NuGet 包](#microsoftcodeanalysismetrics-nuget-package) 或自行生成 [Metrics.exe](#metricsexe) 可执行文件。

### <a name="microsoftcodeanalysismetrics-nuget-package"></a>CodeAnalysis NuGet 包

若要从命令行生成代码度量数据，最简单的方法是安装 [CodeAnalysis](https://www.nuget.org/packages/Microsoft.CodeAnalysis.Metrics/) NuGet 包。 安装程序包后， `msbuild /t:Metrics` 从包含项目文件的目录中运行。 例如：

```shell
C:\source\repos\ClassLibrary3\ClassLibrary3>msbuild /t:Metrics
Microsoft (R) Build Engine version 16.0.360-preview+g9781d96883 for .NET Framework
Copyright (C) Microsoft Corporation. All rights reserved.

Build started 1/22/2019 4:29:57 PM.
Project "C:\source\repos\ClassLibrary3\ClassLibrary3\ClassLibrary3.csproj" on node 1 (Metrics target(s))
.
Metrics:
  C:\source\repos\ClassLibrary3\packages\Microsoft.CodeMetrics.2.6.4-ci\build\\..\Metrics\Metrics.exe /project:C:\source\repos\ClassLibrary3\ClassLibrary3\ClassLibrary3.csproj /out:ClassLibrary3.Metrics.xml
  Loading ClassLibrary3.csproj...
  Computing code metrics for ClassLibrary3.csproj...
  Writing output to 'ClassLibrary3.Metrics.xml'...
  Completed Successfully.
Done Building Project "C:\source\repos\ClassLibrary3\ClassLibrary3\ClassLibrary3.csproj" (Metrics target(s)).

Build succeeded.
    0 Warning(s)
    0 Error(s)
```

您可以通过指定来覆盖输出文件的名称 `/p:MetricsOutputFile=<filename>` 。 还可以通过指定来获取 [旧样式的](#previous-versions) 代码度量数据 `/p:LEGACY_CODE_METRICS_MODE=true` 。 例如：

```shell
C:\source\repos\ClassLibrary3\ClassLibrary3>msbuild /t:Metrics /p:LEGACY_CODE_METRICS_MODE=true /p:MetricsOutputFile="Legacy.xml"
Microsoft (R) Build Engine version 16.0.360-preview+g9781d96883 for .NET Framework
Copyright (C) Microsoft Corporation. All rights reserved.

Build started 1/22/2019 4:31:00 PM.
The "MetricsOutputFile" property is a global property, and cannot be modified.
Project "C:\source\repos\ClassLibrary3\ClassLibrary3\ClassLibrary3.csproj" on node 1 (Metrics target(s))
.
Metrics:
  C:\source\repos\ClassLibrary3\packages\Microsoft.CodeMetrics.2.6.4-ci\build\\..\Metrics.Legacy\Metrics.Legacy.exe /project:C:\source\repos\ClassLibrary3\ClassLibrary3\ClassLibrary3.csproj /out:Legacy.xml
  Loading ClassLibrary3.csproj...
  Computing code metrics for ClassLibrary3.csproj...
  Writing output to 'Legacy.xml'...
  Completed Successfully.
Done Building Project "C:\source\repos\ClassLibrary3\ClassLibrary3\ClassLibrary3.csproj" (Metrics target(s)).

Build succeeded.
    0 Warning(s)
    0 Error(s)
```

### <a name="code-metrics-output"></a>代码度量输出

生成的 XML 输出采用以下格式：

::: moniker range=">=vs-2019"

```xml
<?xml version="1.0" encoding="utf-8"?>
<CodeMetricsReport Version="1.0">
  <Targets>
    <Target Name="ConsoleApp20.csproj">
      <Assembly Name="ConsoleApp20, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
        <Metrics>
          <Metric Name="MaintainabilityIndex" Value="100" />
          <Metric Name="CyclomaticComplexity" Value="1" />
          <Metric Name="ClassCoupling" Value="1" />
          <Metric Name="DepthOfInheritance" Value="1" />
          <Metric Name="SourceLines" Value="11" />
          <Metric Name="ExecutableLines" Value="1" />
        </Metrics>
        <Namespaces>
          <Namespace Name="ConsoleApp20">
            <Metrics>
              <Metric Name="MaintainabilityIndex" Value="100" />
              <Metric Name="CyclomaticComplexity" Value="1" />
              <Metric Name="ClassCoupling" Value="1" />
              <Metric Name="DepthOfInheritance" Value="1" />
              <Metric Name="SourceLines" Value="11" />
              <Metric Name="ExecutableLines" Value="1" />
            </Metrics>
            <Types>
              <NamedType Name="Program">
                <Metrics>
                  <Metric Name="MaintainabilityIndex" Value="100" />
                  <Metric Name="CyclomaticComplexity" Value="1" />
                  <Metric Name="ClassCoupling" Value="1" />
                  <Metric Name="DepthOfInheritance" Value="1" />
                  <Metric Name="SourceLines" Value="7" />
                  <Metric Name="ExecutableLines" Value="1" />
                </Metrics>
                <Members>
                  <Method Name="void Program.Main(string[] args)" File="C:\source\repos\ConsoleApp20\ConsoleApp20\Program.cs" Line="7">
                    <Metrics>
                      <Metric Name="MaintainabilityIndex" Value="100" />
                      <Metric Name="CyclomaticComplexity" Value="1" />
                      <Metric Name="ClassCoupling" Value="1" />
                      <Metric Name="SourceLines" Value="4" />
                      <Metric Name="ExecutableLines" Value="1" />
                    </Metrics>
                  </Method>
                </Members>
              </NamedType>
            </Types>
          </Namespace>
        </Namespaces>
      </Assembly>
    </Target>
  </Targets>
</CodeMetricsReport>
```

::: moniker-end
::: moniker range="vs-2017"

```xml
<?xml version="1.0" encoding="utf-8"?>
<CodeMetricsReport Version="1.0">
  <Targets>
    <Target Name="ConsoleApp20.csproj">
      <Assembly Name="ConsoleApp20, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
        <Metrics>
          <Metric Name="MaintainabilityIndex" Value="100" />
          <Metric Name="CyclomaticComplexity" Value="1" />
          <Metric Name="ClassCoupling" Value="1" />
          <Metric Name="DepthOfInheritance" Value="1" />
          <Metric Name="LinesOfCode" Value="11" />
        </Metrics>
        <Namespaces>
          <Namespace Name="ConsoleApp20">
            <Metrics>
              <Metric Name="MaintainabilityIndex" Value="100" />
              <Metric Name="CyclomaticComplexity" Value="1" />
              <Metric Name="ClassCoupling" Value="1" />
              <Metric Name="DepthOfInheritance" Value="1" />
              <Metric Name="LinesOfCode" Value="11" />
            </Metrics>
            <Types>
              <NamedType Name="Program">
                <Metrics>
                  <Metric Name="MaintainabilityIndex" Value="100" />
                  <Metric Name="CyclomaticComplexity" Value="1" />
                  <Metric Name="ClassCoupling" Value="1" />
                  <Metric Name="DepthOfInheritance" Value="1" />
                  <Metric Name="LinesOfCode" Value="7" />
                </Metrics>
                <Members>
                  <Method Name="void Program.Main(string[] args)" File="C:\source\repos\ConsoleApp20\ConsoleApp20\Program.cs" Line="7">
                    <Metrics>
                      <Metric Name="MaintainabilityIndex" Value="100" />
                      <Metric Name="CyclomaticComplexity" Value="1" />
                      <Metric Name="ClassCoupling" Value="1" />
                      <Metric Name="LinesOfCode" Value="4" />
                    </Metrics>
                  </Method>
                </Members>
              </NamedType>
            </Types>
          </Namespace>
        </Namespaces>
      </Assembly>
    </Target>
  </Targets>
</CodeMetricsReport>
```

::: moniker-end

### <a name="metricsexe"></a>Metrics.exe

如果你不想安装 NuGet 包，则可以直接生成并使用 *Metrics.exe* 可执行文件。 生成 *Metrics.exe* 可执行文件：

1. 克隆 [dotnet/roslyn](https://github.com/dotnet/roslyn-analyzers) 存储库。
2. 以管理员身份打开 Visual Studio 开发人员命令提示。
3. 从 **roslyn** 存储库的根目录中执行以下命令： `Restore.cmd`
4. 将目录更改为 *src\Tools*。
5. 执行以下命令以生成 **度量值 .csproj** 项目：

   ```shell
   msbuild /m /v:m /p:Configuration=Release Metrics.csproj
   ```

   在存储库根下的*artifacts\bin*目录中生成名为*Metrics.exe*的可执行文件。

#### <a name="metricsexe-usage"></a>Metrics.exe 用法

若要运行 *Metrics.exe*，请将项目或解决方案和输出 XML 文件作为参数提供。 例如：

```shell
C:\>Metrics.exe /project:ConsoleApp20.csproj /out:report.xml
Loading ConsoleApp20.csproj...
Computing code metrics for ConsoleApp20.csproj...
Writing output to 'report.xml'...
Completed Successfully.
```

#### <a name="legacy-mode"></a>旧模式

您可以选择在*旧模式下*构建*Metrics.exe* 。 此工具的旧模式版本生成的指标值更接近 [生成的工具的较旧版本](#previous-versions)。 此外，在旧模式下， *Metrics.exe* 为工具生成的代码度量值的同一组方法类型生成代码度量值。 例如，它不会为字段和属性初始值设定项生成代码度量数据。 旧模式可用于向后兼容，或者如果你具有基于代码度量值的代码签入入口。 用于生成旧模式 *Metrics.exe* 的命令为：

```shell
msbuild /m /v:m /t:rebuild /p:LEGACY_CODE_METRICS_MODE=true Metrics.csproj
```

有关详细信息，请参阅 [在传统模式下启用生成代码度量值](https://github.com/dotnet/roslyn-analyzers/pull/1841)。

### <a name="previous-versions"></a>旧版

::: moniker range=">=vs-2019"
Visual Studio 2015 附带了一个命令行代码度量工具，该工具也称为 *Metrics.exe*。 此工具的以前版本执行二进制分析，即基于程序集的分析。 较新版本的 *Metrics.exe* 工具改为分析源代码。 由于较新 *Metrics.exe* 工具是基于源代码的，因此，命令行代码度量结果可能与 VISUAL Studio IDE 和以前版本的 *Metrics.exe*所生成的结果不同。 从 Visual Studio 2019 开始，Visual Studio IDE 将分析类似于命令行工具的源代码，结果应相同。

::: moniker-end
::: moniker range="vs-2017"
Visual Studio 2015 附带了一个命令行代码度量工具，该工具也称为 *Metrics.exe*。 此工具的以前版本执行二进制分析，即基于程序集的分析。 新的 *Metrics.exe* 工具改为分析源代码。 由于新的 *Metrics.exe* 工具是基于源代码的，因此，命令行代码度量结果与 VISUAL Studio IDE 和以前版本的 *Metrics.exe*生成的结果不同。
::: moniker-end

即使存在源代码错误，新的命令行代码度量工具也会计算度量值，前提是解决方案和项目可以加载。

#### <a name="metric-value-differences"></a>指标值差异

::: moniker range=">=vs-2019"
从 Visual Studio 2019 版本16.4 和 CodeAnalysis Dc 中开始 (2.9.5) ， `SourceLines` 并 `ExecutableLines` 替换以前的 `LinesOfCode` 指标。 有关新指标的说明，请参阅 [代码度量值](../code-quality/code-metrics-values.md)。 此 `LinesOfCode` 指标在旧模式下可用。
::: moniker-end
::: moniker range="vs-2017"
此 `LinesOfCode` 指标在新的命令行代码度量工具中更准确且更可靠。 它独立于任何 codegen 差异，并且在工具集或运行时发生更改时不会更改。 新工具将计算代码的实际行数，包括空白行和注释。
::: moniker-end

其他指标（例如 `CyclomaticComplexity` 和） `MaintainabilityIndex` 使用与 *Metrics.exe*以前版本相同的公式，但新的工具会对 (逻辑源指令的数量进行计数， `IOperations` 而不是) 中间语言 (IL) 说明。 这些数字将与 Visual Studio IDE 和以前版本的 *Metrics.exe*生成的数字略有不同。

## <a name="see-also"></a>请参阅

- [使用 "代码度量结果" 窗口](../code-quality/working-with-code-metrics-data.md)
- [代码度量值](../code-quality/code-metrics-values.md)
