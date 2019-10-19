---
title: 禁止显示代码分析警告
ms.date: 12/01/2018
ms.topic: conceptual
helpviewer_keywords:
- source suppression, code analysis
- code analysis, source suppression
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CSharp
- VB
- CPP
ms.workload:
- multiple
ms.openlocfilehash: 2e4a71acfc9872c1709dcfe5abf062a95cb3e89d
ms.sourcegitcommit: 08c144d290da373df841f04fc799e3133540a541
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/17/2019
ms.locfileid: "72535833"
---
# <a name="suppress-code-analysis-warnings"></a>禁止显示代码分析警告

它通常用于指示警告不适用。 这向团队成员表明代码已评审，并且可以禁止显示该警告。 源代码中禁止显示（ISS）使用 <xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute> 特性来禁止显示警告。 特性可放置在生成警告的代码段附近。 您可以通过在源文件中键入来向源文件添加 <xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute> 特性，也可以在**错误列表**中的警告上使用快捷菜单来自动添加它。

仅当在编译时定义了 CODE_ANALYSIS 编译符号时，<xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute> 属性是条件属性，它包含在托管代码程序集的 IL 元数据中。

在C++/cli 中，在头文件中使用宏 CA \_SUPPRESS \_MESSAGE 或 CA \_GLOBAL \_SUPPRESS_MESSAGE 来添加属性。

> [!NOTE]
> 不应在发布版本中使用源内禁止显示，以防止意外发送源中禁止显示元数据。 此外，由于源中禁止显示的处理成本，你的应用程序的性能可能会下降。

::: moniker range="vs-2017"

> [!NOTE]
> 如果将项目迁移到 Visual Studio 2017，可能会突然遇到大量代码分析警告。 如果尚未准备好修复警告，则可以通过选择 "**分析**"  >  "**运行代码分析" 并取消显示活动问题**来禁止显示这些警告。
>
> ![在 Visual Studio 中运行代码分析并取消问题](media/suppress-active-issues.png)

::: moniker-end

::: moniker range=">=vs-2019"

> [!NOTE]
> 如果将项目迁移到 Visual Studio 2019，可能会突然遇到大量代码分析警告。 如果尚未准备好修复警告，可以通过选择 "**分析** > **生成并取消显示活动问题**" 来禁止显示这些警告。

::: moniker-end

## <a name="suppressmessage-attribute"></a>SuppressMessage 特性

如果从**错误列表**中的 "代码分析" 警告的上下文或右键单击菜单中选择 "**隐藏**"，则会在代码或项目的全局禁止显示文件中添加 <xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute> 特性。

@No__t_0 属性采用以下格式：

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

- **类别**-定义规则的类别。 有关代码分析规则类别的详细信息，请参阅[托管代码警告](../code-quality/code-analysis-for-managed-code-warnings.md)。

- **CheckId** -规则的标识符。 支持包括规则标识符的短名称和长名称。 短名称为 CAXXXX;长名称为 CAXXXX： FriendlyTypeName。

- **对齐**-用于记录取消消息原因的文本。

- **MessageId** -每个消息的问题的唯一标识符。

- **作用域**-要禁止显示警告的目标。 如果未指定目标，则将其设置为属性的目标。 支持的[范围](xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute.Scope)包括：

  - `module`

  - `resource`

  - `type`

  - `member`

  - `namespace`-此范围禁止显示针对命名空间本身的警告。 它不会禁止对命名空间中的类型发出警告。

  - `namespaceanddescendants`-（Visual Studio 2019 的新增）此作用域禁止显示命名空间及其所有子代符号中的警告。 旧分析将忽略 `namespaceanddescendants` 值。

- **目标**-用于指定取消警告的目标的标识符。 它必须包含完全限定的项目名称。

## <a name="suppressmessage-usage"></a>SuppressMessage 用法

在 <xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute> 特性应用到的级别上，会禁止显示代码分析警告。 例如，可以将属性应用于程序集、模块、类型、成员或参数级别。 这样做的目的是将抑制信息紧密地耦合到发生冲突的代码中。

禁止显示的一般形式包括规则类别和规则标识符，其中包含规则名称的可选可读表示形式。 例如:

`[SuppressMessage("Microsoft.Design", "CA1039:ListsAreStrongTyped")]`

如果由于最大程度地减少了源中禁止显示元数据的性能原因，则可以省略规则名称。 规则类别及其规则 ID 共同构成了一个足够唯一的规则标识符。 例如:

`[SuppressMessage("Microsoft.Design", "CA1039")]`

出于可维护性的原因，不建议省略规则名称。

## <a name="suppress-selective-violations-within-a-method-body"></a>在方法体中取消选择性冲突

禁止显示特性可应用于方法，但不能嵌入方法体中。 这意味着，如果将 <xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute> 特性添加到方法，则将禁止显示特定规则的所有冲突。

在某些情况下，您可能需要取消特定的冲突实例，例如，使将来的代码不会自动从代码分析规则中免除。 某些代码分析规则允许通过使用 <xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute> 属性的 `MessageId` 属性来执行此操作。 通常，针对特定符号（局部变量或参数）的冲突的旧规则遵循 `MessageId` 属性。 [CA1500： VariableNamesShouldNotMatchFieldNames](../code-quality/ca1500.md)是此类规则的一个示例。 但是，可执行代码（非符号）上的冲突的旧规则不遵循 `MessageId` 属性。 此外，.NET Compiler Platform （"Roslyn"）分析器不遵从 `MessageId` 属性。

若要取消规则的特定符号冲突，请为 <xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute> 属性指定 `MessageId` 属性的符号名称。 下面的示例演示了 `name` 变量的[CA1500： VariableNamesShouldNotMatchFieldNames](../code-quality/ca1500.md) &mdash;one 两个冲突的代码，以及一个 `age` 变量的代码。 仅禁止 `age` 符号发生冲突。

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

## <a name="generated-code"></a>生成的代码

托管代码编译器和一些第三方工具生成代码，以加速代码开发。 出现在源文件中的编译器生成的代码通常用 `GeneratedCodeAttribute` 属性进行标记。

您可以选择是否取消生成代码的代码分析警告和错误。 有关如何禁止显示这些警告和错误的信息，请参阅[如何：取消显示生成代码的警告](../code-quality/how-to-suppress-code-analysis-warnings-for-generated-code.md)。

> [!NOTE]
> 当应用于整个程序集或单个参数时，代码分析将忽略 `GeneratedCodeAttribute`。

## <a name="global-level-suppressions"></a>全局禁止显示

托管代码分析工具检查在程序集、模块、类型、成员或参数级别应用 `SuppressMessage` 特性。 它还会对资源和命名空间引发冲突。 必须在全局级别应用这些冲突，并确定其作用域和目标。 例如，以下消息取消了命名空间冲突：

`[module: SuppressMessage("Microsoft.Design", "CA1020:AvoidNamespacesWithFewTypes", Scope = "namespace", Target = "MyNamespace")]`

> [!NOTE]
> 当您禁止显示带有 `namespace` 作用域的警告时，它将禁止显示针对命名空间本身的警告。 它不会禁止对命名空间中的类型发出警告。

任何禁止显示都可以通过指定显式范围来表示。 这些禁止显示必须位于全局级别。 不能通过修饰类型来指定成员级禁止显示。

全局级别禁止显示引用编译器生成的代码的消息，这些消息不会映射到显式提供的用户源。 例如，下面的代码针对编译器发出的构造函数禁止发生冲突：

`[module: SuppressMessage("Microsoft.Design", "CA1055:AbstractTypesDoNotHavePublicConstructors", Scope="member", Target="Microsoft.Tools.FxCop.Type..ctor()")]`

> [!NOTE]
> `Target` 始终包含完全限定的项目名称。

## <a name="global-suppression-file"></a>全局禁止显示文件

全局禁止显示文件维护全局级禁止显示或未指定目标的禁止显示的禁止显示。 例如，程序集级别的冲突的禁止显示存储在此文件中。 此外，某些 ASP.NET 禁止显示文件存储在此文件中，因为项目级设置不适用于窗体的代码。 第一次在 "**错误列表**" 窗口中的 "**禁止显示**" 命令的 "**项目禁止显示文件**" 选项中，会创建全局禁止显示文件并将其添加到项目。

## <a name="see-also"></a>请参阅

- <xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute.Scope>
- <xref:System.Diagnostics.CodeAnalysis>
- [使用代码分析器](../code-quality/use-roslyn-analyzers.md)
