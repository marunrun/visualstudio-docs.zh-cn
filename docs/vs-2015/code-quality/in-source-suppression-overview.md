---
title: 在源中禁止显示概述 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
helpviewer_keywords:
- source suppression, code analysis
- code analysis, source suppression
ms.assetid: f1a2dc6a-a9eb-408c-9078-2571e57d207d
caps.latest.revision: 42
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 63d405b0e62735c0c1e3d7bb716ea2db29bc19fe
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72651577"
---
# <a name="in-source-suppression-overview"></a>“源代码中禁止显示”概述
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在源代码中禁止显示，通过将**SuppressMessage**属性添加到导致冲突的代码段中，可以取消或忽略托管代码中的代码分析冲突。 仅当在编译时定义了 CODE_ANALYSIS 编译符号时， **SuppressMessage**属性才会包含在托管代码程序集的 IL 元数据中。

 在 C++/CLI 中，在头文件中使用宏 CA_SUPPRESS_MESSAGE 或 CA_GLOBAL_SUPPRESS_MESSAGE 来添加特性。

 不应在发布版本中使用源内禁止显示，以防止意外发送源中禁止显示元数据。 由于源中禁止显示的处理开销，因此还可以通过包含源中禁止显示的元数据来降低应用程序的性能。

> [!NOTE]
> 无需自行编写这些属性的代码。 有关详细信息，请参阅[如何：使用菜单项禁止显示警告](../code-quality/how-to-suppress-warnings-by-using-the-menu-item.md)。 菜单项不能用于C++代码。

## <a name="suppressmessage-attribute"></a>SuppressMessage 特性
 如果右键单击 "**错误列表**中的" 代码分析 "警告，然后单击"**禁止显示消息**"，则会在代码或项目的全局禁止显示文件中添加**SuppressMessage**特性。

 **SuppressMessage**属性采用以下格式：

```vb
<Scope:SuppressMessage("Rule Category", "Rule Id", Justification = "Justification", MessageId = "MessageId", Scope = "Scope", Target = "Target")>
```

```csharp
[Scope:SuppressMessage("Rule Category", "Rule Id", Justification = "Justification", MessageId = "MessageId", Scope = "Scope", Target = "Target")]

```

 [C++]

```
CA_SUPPRESS_MESSAGE("Rule Category", "Rule Id", Justification = "Justification", MessageId = "MessageId", Scope = "Scope", Target = "Target")

```

 其中：

- **规则类别**-定义规则的类别。 有关代码分析规则类别的详细信息，请参阅[托管代码的代码分析警告](../code-quality/code-analysis-for-managed-code-warnings.md)。

- **规则 Id** -规则的标识符。 支持包括规则标识符的短名称和长名称。 短名称为 CAXXXX;长名称为 CAXXXX： FriendlyTypeName。

- **对齐**-用于记录取消消息原因的文本。

- **消息 Id** -每个消息的问题的唯一标识符。

- **作用域**-要禁止显示警告的目标。 如果未指定目标，则将其设置为属性的目标。 支持的范围包括：

  - 模块

  - Namespace

  - 资源

  - 键入

  - 成员

- **目标**-用于指定取消警告的目标的标识符。 它必须包含完全限定的项目名称。

## <a name="suppressmessage-usage"></a>SuppressMessage 用法
 在应用**SuppressMessage**属性的实例的级别上，会禁止显示代码分析警告。 这样做的目的是将抑制信息紧密地耦合到发生冲突的代码中。

 抑制的一般形式包括规则类别和规则标识符，其中包含可选的规则名称的可读表示形式。 例如，应用于对象的

 `[SuppressMessage("Microsoft.Design", "CA1039:ListsAreStrongTyped")]`

 如果由于最大程度地减少了源中禁止显示元数据的性能原因，则可以省略规则名称本身。规则类别及其规则 ID 共同构成了一个足够唯一的规则标识符。 例如，应用于对象的

 `[SuppressMessage("Microsoft.Design", "CA1039")]`

 由于可维护性问题，不建议使用此格式。

## <a name="suppressing-multiple-violations-within-a-method-body"></a>禁止在方法体内发生多个冲突
 特性只能应用于方法，不能嵌入方法体。 不过，您可以将标识符指定为消息 ID，以区分方法中出现冲突的多个情况。

 [!code-cpp[InSourceSuppression#1](../snippets/cpp/VS_Snippets_CodeAnalysis/InSourceSuppression/cpp/insourcesuppression.cpp#1)]
 [!code-csharp[InSourceSuppression#1](../snippets/csharp/VS_Snippets_CodeAnalysis/InSourceSuppression/cs/InSourceSuppression.cs#1)]
 [!code-vb[InSourceSuppression#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/InSourceSuppression/vb/InSourceSuppression.vb#1)]

## <a name="generated-code"></a>生成的代码
 托管代码编译器和一些第三方工具生成代码，以加速代码开发。 出现在源文件中的编译器生成的代码通常用**system.codedom.compiler.generatedcodeattribute> 开头**特性标记。

 您可以选择是否取消生成代码的代码分析警告和错误。 有关如何禁止显示这些警告和错误的信息，请参阅[如何：取消显示生成代码的警告](../code-quality/how-to-suppress-code-analysis-warnings-for-generated-code.md)。

 请注意，当应用于整个程序集或单个参数时，代码分析将忽略**system.codedom.compiler.generatedcodeattribute> 开头**。 这种情况很少发生。

## <a name="global-level-suppressions"></a>全局禁止显示
 托管代码分析工具将检查应用于程序集、模块、类型、成员或参数级别的**SuppressMessage**特性。 它还会对资源和命名空间引发冲突。 必须在全局级别应用这些冲突，并确定其作用域和目标。 例如，以下消息取消了命名空间冲突：

 `[module: SuppressMessage("Microsoft.Design", "CA1020:AvoidNamespacesWithFewTypes", Scope = "namespace", Target = "MyNamespace")]`

> [!NOTE]
> 当您禁止显示带有命名空间范围的警告时，它将禁止显示针对命名空间本身的警告。 它不会禁止对命名空间中的类型发出警告。

 任何禁止显示都可以通过指定显式范围来表示。 这些禁止显示必须位于全局级别。 不能通过修饰类型来指定成员级禁止显示。

 全局级别禁止显示引用编译器生成的代码的消息，这些消息不会映射到显式提供的用户源。 例如，下面的代码针对编译器发出的构造函数禁止发生冲突：

 `[module: SuppressMessage("Microsoft.Design", "CA1055:AbstractTypesDoNotHavePublicConstructors", Scope="member", Target="Microsoft.Tools.FxCop.Type..ctor()")]`

> [!NOTE]
> 目标始终包含完全限定的项目名称。

## <a name="global-suppression-file"></a>全局禁止显示文件
 全局禁止显示文件维护全局级禁止显示或未指定目标的禁止显示的禁止显示。 例如，程序集级别冲突的禁止显示存储在此文件中。 此外，某些 ASP.NET 禁止显示文件存储在此文件中，因为项目级设置不适用于窗体的代码。 第一次在 "错误列表" 窗口中的 "**禁止显示消息**" 命令的 "**项目禁止显示文件**" 选项中，会创建全局禁止显示并将其添加到项目。 有关详细信息，请参阅[如何：使用菜单项禁止显示警告](../code-quality/how-to-suppress-warnings-by-using-the-menu-item.md)。

## <a name="see-also"></a>请参阅
 <xref:System.Diagnostics.CodeAnalysis>
