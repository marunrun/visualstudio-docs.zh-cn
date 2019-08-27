---
title: T4 文本模板编写准则
ms.date: 11/04/2016
ms.topic: conceptual
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ce316f87e47a7846fc30f480c8e2bf197f38051d
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62993463"
---
# <a name="guidelines-for-writing-t4-text-templates"></a>T4 文本模板编写准则

这些常规准则可能会有帮助，如果在 Visual Studio 中生成程序代码或其他应用程序资源。 它们不被固定的规则。

## <a name="guidelines-for-design-time-t4-templates"></a>设计时 T4 模板的指导原则

设计时 T4 模板是模板，在设计时在 Visual Studio 项目中生成代码。 有关详细信息，请参阅[使用 T4 文本模板生成设计时代码](../modeling/design-time-code-generation-by-using-t4-text-templates.md)。

生成的应用程序的可变方面。

代码生成是最适用于这些方面可能会更改该项目，或将更改应用程序的不同版本之间的应用程序。 这些变量部分分开更固定的方面，以便可以更轻松地确定必须为其生成的内容。 例如，如果你的应用程序提供了一个网站，单独的标准页面服务定义到另一个页面中的导航路径的逻辑函数。

对一个或多个源模型中的变量部分进行编码。

模型是代码的文件或数据库的每个模板都可以读取以获得要生成的可变部分的特定值。 模型可以是数据库、 设计、 关系图或域特定语言的 XML 文件。 通常情况下，一个模型用于 Visual Studio 项目中生成多个文件。 从单独的模板生成每个文件。

在项目中，可以使用多个模型。 例如，可以定义 web 页和页的布局的单独的模型之间的导航模型。

将模型的侧重点上用户的需求和词汇、 不关注您的实现。

例如，在网站应用程序中，将希望模型来指代网页和超链接。

理想情况下，选择适合的模型表示的信息种类的演示文稿的窗体。 例如，通过网站的导航路径的模型可能是框和箭头的关系图。

测试生成的代码。

使用手动或自动测试来验证生成的代码按用户所需的正常工作。 避免从同一模型从其生成的代码生成测试。

在某些情况下，可以直接对模型执行一般测试。 例如，可以编写一个测试，以便可确保从任何其他的导航可以访问的网站中的每一页。

允许自定义代码： 生成分部类。

允许您手动编写此外到生成的代码的代码。 很少的代码生成架构，以便能够应对可能出现的所有可能变体。 因此，你应该会添加到或重写某些生成的代码。 其中生成的材料是一种.NET 语言在如C#或 Visual Basic 中，两种策略是特别有用：

- 生成的类应为部分。 这样可以将内容添加到生成的代码。

- 应在对，继承自另一个中生成类。 所有生成的方法和属性，应包含类的基类和派生的类应包含仅的构造函数。 这允许您手动编写的代码以重写任何生成的方法。

在 XML 等其他生成语言，使用`<#@include#>`指令以使手动编写和生成内容的简单组合。 在更复杂的情况下，可能需要编写结合了手动编写的任何文件与生成的文件的后续处理步骤。

将通用材料移动到包含文件或运行时模板。

若要避免重复类似的文本块和多个模板中的代码，使用`<#@ include #>`指令。 有关详细信息，请参阅[T4 包含指令](../modeling/t4-include-directive.md)。

您可以还生成一个单独的项目中的运行时文本模板，然后从设计时模板调用它们。 若要执行此操作，请使用`<#@ assembly #>`指令以访问单独的项目。

请考虑将较大的代码块移动到单独的程序集。

如果有大型代码块和类功能块时，可能会将此代码的一些移动到在一个单独的项目进行编译的方法很有用。 可以使用`<#@ assembly #>`指令来访问模板中的代码。 有关详细信息，请参阅[T4 程序集指令](../modeling/t4-assembly-directive.md)。

可以将方法放在该模板可以继承一个抽象类。 抽象类必须继承<xref:Microsoft.VisualStudio.TextTemplating.TextTransformation?displayProperty=fullName>。 有关详细信息，请参阅[T4 模板指令](../modeling/t4-template-directive.md)。

生成代码，而不配置文件。

编写变量的应用程序的一种方法是编写接受配置文件的一般程序代码。 以这种方式编写的应用程序非常灵活，并可在业务需求变化，而无需重新生成应用程序时重新配置。 但是，此方法的缺点是应用程序将执行效果不如更具体的应用程序。 此外，其程序代码将更难以阅读和维护，部分原因是因为它始终都不得不面临的最通用类型。

与此相反，其变量部分会在编译之前生成的应用程序可以为强类型。 这样，就更容易、 更可靠地编写手动编写代码，并将其与生成集成的软件的部分。

若要获取代码生成的全部优势，请尝试生成程序代码而不是配置文件。

使用生成的代码的文件夹。

将模板和生成的文件放在名为的项目文件夹**生成的代码**若要让其清除，这不应直接编辑的文件。 如果创建自定义代码来覆盖或添加到生成的类，请将这些类放在名为的文件夹**自定义代码**。 典型的项目的结构如下所示：

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

## <a name="guidelines-for-run-time-preprocessed-t4-templates"></a>运行时 （预处理过的） T4 模板的指导原则

将通用材料移到继承的模板。

可以使用继承共享方法和 T4 文本模板之间的文本块。 有关详细信息，请参阅[T4 模板指令](../modeling/t4-template-directive.md)。

此外可以使用包含具有运行时模板的文件。

将太多的代码移入一个分部类。

每个运行时模板生成一个具有与模板相同的名称的分部类定义。 可以编写一个文件，其中包含同一个类的另一个分部定义。 可以将方法、 字段和构造函数添加到这种方式中的类。 可以从模板中的代码块中调用这些成员。

执行此操作的一个优点是代码更易编写，因为 IntelliSense 可用。 此外，您可以获得更好地分离演示文稿和的基本逻辑。

例如，在**MyReportText.tt**:

`The total is: <#= ComputeTotal() #>`

在中**MyReportText Methods.cs**:

`private string ComputeTotal() { ... }`

允许自定义代码： 提供扩展点。

请考虑生成中的虚拟方法\<#+ 类功能块 #>。 这允许单个模板可以在无需修改许多上下文中使用。 而不是修改的模板，可以构造在派生的类提供的最小的其他逻辑。 在派生的类可以是常规的代码，也可以是运行时模板。

例如，在 MyStandardRunTimeTemplate.tt:

```
This page is copyright <#= CompanyName() #>.
<#+ protected virtual string CompanyName() { return ""; } #>
```

在应用程序的代码：

```
class FabrikamTemplate : MyStandardRunTimeTemplate
{
  protected override string CompanyName() { return "Fabrikam"; }
}
...
  string PageToDisplay = new FabrikamTemplate().TextTransform();
```

## <a name="guidelines-for-all-t4-templates"></a>对于所有 T4 模板的指导原则

从文本生成的单独数据收集。

尽量避免混合计算和文本块。 在每个文本模板中，使用第一个\<# 代码块 #> 若要设置变量并执行复杂计算。 从模板或第一个末尾到第一个文本块\<#+ 类功能块 #>、 避免长表达式，并避免循环和条件语句，除非它们包含文本块。 这种做法使模板更轻松地阅读和维护。

不要使用`.tt`包含文件。

使用不同的文件扩展名，例如`.ttinclude`包含文件。 使用`.tt`仅为你想要的文件处理为运行时或设计时文本模板。 在某些情况下，Visual Studio 能够识别`.tt`文件，并自动设置其属性以进行处理。

以固定的原型中启动每个模板。

编写你想要生成，并确保它是正确的代码或文本的示例。 然后将其扩展名更改为.tt 和以增量方式插入通过读取模型修改内容的代码。

请考虑使用类型化的模型。

虽然可以为您的模型创建的 XML 或数据库架构，可能会很有用，若要创建域特定语言 (DSL)。 DSL 的优点它生成一个类来表示架构和属性来表示属性中的每个节点。 这意味着，您可以依据业务模型进行编程。 例如：

```
Team Members:
<# foreach (Person p in team.Members)
 { #>
    <#= p.Name #>
<# } #>
```

请考虑对您的模型使用关系图。

最有效地显示和尤其是当它们非常大，只需作为文本表管理多个模型。

但是，对于某些类型的业务要求，务必要阐明复杂的关系和工作流、 集和关系图是最适合的介质。 关系图的一个优点是很容易地与用户和其他利益干系人一起讨论。 通过从级别的业务需求模型生成代码，可以将你的代码更灵活在需求变化时。

此外可以作为域特定语言 (DSL) 来设计自己的关系图的类型。 可以从 UML 和 Dsl 生成代码。 有关详细信息，请参阅[分析和建模体系结构](../modeling/analyze-and-model-your-architecture.md)。

## <a name="see-also"></a>请参阅

- [使用 T4 文本模板生成设计时代码](../modeling/design-time-code-generation-by-using-t4-text-templates.md)
- [使用 T4 文本模板的运行时文本生成](../modeling/run-time-text-generation-with-t4-text-templates.md)