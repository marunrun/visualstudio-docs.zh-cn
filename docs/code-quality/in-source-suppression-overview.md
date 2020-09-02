---
title: 禁止显示代码分析冲突
ms.date: 08/27/2020
ms.topic: conceptual
helpviewer_keywords:
- source suppression, code analysis
- code analysis, source suppression
author: mikadumont
ms.author: midumont
manager: jillfra
dev_langs:
- CSharp
- VB
- CPP
ms.workload:
- multiple
ms.openlocfilehash: aa650197f291c48c0c025563098181ea1cfa19a7
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89091433"
---
# <a name="suppress-code-analysis-violations"></a>禁止显示代码分析冲突

它通常用于指示警告不适用。 这向团队成员表明代码已评审，并且可以禁止显示该警告。  (ISS) 中的源代码中禁止 <xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute> 显示警告。 特性可放置在生成警告的代码段附近。 可以 <xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute> 通过在源文件中键入来将其添加到源文件中，也可以使用 **错误列表** 中的警告的快捷菜单来自动添加该属性。

<xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute>特性是一个条件特性，仅当编译时定义了 CODE_ANALYSIS 编译符号时，它才包含在托管代码程序集的 IL 元数据中。

在 c + +/CLI 中，使用 \_ 标头文件中的宏 CA 禁止显示 \_ 消息或 CA \_ 全局 \_ SUPPRESS_MESSAGE 来添加属性。

> [!NOTE]
> 不应在发布版本中使用源内禁止显示，以防止意外发送源中禁止显示元数据。 此外，由于源中禁止显示的处理成本，你的应用程序的性能可能会下降。

::: moniker range="vs-2017"

> [!NOTE]
> 如果将项目迁移到 Visual Studio 2017，可能会突然遇到大量代码分析警告。 如果尚未准备好修复警告，则可以通过选择 "**分析**" "  >  **运行代码分析" 并取消 "活动问题**" 来取消所有这些警告。
>
> ![在 Visual Studio 中运行代码分析并取消问题](media/suppress-active-issues.png)

::: moniker-end

::: moniker range=">=vs-2019"

> [!NOTE]
> 如果将项目迁移到 Visual Studio 2019，可能会突然遇到大量代码分析警告。 如果尚未准备好修复警告，则可以通过选择 "**分析**  >  **生成并取消活动问题**" 来禁止显示这些警告。

::: moniker-end

## <a name="suppressmessage-attribute"></a>SuppressMessage 特性

如果从**错误列表**中的 "代码分析" 警告的上下文或右键单击菜单中选择 "**隐藏**"，则 <xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute> 会在代码或项目的全局禁止显示文件中添加特性。

该 <xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute> 属性具有以下格式：

```vb
<Scope:SuppressMessage("Rule Category", "Rule Id", Justification = "Justification", MessageId = "MessageId", Scope = "Scope", Target = "Target")>
```

```csharp
[Scope:SuppressMessage("Rule Category", "Rule Id", Justification = "Justification", MessageId = "MessageId", Scope = "Scope", Target = "Target")]
```

```cpp
CA_SUPPRESS_MESSAGE("Rule Category", "Rule Id", Justification = "Justification", MessageId = "MessageId", Scope = "Scope", Target = "Target")
```

属性的属性包括：

- **类别** -定义规则的类别。 有关代码分析规则类别的详细信息，请参阅 [托管代码警告](../code-quality/code-analysis-for-managed-code-warnings.md)。

- **CheckId** -规则的标识符。 支持包括规则标识符的短名称和长名称。 短名称为 CAXXXX;长名称为 CAXXXX： FriendlyTypeName。

- **对齐** -用于记录取消消息原因的文本。

- **MessageId** -每个消息的问题的唯一标识符。

- **作用域** -要禁止显示警告的目标。 如果未指定目标，则将其设置为属性的目标。 支持的 [范围](xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute.Scope) 包括：

  - [`module`](#module-suppression-scope) -此作用域禁止对程序集发出警告。 它是适用于整个项目的全局禁止显示。

  - `resource` - ([仅](../code-quality/static-code-analysis-for-managed-code-overview.md)) 此作用域中的警告，会禁止将诊断信息中的警告写入属于模块 (程序集) 模块的资源文件中。 对于 Roslyn 分析器诊断，不在 c #/VB 编译器中阅读/遵循此范围，仅分析源文件。

  - `type` -此作用域禁止对类型发出警告。

  - `member` -此作用域禁止对成员的警告。

  - `namespace` -此范围禁止显示针对命名空间本身的警告。 它不会禁止对命名空间中的类型发出警告。

  - `namespaceanddescendants` - (需要编译器版本3.x 或更高版本以及 Visual Studio 2019) 此范围禁止显示命名空间及其所有子代符号中的警告。 `namespaceanddescendants`旧分析将忽略该值。

- **目标** -用于指定取消警告的目标的标识符。 它必须包含完全限定的项目名称。

当你在 Visual Studio 中看到警告时，可以 `SuppressMessage` 通过 [将抑制添加到全局禁止显示文件来](../code-quality/use-roslyn-analyzers.md#suppress-violations)查看的示例。 禁止显示属性及其必需的属性将显示在预览窗口中。

## <a name="suppressmessage-usage"></a>SuppressMessage 用法

代码分析警告会在属性应用到的级别上取消 <xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute> 。 例如，可以将属性应用于程序集、模块、类型、成员或参数级别。 这样做的目的是将抑制信息紧密地耦合到发生冲突的代码中。

禁止显示的一般形式包括规则类别和规则标识符，其中包含规则名称的可选可读表示形式。 例如：

`[SuppressMessage("Microsoft.Design", "CA1039:ListsAreStrongTyped")]`

如果由于最大程度地减少了源中禁止显示元数据的性能原因，则可以省略规则名称。 规则类别及其规则 ID 共同构成了一个足够唯一的规则标识符。 例如：

`[SuppressMessage("Microsoft.Design", "CA1039")]`

出于可维护性的原因，不建议省略规则名称。

## <a name="suppress-selective-violations-within-a-method-body"></a>在方法体中取消选择性冲突

禁止显示特性可应用于方法，但不能嵌入方法体中。 这意味着，如果将特性添加到方法，则将禁止显示某个特定规则的所有冲突 <xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute> 。

在某些情况下，您可能需要取消特定的冲突实例，例如，使将来的代码不会自动从代码分析规则中免除。 某些代码分析规则允许通过使用属性的属性来执行此操作 `MessageId` <xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute> 。 通常情况下，特定符号上的冲突 (本地变量或参数) 遵从 `MessageId` 属性。 [CA1500： VariableNamesShouldNotMatchFieldNames](../code-quality/ca1500.md) 是此类规则的一个示例。 但是，对可执行代码 (非符号) 的冲突的旧规则不遵守 `MessageId` 属性。 此外，.NET Compiler Platform ( "Roslyn" ) 分析器不遵从 `MessageId` 属性。

若要取消规则的特定符号冲突，请为属性的属性指定符号名称 `MessageId` <xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute> 。 下面的示例显示了[CA1500： VariableNamesShouldNotMatchFieldNames](../code-quality/ca1500.md)的两个冲突的代码 &mdash; ，一个用于 `name` 变量，另一个用于 `age` 变量。 仅 `age` 禁止符号冲突。

```vb
Public Class Animal
    Dim age As Integer
    Dim name As String

    <CodeAnalysis.SuppressMessage("Microsoft.Maintainability", "CA1500:VariableNamesShouldNotMatchFieldNames", MessageId:="age")>
    Sub PrintInfo()
        Dim age As Integer = 5
        Dim name As String = "Charlie"

        Console.WriteLine("Age {0}, Name {1}", age, name)
    End Sub

End Class
```

```csharp
public class Animal
{
    int age;
    string name;

    [System.Diagnostics.CodeAnalysis.SuppressMessage("Microsoft.Maintainability", "CA1500:VariableNamesShouldNotMatchFieldNames", MessageId = "age")]
    private void PrintInfo()
    {
        int age = 5;
        string name = "Charlie";

        Console.WriteLine($"Age {age}, Name {name}");
    }
}
```

## <a name="global-level-suppressions"></a>全局禁止显示

托管代码分析工具检查 `SuppressMessage` 在程序集、模块、类型、成员或参数级别应用的特性。 它还会对资源和命名空间引发冲突。 必须在全局级别应用这些冲突，并确定其作用域和目标。 例如，以下消息取消了命名空间冲突：

`[module: SuppressMessage("Microsoft.Design", "CA1020:AvoidNamespacesWithFewTypes", Scope = "namespace", Target = "MyNamespace")]`

> [!NOTE]
> 当您禁止显示带有作用域的警告时 `namespace` ，它将禁止显示针对命名空间本身的警告。 它不会禁止对命名空间中的类型发出警告。

任何禁止显示都可以通过指定显式范围来表示。 这些禁止显示必须位于全局级别。 不能通过修饰类型来指定成员级禁止显示。

全局级别禁止显示引用编译器生成的代码的消息，这些消息不会映射到显式提供的用户源。 例如，下面的代码针对编译器发出的构造函数禁止发生冲突：

`[module: SuppressMessage("Microsoft.Design", "CA1055:AbstractTypesDoNotHavePublicConstructors", Scope="member", Target="Microsoft.Tools.FxCop.Type..ctor()")]`

> [!NOTE]
> `Target` 始终包含完全限定的项目名称。

### <a name="global-suppression-file"></a>全局禁止显示文件

全局禁止显示文件维护全局级禁止显示或未指定目标的禁止显示的禁止显示。 例如，程序集级别的冲突的禁止显示存储在此文件中。 此外，某些 ASP.NET 禁止显示文件存储在此文件中，因为项目级设置不适用于窗体的代码。 第一次在 "**错误列表**" 窗口中的 "**禁止显示**" 命令的 "**项目禁止显示文件**" 选项中，会创建全局禁止显示文件并将其添加到项目。

### <a name="module-suppression-scope"></a>模块禁止显示范围

您可以使用 **模块** 范围禁止整个程序集的代码质量冲突。

例如， _GlobalSuppressions_ 项目文件中的以下属性将抑制 ASP.NET Core 项目的 ConfigureAwait 冲突：

`[assembly: System.Diagnostics.CodeAnalysis.SuppressMessage("Reliability", "CA2007:Consider calling ConfigureAwait on the awaited task", Justification = "ASP.NET Core doesn't use thread context to store request context.", Scope = "module")]`

## <a name="generated-code"></a>生成的代码

托管代码编译器和一些第三方工具生成代码，以加速代码开发。 出现在源文件中的编译器生成的代码通常用 `GeneratedCodeAttribute` 特性标记。

对于源代码分析，可以使用项目或解决方案根目录中的 [editorconfig](../code-quality/configure-fxcop-analyzers.md) 文件来取消生成的代码中的消息。 使用文件模式与生成的代码匹配。 例如，若要排除 **designer.cs* 文件中的 CS1591 警告，请在配置文件中使用它。

``` cmd
[*.designer.cs]
dotnet_diagnostic.CS1591.severity = none
```

对于旧的代码分析，可以选择是否取消生成代码的代码分析警告和错误。 有关如何禁止显示这些警告和错误的信息，请参阅 [如何：取消显示生成代码的警告](../code-quality/how-to-suppress-code-analysis-warnings-for-generated-code.md)。

> [!NOTE]
> `GeneratedCodeAttribute`当应用于整个程序集或单个参数时，代码分析将忽略。

## <a name="see-also"></a>另请参阅

- <xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute.Scope>
- <xref:System.Diagnostics.CodeAnalysis>
- [使用代码分析器](../code-quality/use-roslyn-analyzers.md)
