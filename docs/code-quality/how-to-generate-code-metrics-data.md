---
title: 从 IDE 或命令行生成代码指标
ms.date: 11/02/2018
ms.topic: conceptual
helpviewer_keywords:
- code metrics data
- code metrics results
- code metrics [Visual Studio]
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 1abae26ed8a5e5db74f7b0d04db66d9d99930d5c
ms.sourcegitcommit: ade07bd1cf69b8b494d171ae648cfdd54f7800d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81649332"
---
# <a name="how-to-generate-code-metrics-data"></a>如何：生成代码指标数据

您可以通过三种方式生成代码指标数据：

- 通过安装[FxCop 分析器](#fxcop-analyzers-code-metrics-rules)并启用它包含的四个代码指标（可维护性）规则。

- 通过在可视化工作室中选择"[**分析** > 计算代码指标"](#calculate-code-metrics-menu-command)菜单命令。

- 从 C# 和可视化基本项目[的命令行](#command-line-code-metrics)。

## <a name="fxcop-analyzers-code-metrics-rules"></a>FxCop 分析器代码指标规则

[FxCopAnalyzers NuGet 包](https://www.nuget.org/packages/Microsoft.CodeAnalysis.FxCopAnalyzers)包括多个代码指标[分析器](roslyn-analyzers-overview.md)规则：

- [CA1501](ca1501-avoid-excessive-inheritance.md)
- [CA1502](ca1502.md)
- [CA1505](ca1505.md)
- [CA1506](ca1506.md)

默认情况下禁用这些规则，但可以从[**解决方案资源管理器**](use-roslyn-analyzers.md#set-rule-severity-from-solution-explorer)或[规则集](using-rule-sets-to-group-code-analysis-rules.md)文件中启用这些规则。 例如，要启用规则 CA1502 作为警告，您的 .ruleset 文件将包含以下条目：

```xml
<?xml version="1.0" encoding="utf-8"?>
<RuleSet Name="Rules" Description="Rules" ToolsVersion="16.0">
  <Rules AnalyzerId="Microsoft.CodeQuality.Analyzers" RuleNamespace="Microsoft.CodeQuality.Analyzers">
    <Rule Id="CA1502" Action="Warning" />
  </Rules>
</RuleSet>
```

### <a name="configuration"></a>配置

您可以配置 FxCop 分析器包中代码指标规则触发的阈值。

1. 创建文本文件。 例如，您可以将其命名为*CodeMetricsConfig.txt*。

2. 以以下格式向文本文件添加所需的阈值：

   ```txt
   CA1502: 10
   ```

   在此示例中，规则[CA1502](ca1502.md)配置为在方法的循环复杂性大于 10 时触发。

3. 在 Visual Studio**的"属性"** 窗口中或项目文件中，将配置文件的生成操作标记为[**"附加文件**](../ide/build-actions.md#build-action-values)"。 例如：

   ```xml
   <ItemGroup>
     <AdditionalFiles Include="CodeMetricsConfig.txt" />
   </ItemGroup>
   ```

## <a name="calculate-code-metrics-menu-command"></a>计算代码指标菜单命令

通过使用 **"分析** > **计算代码指标"** 菜单，为 IDE 中的一个或所有打开的项目生成代码指标。

### <a name="generate-code-metrics-results-for-an-entire-solution"></a>为整个解决方案生成代码指标结果

您可以通过以下任何方式为整个解决方案生成代码指标结果：

- 在菜单栏中，选择 **"分析** > **计算解决方案****的代码指标** > "。

- 在**解决方案资源管理器**中，右键单击解决方案，然后选择 **"计算代码指标**"。

- 在 **"代码指标结果"** 窗口中，选择 **"计算解决方案的代码指标"** 按钮。

生成结果并显示 **"代码指标结果**"窗口。 要查看结果详细信息，请展开 **"层次结构**"列中的树。

### <a name="generate-code-metrics-results-for-one-or-more-projects"></a>为一个或多个项目生成代码指标结果

1. 在**解决方案资源管理器中**，选择一个或多个项目。

1. 从菜单栏中，选择 **"分析** > **计算** > **所选项目**的代码指标"。

生成结果并显示 **"代码指标结果**"窗口。 要查看结果详细信息，请展开**层次结构**中的树。

::: moniker range="vs-2017"

> [!NOTE]
> **计算代码指标命令**不适用于 .NET Core 和 .NET 标准项目。 要计算 .NET Core 或 .NET 标准项目的代码指标，可以：
>
> - 而是从[命令行](#command-line-code-metrics)计算代码指标
>
> - 升级到[视觉工作室 2019](https://visualstudio.microsoft.com/downloads)

::: moniker-end

## <a name="command-line-code-metrics"></a>命令行代码指标

可以从 .NET Framework、.NET Core 和 .NET 标准应用的 C# 和 Visual Basic 项目的命令行生成代码指标数据。 要从命令行运行代码指标，请安装[Microsoft.CodeAnalysis.Metrics NuGet 包](#microsoftcodeanalysismetrics-nuget-package)或自行构建[指标.exe](#metricsexe)可执行文件。

### <a name="microsoftcodeanalysismetrics-nuget-package"></a>微软.代码分析.指标 NuGet 包

从命令行生成代码指标数据的最简单方法是安装[Microsoft.CodeAnalysis.Metrics](https://www.nuget.org/packages/Microsoft.CodeAnalysis.Metrics/) NuGet 包。 安装包后，从包含项目文件的目录`msbuild /t:Metrics`运行。 例如：

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

可以通过指定`/p:MetricsOutputFile=<filename>`覆盖输出文件名来覆盖输出文件名。 还可以通过指定`/p:LEGACY_CODE_METRICS_MODE=true`获取[旧式](#previous-versions)代码指标数据。 例如：

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

### <a name="code-metrics-output"></a>代码指标输出

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

### <a name="metricsexe"></a>指标.exe

如果不想安装 NuGet 包，可以直接生成和使用*Metrics.exe*可执行文件。 要生成*指标.exe*可执行文件：

1. 克隆[点网/罗斯林分析器](https://github.com/dotnet/roslyn-analyzers)回购。
2. 打开 Visual Studio 的开发人员命令提示符作为管理员。
3. 从**roslyn 分析器**回购的根，执行以下命令：`Restore.cmd`
4. 将目录更改为*src_Tools*。
5. 执行以下命令以生成**Metrics.csproj**项目：

   ```shell
   msbuild /m /v:m /p:Configuration=Release Metrics.csproj
   ```

   在存储库根目录下*的项目\bin*目录中生成名为*Metrics.exe*的可执行文件。

#### <a name="metricsexe-usage"></a>指标.exe 用法

要运行*Metrics.exe，* 提供项目或解决方案以及输出 XML 文件作为参数。 例如：

```shell
C:\>Metrics.exe /project:ConsoleApp20.csproj /out:report.xml
Loading ConsoleApp20.csproj...
Computing code metrics for ConsoleApp20.csproj...
Writing output to 'report.xml'...
Completed Successfully.
```

#### <a name="legacy-mode"></a>旧模式

您可以选择在*旧模式下*构建*指标.exe。* 该工具的旧模式版本生成的指标值更接近[工具的旧版本](#previous-versions)生成。 此外，在旧模式下 *，Metrics.exe*为工具的早期版本为其生成代码指标的相同方法类型生成代码指标。 例如，它不为字段和属性初始化器生成代码指标数据。 旧版模式对于向后兼容性或基于代码指标编号的代码签入门非常有用。 在旧模式下生成*Metrics.exe*的命令是：

```shell
msbuild /m /v:m /t:rebuild /p:LEGACY_CODE_METRICS_MODE=true Metrics.csproj
```

有关详细信息，请参阅[在旧模式下启用生成代码指标](https://github.com/dotnet/roslyn-analyzers/pull/1841)。

### <a name="previous-versions"></a>以前的版本

::: moniker range=">=vs-2019"
Visual Studio 2015 包括一个命令行代码指标工具，也称为*Metrics.exe*。 该工具的早期版本做了二进制分析，即基于程序集的分析。 较新版本的*Metrics.exe*工具将分析源代码。 由于较新的*Metrics.exe*工具基于源代码，因此命令行代码指标的结果可能与 Visual Studio IDE 和早期*版本的 Metrics.exe*生成的指标不同。 从 Visual Studio 2019 开始，Visual Studio IDE 会分析源代码，如命令行工具，结果应相同。

::: moniker-end
::: moniker range="vs-2017"
Visual Studio 2015 包括一个命令行代码指标工具，也称为*Metrics.exe*。 该工具的早期版本做了二进制分析，即基于程序集的分析。 新的*Metrics.exe*工具将分析源代码。 由于新的*Metrics.exe*工具基于源代码，因此命令行代码指标结果与 Visual Studio IDE 和早期*版本的 Metrics.exe*生成的结果不同。
::: moniker-end

新的命令行代码指标工具即使在存在源代码错误的情况下也计算指标，只要可以加载解决方案和项目。

#### <a name="metric-value-differences"></a>指标值差异

::: moniker range=">=vs-2019"
从 Visual Studio 2019 版本 16.4 和 Microsoft.CodeAnalysis.Metics `SourceLines` （2.9.5） 开始，并`ExecutableLines`替换以前的`LinesOfCode`指标。 有关新指标的说明，请参阅[代码指标值](../code-quality/code-metrics-values.md)。 该`LinesOfCode`指标在旧模式下可用。
::: moniker-end
::: moniker range="vs-2017"
在新的`LinesOfCode`命令行代码指标工具中，该指标更准确、更可靠。 它独立于任何代码项差异，并且在工具集或运行时更改时不会更改。 新工具计算实际代码行，包括空白行和注释。
::: moniker-end

其他`CyclomaticComplexity`指标（如 和`MaintainabilityIndex`使用的公式与以前版本的*Metrics.exe）* 相同，但新工具计算（逻辑源`IOperations`指令）的数量，而不是中间语言 （IL） 指令的数量。 这些数字将略有不同，由视觉工作室IDE和早期版本的*Metrics.exe*生成。

## <a name="see-also"></a>另请参阅

- [使用"代码指标结果"窗口](../code-quality/working-with-code-metrics-data.md)
- [代码指标值](../code-quality/code-metrics-values.md)
