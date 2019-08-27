---
title: 源代码中禁止显示概述 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
helpviewer_keywords:
- source suppression, code analysis
- code analysis, source suppression
ms.assetid: f1a2dc6a-a9eb-408c-9078-2571e57d207d
caps.latest.revision: 42
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: cb2b23dcc01d90bc4365c7d5673e6232229b8d3e
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2019
ms.locfileid: "67825990"
---
# <a name="in-source-suppression-overview"></a>“源代码中禁止显示”概述
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在源代码中禁止显示是能够禁止显示或通过添加忽略托管代码中的代码分析冲突**SuppressMessage**属性会导致冲突的代码段。 **SuppressMessage**属性是 conditional 特性在编译时定义 CODE_ANALYSIS 编译符号，才包含在托管的代码程序集的 IL 元数据。  
  
 在 C++/CLI 中，在头文件中使用宏 CA_SUPPRESS_MESSAGE 或 CA_GLOBAL_SUPPRESS_MESSAGE 来添加特性。  
  
 不应在发布版本使用在源代码中禁止显示以防止意外地传送在源代码中禁止显示元数据。 由于在源代码中禁止显示的处理成本，还通过包括在源代码中禁止显示元数据降低应用程序的性能。  
  
> [!NOTE]
> 您不需要亲自为手动代码这些属性。 有关详细信息，请参阅[如何：使用菜单项禁止显示警告](../code-quality/how-to-suppress-warnings-by-using-the-menu-item.md)。 菜单项不是可用于C++代码。  
  
## <a name="suppressmessage-attribute"></a>SuppressMessage 特性  
 右键单击中的代码分析警告时**错误列表**，然后单击**禁止显示消息**即**SuppressMessage**在代码中或为添加属性项目的全局禁止显示文件。  
  
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
  
- **规则类别**-定义了该规则的类别。 有关代码分析规则类别的详细信息，请参阅[的代码分析托管代码警告](../code-quality/code-analysis-for-managed-code-warnings.md)。  
  
- **规则 Id** -规则的标识符。 支持包括以上两个规则标识符的短期和长期名称。 短名称是 CAXXXX;长名称是 CAXXXX:FriendlyTypeName。  
  
- **理由**-用于记录取消消息的规则的原因的文本。  
  
- **消息 Id** -为每个消息问题的唯一标识符。  
  
- **作用域**-取消该警告的目标。 如果未指定目标，则将它设置为属性的目标。 受支持的作用域包括：  
  
  - 模块  

  - 命名空间  

  - 资源  

  - 类型  

  - 成员  
  
- **目标**-用于取消该警告将目标指定的标识符。 它必须包含完全限定的项名称。  
  
## <a name="suppressmessage-usage"></a>SuppressMessage 使用情况  
 在向其级别禁止显示代码分析警告的实例**SuppressMessage**应用属性。 这样做的目的是紧密耦合到代码的禁止显示信息发生冲突。  
  
 禁止显示的一般形式包括规则类别和其中包含的规则名称的可选用户可读表示形式的规则标识符。 例如，应用于对象的  
  
 `[SuppressMessage("Microsoft.Design", "CA1039:ListsAreStrongTyped")]`  
  
 如果有严格的性能的最大程度减少在源代码中禁止显示元数据的原因，可以省略规则名称本身。规则类别和其规则 ID 一起构成足够唯一的规则标识符。 例如，应用于对象的  
  
 `[SuppressMessage("Microsoft.Design", "CA1039")]`  
  
 由于可维护性问题，不建议使用此格式。  
  
## <a name="suppressing-multiple-violations-within-a-method-body"></a>禁止显示方法体中的多个冲突  
 属性仅应用于方法，不能在方法体中嵌入。 但是，您可以指定标识符作为要区分多个出现的冲突的方法内的消息 ID。  
  
 [!code-cpp[InSourceSuppression#1](../snippets/cpp/VS_Snippets_CodeAnalysis/InSourceSuppression/cpp/insourcesuppression.cpp#1)]
 [!code-csharp[InSourceSuppression#1](../snippets/csharp/VS_Snippets_CodeAnalysis/InSourceSuppression/cs/InSourceSuppression.cs#1)]
 [!code-vb[InSourceSuppression#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/InSourceSuppression/vb/InSourceSuppression.vb#1)]  
  
## <a name="generated-code"></a>生成的代码  
 托管的代码编译器和一些第三方工具生成代码以加快代码的开发。 在源文件中出现的编译器生成的代码通常标有**GeneratedCodeAttribute**属性。  
  
 您可以选择是否要取消显示代码分析警告和错误生成的代码。 有关如何禁止显示此类警告和错误的信息，请参阅[如何：禁止显示生成的代码的警告](../code-quality/how-to-suppress-code-analysis-warnings-for-generated-code.md)。  
  
 请注意，代码分析忽略了**GeneratedCodeAttribute**时应用于整个程序集或单个参数。 这种情况下很少发生。  
  
## <a name="global-level-suppressions"></a>全局级禁止显示  
 托管的代码分析工具可检查**SuppressMessage**应用于程序集、 模块、 类型、 成员或参数级别的属性。 它还会激发针对资源和命名空间冲突。 必须在全局级别应用这些冲突作用域和有针对性。 例如，以下消息禁止显示命名空间冲突：  
  
 `[module: SuppressMessage("Microsoft.Design", "CA1020:AvoidNamespacesWithFewTypes", Scope = "namespace", Target = "MyNamespace")]`  
  
> [!NOTE]
> 禁止显示警告，其中包含命名空间范围内时，它将阻止对自身的命名空间的警告。 它不会取消该警告针对在命名空间内的类型。  
  
 可以通过指定显式作用域表示任何禁止显示。 在全局级别还必须遵循这些禁止显示。 不能通过修饰类型来指定成员级禁止显示。  
  
 全局级禁止显示是唯一的方法来禁止显示编译器生成的代码未映射到显式提供的用户源是指的消息。 例如，以下代码取消针对编译器发出的构造函数冲突：  
  
 `[module: SuppressMessage("Microsoft.Design", "CA1055:AbstractTypesDoNotHavePublicConstructors", Scope="member", Target="Microsoft.Tools.FxCop.Type..ctor()")]`  
  
> [!NOTE]
> 目标始终包含完全限定的项名称。  
  
## <a name="global-suppression-file"></a>全局禁止显示文件  
 全局禁止显示文件维护全局级禁止显示或不指定目标的禁止显示的禁止显示。 例如，禁止显示的程序集级别冲突存储在该文件中。 此外，某些 ASP.NET 禁止显示存储在此文件中，是因为项目级别设置不可用于窗体背后的代码。 全局禁止显示被创建并添加到你的项目选择第一次**在项目禁止显示文件**的选项**禁止显示消息**命令，在错误列表窗口。 有关详细信息，请参阅[如何：使用菜单项禁止显示警告](../code-quality/how-to-suppress-warnings-by-using-the-menu-item.md)。  
  
## <a name="see-also"></a>请参阅  
 <xref:System.Diagnostics.CodeAnalysis>
