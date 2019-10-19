---
title: 从 UML 模型生成文件 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- UML model, generating files
ms.assetid: 4e28b0e6-ce8f-45ee-9e3a-e4d600a0ad81
caps.latest.revision: 21
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 832dc3f7fea959ff4d2834aba921cd16f1117b5c
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72666147"
---
# <a name="generate-files-from-a-uml-model"></a>从 UML 模型生成文件
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可以从 UML 模型生成程序代码、架构、文档、资源和其他任意类型的项目。 从 UML 模型生成文本文件的一种简便方法是使用[文本模板](../modeling/code-generation-and-t4-text-templates.md)。 这些让你可以将程序代码嵌入到要生成的文本内部。

 有三种主要方案：

- [从菜单命令或笔势生成文件](#Command)。 定义在 UML 模型上可用的 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 命令。

- [从应用程序生成文件](#Application)。 编写读取 UML 模型并生成文件的应用程序。

- [在设计时生成](#Design)。 可使用模型定义应用程序的某些功能，并在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 解决方案中生成代码、资源等。

  本主题最后讨论了[如何使用文本生成](#What)。 有关详细信息，请参阅[代码生成和 T4 文本模板](../modeling/code-generation-and-t4-text-templates.md)。

## <a name="Command"></a>从菜单命令生成文件
 可以在 UML 菜单命令内使用预处理文本模板。 在文本模板的代码中（或在单独的分部类中），可以读取由关系图查看的模型。

 有关这些功能的详细信息，请参阅以下主题：

- [在建模图上定义菜单命令](../modeling/define-a-menu-command-on-a-modeling-diagram.md)

- [使用 T4 文本模板的运行时文本生成](../modeling/run-time-text-generation-with-t4-text-templates.md)

- [导航 UML 模型](../modeling/navigate-the-uml-model.md)

  当从模型关系图之一启动操作时，以下示例中演示的方法适用于从单一模型中生成文本。 若要在单独的上下文中处理模型，请考虑使用[Visual Studio Modelbus](../modeling/integrate-uml-models-with-other-models-and-tools.md)访问模型及其元素。

### <a name="example"></a>示例
 若要运行此示例，请创建 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 扩展 (VSIX) 项目。 在此示例中使用的项目名称是 `VdmGenerator`。 在**source.extension.vsixmanifest**文件中，单击 "**添加内容**"，并将 "类型" 字段设置为 " **MEF 组件**" 和引用当前项目的源路径。 有关如何设置此类型的项目的详细信息，请参阅[在建模图上定义菜单命令](../modeling/define-a-menu-command-on-a-modeling-diagram.md)。

 在项目中添加一个包含以下代码的 C# 文件。 此类定义一个将显示在 UML 类关系图中的菜单命令。

```
using System;
using System.ComponentModel.Composition;
using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Uml;
using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Presentation;
using Microsoft.VisualStudio.Modeling.ExtensionEnablement;

namespace VdmGenerator
{
  [Export(typeof(ICommandExtension))]
  [ClassDesignerExtension]
  public class GenerateVdmFromClasses : ICommandExtension
  {
    [Import] public IDiagramContext DiagramContext { get; set; }
    public void Execute(IMenuCommand command)
    {
      // Initialize the template with the Model Store.
      VdmGen generator = new VdmGen(
             DiagramContext.CurrentDiagram.ModelStore);
      // Generate the text and write it.
      System.IO.File.WriteAllText
        (System.IO.Path.Combine(
            Environment.GetFolderPath(
                Environment.SpecialFolder.Desktop),
            "Generated.txt")
         , generator.TransformText());
    }
    public void QueryStatus(IMenuCommand command)
    {
      command.Enabled = command.Visible = true;
    }
    public string Text
    { get { return "Generate VDM"; } }
  }
}
```

 以下文件为文本模板。 它为模型中的每个 UML 类生成一行文本，并为每个类中的每个特性生成一行文本。 用于读取模型的代码嵌入在文本中，由 `<# ... #>` 分隔。

 若要创建此文件，请在解决方案资源管理器中右键单击项目，指向 "**添加**"，然后单击 "**新建项**"。 选择 "**预处理文本模板**"。 此示例的文件名应为**VdmGen.tt**。 文件的 "**自定义工具**" 属性应为**TextTemplatingFilePreprocessor**。 有关预处理文本模板的详细信息，请参阅[带有 T4 文本模板的运行时文本生成](../modeling/run-time-text-generation-with-t4-text-templates.md)。

```
<#@ import namespace="Microsoft.VisualStudio.Uml.Classes" #>
<#
   foreach (IClass classElement in store.AllInstances<IClass>())   {
#>
Type <#= classElement.Name #> ::
<#
     foreach (IProperty attribute in classElement.OwnedAttributes)     {
#>
       <#= attribute.Name #> : <#=
           attribute.Type == null ? ""
                                  : attribute.Type.Name #>
<#
     }   }
#>
```

 文本模板会生成一个 C# 分部类，此分部类将成为 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 项目的一部分。 在单独的文件中，添加同一类的另一个分部声明。 此代码为模板提供对 UML 模型存储的访问权：

```
using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Uml;
namespace VdmGenerator
{
    public partial class VdmGen
    {
        private IModelStore store;
        public VdmGen(IModelStore s)
        { store = s; }
    }
}
```

 若要测试项目，请按**F5**。 将启动 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 新实例。 在此实例中，打开或创建包含类关系图的 UML 模型。 将某些类添加到关系图，并将某些特性添加到每个类。 右键单击关系图，然后单击示例命令 `Generate VDM`。 命令 `C:\Generated.txt` 创建文件。 检查此文件。 它的内容应与以下文本类似，但它将列出自己的类和特性：

```
Type Class1 ::
          Attribute1 : int
          Attribute2 : string
Type Class2 ::
          Attribute3 : string
```

## <a name="Application"></a>从应用程序生成文件
 可以从读取 UML 模型的应用程序中生成文件。 出于此目的，访问模型及其元素的最灵活、最可靠的方法是[Visual Studio Modelbus](../modeling/integrate-uml-models-with-other-models-and-tools.md)。

 也可以使用基本 API 来加载模型，并使用与上一节中相同的方法将模型传递到文本模板。 有关加载模型的详细信息，请参阅[在程序代码中读取 UML 模型](../modeling/read-a-uml-model-in-program-code.md)。

## <a name="Design"></a>在设计时生成文件
 如果你的项目具有一种可将 UML 解释为代码的标准方法，则可以创建允许你在项目中从 UML 模型生成代码的文本模板。 通常，你会具有一个包含 UML 模型项目以及一个或多个应用程序代码项目的解决方案。 每个代码项目可能会包含若干个模板，这些模板将基于模型的内容生成程序代码、资源和配置文件。 开发人员可以通过单击 "解决方案资源管理器" 工具栏中的 "**转换所有模板**" 来运行所有模板。 程序代码通常以分部类的形式生成，以便于集成手动编写的部分。

 这种类型的 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 项目可通过模板的形式进行分发，以便团队的每个成员都能创建以相同方式从模型生成代码的项目。 通常，模板属于扩展软件包的一部分，而扩展软件包会包含针对模型的验证约束以确保满足生成代码的前置条件。

### <a name="outline-procedure-for-generating-files"></a>用于生成文件的大致过程

- 若要将模板添加到项目，请在 "添加新文件" 对话框中选择 "**文本模板**"。 可以将模板添加到大多数类型的项目中，但不能添加到建模项目中。

- 模板文件的 "自定义工具" 属性应为**TextTemplatingFileGenerator**，文件扩展名应为. tt。

- 模板至少应具有一个输出指令：

     `<#@ output extension=".cs" #>`

     根据项目的语言设置扩展字段。

- 若要允许模板中的生成代码访问模型，请为读取 UML 模型所需的程序集编写 `<#@ assembly #>` 指令。 使用 `ModelingProject.LoadReadOnly()` 打开模型。 有关详细信息，请参阅[在程序代码中读取 UML 模型](../modeling/read-a-uml-model-in-program-code.md)。

- 当你保存模板时，当你单击 "解决方案资源管理器" 工具栏中的 "**转换所有模板**" 时，将执行该模板。

- 有关此类型模板的详细信息，请参阅[使用 T4 文本模板生成设计时代码](../modeling/design-time-code-generation-by-using-t4-text-templates.md)。

- 在典型的项目中，你将具有若干个可从同一模型生成不同文件的模板。 每个模板的第一部分都将相同。 若要减少此重复，请将公共部分移到一个单独的文本文件中，然后通过在每个模板中使用指令 `<#@include file="common.txt"#>` 来调用该文件。

- 你也可以定义一个专用指令处理器，让你在文本生成过程中提供参数 有关详细信息，请参阅[自定义 T4 文本转换](../modeling/customizing-t4-text-transformation.md)。

### <a name="example"></a>示例
 此示例为源模型中的每个 UML 类生成一个 C# 类。

##### <a name="to-set-up-a-visual-studio-solution-for-this-example"></a>针对此示例设置 Visual Studio 解决方案

1. 在新的解决方案的建模项目中创建一个 UML 类图。

   1. 在 "**体系结构**" 菜单中，单击 "**新建关系图**"。

   2. 选择 " **UML 类图**"。

   3. 按照提示创建新的解决方案和建模项目。

   4. 通过从工具箱拖动 UML 类工具，将某些类添加到关系图上。

   5. 保存该文件。

2. 在同一个解决方案中创建一个 C# 或 Visual Basic 项目。

   - 在解决方案资源管理器中，右键单击解决方案，指向 "**添加**"，然后单击 "**新建项目**"。 在 "**已安装的模板**" 下，单击**Visual Basic**或**视觉对象C#，** 然后选择 "**控制台应用程序**" 等项目类型。

3. 将一个纯文本文件添加到 C# 或 Visual Basic 项目中。 此文件将包含你在编写多个文本模板时可共享的代码。

   - 在解决方案资源管理器中，右键单击项目，指向 "**添加**"，然后单击 "**新建项**"。 选择 "**文本文件**"。

     插入下节中显示的文本。

4. 将一个文本模板文件添加到 C# 或 Visual Basic 项目中。

   - 在解决方案资源管理器中，右键单击项目，指向 "**添加**"，然后单击 "**新建项**"。 选择 "**文本模板**"。

     将以下的代码插入到该文本模板文件中。

5. 保存该文本模板文件。

6. 检查附属文件中的代码。 它应包含与模型中的每个 UML 类相对应的类。

   1. 在 Visual Basic 项目中，单击解决方案资源管理器工具栏中的 "**显示所有文件**"。

   2. 在解决方案资源管理器中展开模板文件节点。

#### <a name="content-of-the-shared-text-file"></a>共享文本文件的内容
 在此示例中，文件名为“SharedTemplateCode.txt”，并且位于与文本模板相同的文件夹中。

```
<# /* Common material for inclusion in my model templates */ #>
<# /* hostspecific allows access to the Visual Studio API */ #>
<#@ template debug="false" hostspecific="true" language="C#" #>
<#@ assembly name="Microsoft.VisualStudio.Uml.Interfaces.dll"#>
<#@ assembly name="Microsoft.VisualStudio.ArchitectureTools.Extensibility.dll"#>
<#@ assembly name="EnvDTE" #>
<#@ import namespace="Microsoft.VisualStudio.Uml.Classes" #>
<#@ import namespace="Microsoft.VisualStudio.ArchitectureTools.Extensibility" #>
<#@ import namespace="Microsoft.VisualStudio.ArchitectureTools.Extensibility.Uml" #>
<#+  // Note this is a Class Feature Block
///<summary>
/// Text templates are run in a common AppDomain, so
/// we can cache the model store that we find.
///</summary>
private IModelStore StoreCache
{
  get { return AppDomain.CurrentDomain.GetData("ModelStore") as IModelStore; }
  set { AppDomain.CurrentDomain.SetData("ModelStore", value); }
}
private bool CacheIsOld()
{
    DateTime? dt = AppDomain.CurrentDomain
           .GetData("latestAccessTime") as DateTime?;
    DateTime t = dt.HasValue ? dt.Value : new DateTime();
    DateTime now = DateTime.Now;
    AppDomain.CurrentDomain.SetData("latestAccessTime", now);
    return now.Subtract(t).Seconds > 3;
}

///<summary>
/// Find the UML modeling project in this solution,
/// and load the model.
///</summary>
private IModelStore ModelStore
{
  get
  {
    // Avoid loading the model for every template:
    if (StoreCache == null || CacheIsOld())
    {
      // Use Visual Studio API to find modeling project:
      EnvDTE.DTE dte = (EnvDTE.DTE) ((IServiceProvider) this.Host)
                       .GetService(typeof(EnvDTE.DTE));
      EnvDTE.Project project = null;
      foreach (EnvDTE.Project p in dte.Solution.Projects)
      {
        if (p.FullName.EndsWith(".modelproj"))
        {
          project = p;
          break;
        }
      }
      if (project == null) return null;

      // Load UML model into this AppDomain
      // and access model store:
      IModelingProjectReader reader =
           ModelingProject.LoadReadOnly(project.FullName);
      StoreCache = reader.Store;
    }
    return StoreCache;
  }
}
#>
```

#### <a name="content-of-the-text-template-file"></a>文本模板文件的内容
 以下文本位于**tt**文件中。 此示例基于模型中的 UML 类在 C# 文件中生成类。 但是，你可以生成任意类型的文件。 所生成文件的语言与编写文本模板代码所使用的语言无关。

```
<#@include file="SharedTemplateCode.txt"#>
<#@ output extension=".cs" #>
namespace Test{
<#
      foreach (IClass c in ModelStore.AllInstances<IClass>())
      {
#>
   public partial class <#=c.Name#>
   {   }
<#
      }
#>
}
```

## <a name="What"></a>如何使用文本生成
 当你使用模型在要求或体系结构级别进行设计时，将会发挥建模的真正作用。 可以使用文本模板来执行某些将高级概念转变为代码的工作。 在很多情况下，这不会导致 UML 模型中的元素与程序代码的类或其他部分之间的一一对应关系。

 此外，该转换取决于你的问题域；模型和代码之间没有通用的映射。

 以下是一些从模型生成代码的示例：

- **产品线**。 Fabrikam，Inc. 构建并安装机场行李处理系统。 每次安装的软件的很多内容都是非常类似的，但软件的配置要取决于所安装的行李处理设备以及这些设备通过传送带相互连接的方式。 在订立合同之初，Fabrikam 的分析人员会机场管理人员讨论需求，并使用 UML 活动图制定硬件计划。 基于此模型，开发团队将生成配置文件、程序代码、计划和用户文档。 他们通过手动添加和调整代码来完成工作。 随着他们从一个接一个的作业中获得经验，他们会扩展生成的材料的范围。

- **模式**。 Contoso, Ltd 的开发人员通常构建网站，并使用 UML 类图设计导航方案。 每个网页由一个类表示，而且关联表示导航链接。 开发人员会从模型中生成很多网站代码。 每个网页都对应着若干个类和资源文件项。  此方法具有所构造的每个网页符合单一模式的优势，这比手动编写代码更为可靠和灵活。 当在生成模板中使用模式时，可使用模型捕获变量部分。

- **架构**。 Humongous Insurance 在全球范围内具有数千个系统。 这些系统使用不同的数据库、语言和接口。 中心体系结构团队会在内部发布业务概念和过程的模型。 利用这些模型，本地团队生成各自的数据库和交换架构、程序代码中的声明等。 这些模型的图形表示形式可帮助团队讨论建议。 各团队会创建多个关系图，以显示应用于不同业务领域的模型的子集。 他们还会使用颜色来突出显示可能会有所变化的领域。

## <a name="important-techniques-for-generating-artifacts"></a>生成项目的重要方法
 在前面的示例中，各个模型用于不同的业务相关目的，而且对建模元素（如类和活动）的解释也随应用程序不同而有所变化。 下列方法对于从模型生成项目的情况非常有用。

- **配置文件**。 即使是在同一个业务领域内，元素类型的解释也会有所不同。 例如，在网站关系图上，有些类可能表示网页，而其他类则表示内容块。 为了方便用户记录这些区别，可定义构造型。 利用构造型还可以附加应用于此类元素的其他属性。 构造型打包在配置文件中。 有关详细信息，请参阅[定义用于扩展 UML 的配置文件](../modeling/define-a-profile-to-extend-uml.md)。

     在模板代码中，可以轻松地访问在对象上定义的构造型。 例如:

    ```
    public bool HasStereotype(IClass c, string profile, string stereo)
    { return c.AppliedStereotypes.Any
       (s => s.Profile == profile && s.Name == stereo ); }
    ```

- **约束的模型**。 不是所有可以创建的模型都对每种用途有效。 例如，在 Fabrikam 的机场行李模型中，没有外运输送带的登机手续办理台是错误的。 可以定义验证函数来帮助用户遵循这些约束。 有关详细信息，请参阅为[UML 模型定义验证约束](../modeling/define-validation-constraints-for-uml-models.md)。

- **保留手动更改**。 只有某些解决方案文件才可以从模型中生成。 在大多数情况下，你需要能够手动添加或调整生成内容。 不过，当模板转换再次运行时应保留这些手动更改，这一点很重要。

     如果模板以 [!INCLUDE[TLA2#tla_net](../includes/tla2sharptla-net-md.md)] 语言生成代码，则这些模板应生成分部类，以便开发人员可以添加方法和代码。 成对生成每个类也很有用：一个包含方法的抽象基类和一个只包含构造函数的继承类。 这让开发人员能够重写方法。 若要允许重写初始化，应在单独的方法中（而非构造函数中）完成此操作。

     如果模板生成 XML 和其他类型的输出，则将手动内容与生成的内容保持分离可能会更加困难。 一种方法是在生成过程中创建一个任务，将这两个文件合并在一起。 开发人员可使用的另一种方法是调整生成模板的本地副本。

- **将代码移动到单独的程序集中**。 我们建议不要在模板中编写太多代码。 最好将生成的内容与计算保持分离，文本模板对编辑代码的支持也不是太好。

     不过，如果你必须执行大量计算来生成文本，请在一个单独的程序集中生成这些函数，并从模板中调用其方法。
