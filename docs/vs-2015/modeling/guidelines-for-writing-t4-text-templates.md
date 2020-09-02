---
title: 用于编写 T4 文本模板的准则 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
ms.assetid: 04dd3fc4-10e8-488a-bdea-4d615f50f063
caps.latest.revision: 11
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: d1e15a8c00a0614d020defd2df7b06665289a8b2
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "72666055"
---
# <a name="guidelines-for-writing-t4-text-templates"></a>T4 文本模板编写准则
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

如果在中生成程序代码或其他应用程序资源，则这些常规指南可能会很有帮助 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 。 它们不是固定的规则。

## <a name="guidelines-for-design-time-t4-templates"></a>设计时 T4 模板指南
 设计时 T4 模板是在设计时在项目中生成代码的模板 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 。 有关详细信息，请参阅 [使用 T4 文本模板生成设计时代码](../modeling/design-time-code-generation-by-using-t4-text-templates.md)。

 生成应用程序的可变因素。
对于在项目中可能会发生更改的应用程序的这些方面，或在不同版本的应用程序之间更改，代码生成最有用。 将这些变量方面与更固定的方面分开，以便您可以更轻松地确定需要生成的内容。 例如，如果您的应用程序提供了一个网站，则将用于提供函数的标准页与定义从一页到另一页的导航路径的逻辑分离。

 对一个或多个源模型中的变量方面进行编码。
模型是每个模板读取的文件或数据库，用于获取要生成的代码的变量部分的特定值。 模型可以是数据库、自己设计的 XML 文件，也可以是特定于域的语言。 通常，一种模型用于在项目中生成许多文件 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 。 每个文件都是从单独的模板生成的。

 可以在一个项目中使用多个模型。 例如，您可以定义一个模型，以便在网页之间导航，并为页面布局定义单独的模型。

 使模型专注于用户的需求和词汇，而不是实现。
例如，在网站应用程序中，您可能希望模型引用网页和超链接。

 理想情况下，选择一种适合该模型所代表的信息类型的表示形式。 例如，通过网站的导航路径模型可能是一个框和箭头的关系图。

 测试生成的代码。
使用手动或自动测试来验证生成的代码是否按用户要求工作。 避免从生成代码的同一模型生成测试。

 在某些情况下，一般测试可以直接在模型上执行。 例如，你可以编写一个测试，以确保网站中的每个页面都可以通过导航从任何其他页面访问。

 允许自定义代码：生成分部类。
除生成的代码外，还允许使用自己编写的代码。 代码生成方案不太常见，因为这种情况可能会导致可能出现的所有变体。 因此，您应该会希望添加或重写某些生成的代码。 如果生成的材料采用 .NET 语言（如 [!INCLUDE[csprcs](../includes/csprcs-md.md)] 或 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] ），则两个策略特别有用：

- 生成的类应为分部类。 这使您可以将内容添加到生成的代码中。

- 类应成对生成，其中一个继承自另一个。 基类应包含所有生成的方法和属性，并且派生类应仅包含构造函数。 这允许手写代码重写任何生成的方法。

  在其他生成的语言（如 XML）中，使用 `<#@include#>` 指令进行手写写入和生成内容的简单组合。 在更复杂的情况下，您可能需要编写一个将生成的文件与任何手写文件组合在一起的后处理步骤。

  将常见材料移到包含文件或运行时模板中，以避免在多个模板中重复使用类似的文本和代码块，请使用 `<#@ include #>` 指令。 有关详细信息，请参阅 [T4 Include 指令](../modeling/t4-include-directive.md)。

  您还可以在单独的项目中生成运行时文本模板，然后从设计时模板调用它们。 为此，请使用 `<#@ assembly #>` 指令访问单独的项目。

  请考虑将大代码块移到单独的程序集中。
  如果有较大的代码块和类功能块，则将此代码移到在单独的项目中编译的方法可能会很有用。 您可以使用 `<#@ assembly #>` 指令访问模板中的代码。 有关详细信息，请参阅 [T4 Assembly 指令](../modeling/t4-assembly-directive.md)。

  您可以将这些方法放在模板可继承的抽象类中。 抽象类必须继承自 <xref:Microsoft.VisualStudio.TextTemplating.TextTransformation?displayProperty=fullName> 。 有关详细信息，请参阅 [T4 模板指令](../modeling/t4-template-directive.md)。

  生成代码，而不是配置文件编写变量应用程序的一种方法是编写可接受配置文件的通用程序代码。 以这种方式编写的应用程序非常灵活，可以在业务需求改变时重新配置该应用程序，而无需重新生成应用程序。 但是，这种方法的缺点是应用程序的性能要低于更为具体的应用程序。 此外，它的程序代码将更难读取和维护，部分原因是它始终处理最常见的类型。

  与此相反，在编译之前生成变量部分的应用程序可以进行强类型化。 这使得编写手写代码以及将其与软件的生成部分进行集成更为简单、可靠。

  若要充分利用代码生成，请尝试生成程序代码而不是配置文件。

  使用生成的代码文件夹将模板和生成的文件放置在一个名为 " **生成的代码**" 的项目文件夹中，以确保它们不是应直接编辑的文件。 如果创建自定义代码来重写或添加到生成的类，请将这些类放在名为 " **自定义代码**" 的文件夹中。 典型项目的结构如下所示：

```
MyProject
   Custom Code
      Class1.cs
      Class2.cs
   Generated Code
      Class1.tt
          Class1.cs
      Class2.tt
          Class2.cs
   AnotherClass.cs

```

## <a name="guidelines-for-run-time-preprocessed-t4-templates"></a>运行时 (预处理) T4 模板的准则
 将常见材料移到继承的模板中可以使用继承在 T4 文本模板之间共享方法和文本块。 有关详细信息，请参阅 [T4 模板指令](../modeling/t4-template-directive.md)。

 还可以使用包含运行时模板的包含文件。

 将大型代码体移到分部类中。
每个运行时模板生成一个与模板同名的分部类定义。 你可以编写包含同一类的另一个分部定义的代码文件。 可以通过这种方式将方法、字段和构造函数添加到类。 这些成员可以从模板的代码块中调用。

 这样做的一个优点是代码更易于编写，因为 IntelliSense 可用。 此外，您还可以在演示和基础逻辑之间实现更好的隔离。

 例如，在 **MyReportText.tt**中：

 `The total is: <#= ComputeTotal() #>`

 在 **MyReportText-Methods.cs**中：

 `private string ComputeTotal() { ... }`

 允许自定义代码：提供扩展点考虑在中生成虚方法 \<#+ class feature blocks #> 。 这允许在许多上下文中使用单个模板，而无需修改。 您可以构造一个提供最少附加逻辑的派生类，而不是修改模板。 派生类可以是常规代码，也可以是运行时模板。

 例如，在 MyStandardRunTimeTemplate.tt 中：

```
This page is copyright <#= CompanyName() #>.
<#+ protected virtual string CompanyName() { return ""; } #>
```

 在应用程序的代码中：

```
class FabrikamTemplate : MyStandardRunTimeTemplate
{
  protected override string CompanyName() { return "Fabrikam"; }
}
...
  string PageToDisplay = new FabrikamTemplate().TextTransform();

```

## <a name="guidelines-for-all-t4-templates"></a>所有 T4 模板的准则
 从文本生成中单独收集数据会尝试避免混合计算和文本块。 在每个文本模板中，使用第一个 \<# code block #> 设置变量并执行复杂的计算。 从第一个文本块到模板末尾或第一个文本块 \<#+ class feature block #> ，避免出现长表达式，并避免循环和条件，除非它们包含文本块。 这种做法使模板更易于阅读和维护。

 不要 `.tt` 对包含文件使用其他文件扩展名，例如 `.ttinclude` 用于包含文件的。 `.tt`仅对要作为运行时或设计时文本模板处理的文件使用。 在某些情况下 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ， `.tt` 会识别文件并自动设置其属性以进行处理。

 以固定原型的形式启动每个模板。
编写要生成的代码或文本的示例，并确保其正确无误。 然后，将其扩展更改为 tt，并以增量方式插入通过读取模型修改内容的代码。

 请考虑使用类型化模型。
尽管可以为模型创建 XML 架构或数据库架构，但创建域特定语言 (DSL) 可能会很有用。 DSL 的优点在于，它会生成一个类来表示架构中的每个节点，并使用属性来表示属性。 这意味着您可以根据业务模式进行编程。 例如：

```
Team Members:
<# foreach (Person p in team.Members)
 { #>
    <#= p.Name #>
<# } #>
```

 请考虑使用模型的关系图。
许多模型最有效地显示并作为文本表进行管理，尤其是在它们非常大的情况下。

 但是，对于某些类型的业务要求，澄清复杂的关系和工作流集很重要，关系图是最适合的媒介。 关系图的优点是可以轻松地与用户和其他利益干系人进行讨论。 通过从模型中生成代码来满足业务要求，可以在需求改变时使代码更灵活。

 UML 类和活动图通常可用于实现这些目的。 你还可以将自己的关系图类型设计为域特定语言 (DSL) 。 可从 UML 和 Dsl 生成代码。 有关详细信息，请参阅对体系结构进行 [分析和建模](../modeling/analyze-and-model-your-architecture.md) 、 [分析和建模](../modeling/analyze-and-model-your-architecture.md)。

## <a name="see-also"></a>另请参阅
 [使用 t4 文本模板生成设计时代码生成](../modeling/design-time-code-generation-by-using-t4-text-templates.md)使用 [T4 文本模板生成运行时文本](../modeling/run-time-text-generation-with-t4-text-templates.md)
