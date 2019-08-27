---
title: T4 程序集指令
ms.date: 11/04/2016
ms.topic: reference
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e5dfb9a6489fed2c21d05799e9196c813a224571
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63422946"
---
# <a name="t4-assembly-directive"></a>T4 程序集指令

在 Visual Studio 设计时文本模板中，`assembly`指令可加载程序集，以便在模板代码可以使用它的类型。 结果相当于将程序集引用添加到 Visual Studio 项目中。

 编写文本模板的一般概述，请参阅[编写 T4 文本模板](../modeling/writing-a-t4-text-template.md)。

> [!NOTE]
> 运行时（预处理）文本模板中不需要 `assembly` 指令。 相反，将添加到必需的程序集**引用**的 Visual Studio 项目。

## <a name="using-the-assembly-directive"></a>使用 Assembly 指令
 该指令的语法如下所示：

```
<#@ assembly name="[assembly strong name|assembly file name]" #>
```

 程序集名称应为以下各项之一：

- GAC 中程序集的强名称，例如 `System.Xml.dll`。 还可以使用长形式，例如 `name="System.Xml, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"`。 有关详细信息，请参阅 <xref:System.Reflection.AssemblyName>。

- 程序集的绝对路径

  可以使用`$(variableName)`语法来引用 Visual Studio 变量，如`$(SolutionDir)`，和`%VariableName%`来引用环境变量。 例如：

```
<#@ assembly name="$(SolutionDir)\MyProject\bin\Debug\SomeLibrary.Dll" #>
```

 在预处理文本模板中，assembly 指令无效。 相反，包括必要的引用**引用**部分中的 Visual Studio 项目。 有关详细信息，请参阅[使用 T4 文本模板的运行时文本生成](../modeling/run-time-text-generation-with-t4-text-templates.md)。

## <a name="standard-assemblies"></a>标准程序集
 将自动加载以下程序集，您无需为它们编写程序集指令：

- `Microsoft.VisualStudio.TextTemplating.1*.dll`

- `System.dll`

- `WindowsBase.dll`

  如果您使用自定义指令，则指令处理器可能会加载其他程序集。 例如，如果您为域特定语言 (DSL) 编写模板，则无需为以下程序集编写程序集指令：

- `Microsoft.VisualStudio.Modeling.Sdk.1*.dll`

- `Microsoft.VisualStudio.Modeling.Sdk.Diagrams.1*.dsl`

- `Microsoft.VisualStudio.TextTemplating.Modeling.1*.dll`

- 包含 DSL 的程序集。

## <a name="msbuild"></a> 使用 MSBuild 和 Visual Studio 中的项目属性
 在 MSBuild 中无法使用 visual Studio 宏 $ （solutiondir） 等。 如果你想要在生成计算机中转换模板，则必须改用项目属性。

 编辑 .csproj 或 .vbproj 文件以定义项目属性。 此示例定义一个名为 `myLibFolder` 的属性：

```xml
<!-- Define a project property, myLibFolder: -->
<PropertyGroup>
    <myLibFolder>$(MSBuildProjectDirectory)\..\libs</myLibFolder>
</PropertyGroup>

<!-- Tell the MSBuild T4 task to make the property available: -->
<ItemGroup>
    <T4ParameterValues Include="myLibFolder">
      <Value>$(myLibFolder)</Value>
    </T4ParameterValues>
  </ItemGroup>
```

 现在你可在文本模板中使用项目属性，此类模板将在 Visual Studio 和 MSBuild 中正确转换：

```
<#@ assembly name="$(myLibFolder)\MyLib.dll" #>
```

## <a name="see-also"></a>请参阅

- [T4 包含指令](../modeling/t4-include-directive.md)