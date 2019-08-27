---
title: 从 UML 类图生成代码 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
f1_keywords:
- vs.teamarch.logicalclassdiagram.shapes.properties.Templates
- vs.teamarch.logicalclassdiagram.shapes.properties.Templates.TextTransformationDataCollectionEditor
helpviewer_keywords:
- code generation, UML class diagrams
- class diagrams - UML, generating code
- UML diagrams, generating code
ms.assetid: 2790e64d-7728-4c2e-a4dd-4131e795f730
caps.latest.revision: 53
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 23cefa3d072c2e582237152bff77a2271046053d
ms.sourcegitcommit: 2da366ba9ad124366f6502927ecc720985fc2f9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68871833"
---
# <a name="generate-code-from-uml-class-diagrams"></a>从 UML 类关系图生成代码
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

若要在C# visual Studio 中从 UML 类图生成 Visual .net 代码, 请使用 "**生成代码**" 命令。 默认情况下，此命令为你选择的每个 UML 类型生成一个 C# 类型。 可以通过修改或复制生成代码的文本模板来修改和扩展此行为。 可以为包含在模型中不同的包中的类型指定不同的行为。

 "**生成代码**" 命令特别适用于从用户选择的元素生成代码, 并为每个 UML 类或其他元素生成一个文件。 例如，屏幕快照显示了已从两个 UML 类生成的两个 C# 文件。

 作为替代方法, 如果想要生成的代码中生成的文件与 UML 元素之间没有1:1 关系, 可以考虑使用 "**转换所有模板**" 命令来编写调用的文本模板。 有关该方法的详细信息, 请参阅[从 UML 模型生成文件](../modeling/generate-files-from-a-uml-model.md)。

 ![UML 类图和生成的&#35; C 类文件。](../modeling/media/oob-gencode1.png "oob_GenCode1")

 有关在 Visual Studio 中的 UML 类关系图的详细信息，请参阅以下主题：

- [UML 类关系图：参考](../modeling/uml-class-diagrams-reference.md)

- [UML 类关系图：指南](../modeling/uml-class-diagrams-guidelines.md)

  若要查看支持 UML 类图的 Visual Studio 版本, 请参阅[体系结构和建模工具的版本支持](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)。

## <a name="using-the-generate-code-command"></a>使用生成代码命令
 以下过程描述了 "**生成代码**" 命令的默认行为:

#### <a name="to-generate-a-separate-file-for-each-element"></a>为每个元素生成一个单独的文件

1. 创建一个包含类的 UML 模型。 你可能希望将构造型应用于模型元素。

    有关详细信息, 请参阅[默认代码生成转换](#default)。

2. 在类图或**UML 模型资源管理器**中, 选择要从其生成代码的元素。 可以选择下列项目之一：

   - 一组特定元素。

   - 一个包或模型，以便从其内容生成代码。

   - 关系图，以便选择关系图上的所有元素。

3. 打开所选元素的快捷菜单, 然后选择 "**生成代码**"。

    首次使用在特定模型中**生成代码**时, 将出现一个对话框。 使用此对话框可以编辑模型的代码生成参数。

    选择 **"确定"** , 除非你知道要更改这些参数。

    若要稍后返回此对话框, 请打开 " **UML 模型资源管理器**"。 打开建模项目快捷菜单, 然后选择 "**设置代码生成**"。 有关详细信息, 请参阅[自定义 "生成代码" 命令](#custom)。

   将生成包含 C# 代码的文件。 默认情况下，为每个类型生成一个文件，这些文件是在 C# 类库项目中生成的。 不过，你可以自定义此行为。 有关详细信息, 请参阅[自定义 "生成代码" 命令](#custom)。

   将一些验证测试应用于模型以确保能将其转换为 C#。 如果这些测试失败，则将显示一条错误消息，并且不执行代码生成操作。 如果你创建了一个验证菜单命令，则不会为其验证命令失败的任何元素生成代码。 有关详细信息, 请参阅为[UML 模型定义验证约束](../modeling/define-validation-constraints-for-uml-models.md)。

## <a name="default"></a>默认代码生成转换
 此部分汇总了 "**生成代码**" 命令生成的结果, 除非自定义该命令。 有关详细信息, 请参阅[自定义 "生成代码" 命令](#custom)。

- 为你在 UML 模型中选择的每个类型生成一个 C# 类型。 每个类型都放置在**GeneratedCode**文件夹下的单独代码文件中。

- 如果 UML 类型包含在包中，则将生成的 C# 类型置于一个命名空间中，并在具有与命名空间相同的名称的文件夹中生成文件。

- 为 UML 类的每个 `Attribute` 生成一个 C# 属性。

- 为 UML 类型的每个 `Operation` 生成一个 C# 方法。

- 为类参与的每个可导航关联生成一个 C# 字段。

  通过向每个 UML 类型添加一个构造型，可以控制生成的 C# 类型的更多属性。

|**创建此C#类型**|**绘制此 UML 类型**|**应用此构造型**|
|---------------------------------|----------------------------|-------------------------------|
|类|类|\<无 > 或<br /><br /> C# class|
|接口|接口|\<无 > 或<br /><br /> C# interface|
|枚举|枚举|\<无 > 或<br /><br /> C# enum|
|委托|类|C# delegate|
|结构|类|C# struct|

#### <a name="to-set-a-stereotype-on-a-type-or-other-element"></a>在类型或其他元素上设置构造型

1. 在关系图或**UML 模型资源管理器**中打开元素的快捷菜单, 然后选择 "**属性**"。

2. 在 "**属性**" 窗口中, 选择 "**构造型**" 属性中的下拉箭头, 然后选中要应用的构造型的复选框。

   > [!TIP]
   > 如果未出现 C# 构造型，则为模型或包含你感兴趣的模型元素的包启用 C# 配置文件。 在 " **UML 模型资源管理器**" 中选择包或模型的根。 然后, 在 "**属性**" 窗口中选择 "**配置文件**" C# , 然后启用配置文件。

3. 展开 "**构造型**" 属性, 以查看可以设置的其他属性。

   类型、特性、操作和关联的**说明**属性将写入`<summary>`生成的代码中的注释。 将链接到类型的注释元素写入 `<remarks>` 注释。

## <a name="varying-the-generated-code"></a>改变生成的代码
 生成的代码随每个类型、特性或操作的属性的不同而不同。 例如, 如果您将类的 "**是" 为 "抽象**" 属性设置为 " `abstract` true", 则关键字将出现在生成的类上。 如果将特性的重**数**设置为**0\*** , 则生成`IEnumerable<>`的属性将具有类型。

 另外，每个构造型提供了多个可设置的附加属性。 这些值将转换为 C# 代码中的相应关键字。 例如，如果你在类上设置属性 `Is Static`，则 C# 类将为 `static`。

 若要设置这些附加属性，请在关系图中选择该类或其他元素。 在属性窗口中, 展开 "**构造型**", 然后C#展开构造型, 如 **C#类**。  对于类，这些附加属性包括：

- CLR Attributes

- Is Partial

- Is Static

- Is Unsafe

- Package Visibility

  每个特性和操作还包含可设置的构造型属性。 如果看不到新属性的属性, 请运行 "**生成代码**"。

## <a name="custom"></a>自定义 "生成代码" 命令
 "**生成代码**" 命令的工作原理是使用一组文本模板来转换模型元素。 有关文本模板的详细信息, 请参阅[代码生成和 T4 文本模板](../modeling/code-generation-and-t4-text-templates.md)。

 模板在一组*文本模板绑定*中指定。 文本模板绑定指定应应用的模板、应放置生成的输出的位置以及 "**生成代码**" 命令的其他参数。

 首次在特定模型上运行 "**生成代码**" 命令时, 它会将一组默认的模板绑定附加到模型的根。 这些绑定应用于模型中的所有元素。

 但是，可以通过将你自己的绑定附加到包、类或其他元素来替代和添加到这些默认绑定。 绑定应用于它将附加到的元素内包含的所有元素。 例如，如果你希望通过一组不同的模板来转换某个特定包内的所有类型，或将这些类型输出到其他文件夹，则可将模板绑定附加到包。

 若要检查附加到模型元素的模板绑定, 请选择属性窗口的 "**文本模板绑定**" 属性中的省略号 **[...]** 。

 "**生成代码**" 命令将模板应用于所选的每个模型元素。 对于每个元素，应用的模板集是附加到其容器（直至并包括模型的根）的模板的组合集。

 如果此集中的两个模板绑定都具有相同的名称，则小型容器中的绑定将替代大型容器中的绑定。 例如, 模型根包含具有 name**类模板**的绑定。 若要将你自己的模板应用于特定包的内容, 请定义具有 name**类模板**的你自己的模板绑定。

 可将多个模板应用于一个模型元素。 可从每个模型元素中生成多个文件。

> [!NOTE]
> 附加到模型的根的绑定将充当模型中所有元素的默认值。 若要查看这些默认绑定, 请打开 " **UML 模型资源管理器**"。 打开建模项目的快捷菜单, 然后选择 "**设置代码生成**"。 或者，在“UML 模型资源管理器”中选择模型的根。 在属性窗口中, 选择 "**文本模板绑定**" 属性中的 " **[...]** "。 在至少使用一次 "**生成代码**" 命令之前, 将不会显示绑定。 无法将模板绑定附加到关系图。

#### <a name="to-attach-text-template-bindings-to-a-package-or-other-model-element"></a>将文本模板绑定附加到包或其他模型元素

1. 在 " **UML 模型资源管理器**" 中, 打开模型元素的快捷菜单, 然后选择 "**属性**"。 通常，你会将文本模板绑定附加到包或模型的根。

2. 在 "**属性**" 窗口中, 选择 "**文本模板绑定**" 属性中的省略号按钮 ("...")。

    此时将显示 "**文本模板绑定**" 对话框。

3. 选择 "**添加**" 以创建新的文本模板绑定。

    \- 或 -

    选择现有绑定以对其进行编辑。

    每个模板绑定均定义了将指定模板应用于所选模型元素以及它包含的其他模型元素的方式。

4. 在该对话框中，设置文本模板绑定的属性。

   |    **Property**    |                                                                                                                                                                                                                                                                                                                    **说明**                                                                                                                                                                                                                                                                                                                    |
   |--------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   |        名称        |                                                                                                                                                                                                                                                  此绑定的名称。 若要替代继承自包含包或模型的某个绑定，请使用与要替代的绑定相同的名称。                                                                                                                                                                                                                                                  |
   |     Overwrite      |                                                                                                                                                                                                                                                                                                      如果为 True，则替代任何现有代码。                                                                                                                                                                                                                                                                                                       |
   |    Target Name     | 生成的文件的名称。<br /><br /> 可以将表达式插入此字符串 (如或`{Name}` `{Owner.Name}`)。 例如, 可以编写: `{Owner.Name}_{Name}`。 在模型元素上计算表达式。 它可使用元素而非方法的属性。 若要查找可以使用的属性, 请查看**VisualStudio\*** 中的类型的属性。 \*\*重要提示\* :\*只能在"**目标名称**" 属性中使用或`{Owner.Name}`。 `{Name}` 若要更改生成的类的名称，你必须修改模板。 有关详细信息, 请参阅[编写文本模板](#writing)。 |
   |    项目路径    |                                                                      指定将包含转换的输出文件的 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 项目的路径。 使用类型值创建新项目。 选择省略号按钮 (" **[...]** ") 以选择现有项目。<br /><br /> 如果新项目不存在，则将创建它。 它将是一个 C# 类库项目。<br /><br /> 为此，你必须直接键入该项目。 可以包含环境变量宏，例如 %ProgramFiles% 或 %LocalAppData%。                                                                       |
   |  目标目录  |                                                                                          在其中生成目标文件的文件夹。 该路径是项目文件夹的相对路径。<br /><br /> 可以使用 `{PackageStructure}` 表达式插入与包含程序包的名称相对应的路径。 默认值为 `\GeneratedCode\{PackageStructure}`。 还可以包含环境变量，例如 %TEMP% 或 %HomePath%。 **重要提示:** `{PackageStructure}`只能在 "**目标目录**" 属性中使用。                                                                                          |
   | 模板文件路径 |                                                                                                                                                           将执行转换的模板。<br /><br /> 可以使用提供的模板或创建你自己的模板。 可在以下位置找到提供的模板：<br /><br /> …\Program Files\Microsoft Visual Studio 12.0\Common7\IDE\Extensions\Microsoft\Architecture Tools\Extensibility\Templates\Text\                                                                                                                                                           |

5. 可将所需数量的绑定附加到一个元素。

## <a name="writing"></a>编写文本模板
 可编写你自己的文本模板。 文本模板可生成程序代码或任何其他类别的文本文件。

 建议你首先修改标准模板的副本。 可从以下位置复制模板：

 …\Program Files\Microsoft Visual Studio 12.0\Common7\IDE\Extensions\Microsoft\Architecture Tools\Extensibility\Templates\Text\

 若要了解文本模板，请参考以下主题。

- 文本模板是生成的文件的原型，它包含生成的文本和读取模型的程序代码。 有关详细信息, 请参阅[代码生成和 T4 文本模板](../modeling/code-generation-and-t4-text-templates.md)。

- 若要在程序代码中导航 UML 模型，你必须使用 UML API。 有关详细信息, 请参阅[导航 uml 模型](../modeling/navigate-the-uml-model.md)和[API 参考, 了解 uml 建模扩展性](../modeling/api-reference-for-uml-modeling-extensibility.md)。

  若要将模板与 "**生成代码**" 命令一起使用, 必须包括建模指令。 例如:

  `<#@ Modeling ElementType="Microsoft.VisualStudio.Uml.Classes.IClass" Processor="ModelingProcessor" #>`

  `ElementType` 特性定义了此模板将应用于的 UML 元素的类型。

  在模板中，`this` 属于具有以下属性的临时类：

- `Element`= 要应用模板的 UML [IElement](/previous-versions/dd516035(v=vs.140)) 。

- `Errors`: <xref:System.CodeDom.Compiler.CompilerErrorCollection>

- `Host`：[ITextTemplatingEngineHost](/previous-versions/visualstudio/visual-studio-2012/bb126505(v=vs.110))

- `ModelBus`：[ModelBus](/previous-versions/ee904639(v=vs.140))。 有关详细信息, 请参阅将[UML 模型与其他模型和工具集成](../modeling/integrate-uml-models-with-other-models-and-tools.md)。

- `ProfileName` =“C#Profile”

- `ServiceProvider`: <xref:System.IServiceProvider>

- `Session`: <xref:Microsoft.VisualStudio.TextTemplating.TextTemplatingSession>。

- `Store`: <xref:Microsoft.VisualStudio.Modeling.Store>。 这是在其上实现 UML ModelStore 的可视化和建模 SDK 存储。 若要获取 UML [IModelStore](/previous-versions/ee789385(v=vs.140)), 请`this.Element.GetModelStore()`使用。

  当你编写文本模板时，你可能会发现以下几点很有用。 [代码生成和 T4 文本模板](../modeling/code-generation-and-t4-text-templates.md)中详细介绍了此信息。

- 可在 `Output` 指令中设置结果的文件扩展名。 每个文本模板中需要一个 `Output` 指令。

- 模板将自动引用某些程序集。 例如，这些程序集包括 System.dll 和 Microsoft.VisualStudio.Uml.Interfaces.dll。

   若要在生成的程序代码中使用其他程序集，你必须使用 `Assembly` 指令。 例如:

   `<#@ Assembly Name="%ProgramFiles%\Microsoft Visual Studio 12.0\Common7\IDE\PublicAssemblies\Microsoft.VisualStudio.ArchitectureTools.Extensibility.dll" #>`

- 一些命名空间（例如，`System`）会自动导入你的程序代码。 对于其他命名空间，可以按使用 `Import` 语句的方式来使用 `using` 指令。 例如:

   `<#@ Import Namespace="Microsoft.VisualStudio.Uml.Classes" #>`

   `<#@ Import Namespace="Microsoft.VisualStudio.ArchitectureTools.Extensibility.Uml" #>`

- 使用 `Include` 指令以引用其他文件的文本。

- 括在括号`<# ... #>`中的模板部件由 "**生成代码**" 命令执行。 括号外部的模板部分将复制到结果文件。 区分生成的代码和生成的文本很重要。 生成的文本可采用任何语言。

- 计算 `<#= Expressions #>` 并将其转换为字符串。

## <a name="see-also"></a>请参阅
 [UML 类关系图：](../modeling/uml-class-diagrams-reference.md) 引用[UML 类图:](../modeling/uml-class-diagrams-guidelines.md) [从 UML 模型生成文件的](../modeling/generate-files-from-a-uml-model.md)准则
