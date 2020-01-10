---
title: 为 UML 模型定义验证约束 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- UML model, validation constraints
ms.assetid: 87b3b0da-122d-4121-9318-200c38ff49d0
caps.latest.revision: 49
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 32f249b971e8a37bc5b596203cde6bc7b0bcf6f1
ms.sourcegitcommit: c150d0be93b6f7ccbe9625b41a437541502560f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/10/2020
ms.locfileid: "75849742"
---
# <a name="define-validation-constraints-for-uml-models"></a>为 UML 模型定义验证约束
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

你可以定义测试模型是否符合所指定条件的验证约束。 例如，你可以定义一个约束以确保用户不会创建具有继承关系的循环。 用户尝试打开或保存模型时将调用该约束，此外也可手动调用。 如果约束失效，错误窗口中将增加一条你定义的错误消息。 可以将这些约束打包到 Visual Studio 集成扩展 ([VSIX](https://msdn.microsoft.com/library/dd393694(VS.100).aspx)) 中，并将其分发到其他 Visual Studio 用户。

 你还可以定义对照外部资源（如数据库）验证模型的约束。 如果要针对层关系图验证程序代码，请参阅[向层关系图添加自定义体系结构验证](../modeling/add-custom-architecture-validation-to-layer-diagrams.md)。

 若要查看支持 UML 模式的 Visual Studio 版本，请参阅 [Version support for architecture and modeling tools](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)。

## <a name="requirements"></a>需求
 请参阅 [要求](../modeling/extend-uml-models-and-diagrams.md#Requirements)。

 若要查看支持此功能的 Visual Studio 的版本，请参阅 [Version support for architecture and modeling tools](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)。

## <a name="applying-validation-constraints"></a>应用验证约束
 验证约束适用于三种情况：保存模型时、打开模型时，以及单击“体系结构” 菜单上的“验证 UML 模型” 时。 在每种情况下，将仅应用针对该种情况定义的约束，但通常都会将每个约束定义为适用于多种情况。

 验证错误在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 错误窗口中报告，你可以双击错误以选择存在错误的模型元素。

 有关应用验证的详细信息，请参阅[验证 UML 模型](../modeling/validate-your-uml-model.md)。

## <a name="defining-a-validation-extension"></a>定义验证扩展
 若要为 UML 设计器创建验证扩展，必须创建一个用于定义验证约束的类，并将该类嵌入 Visual Studio 集成扩展 (VSIX) 中。 VSIX 用作可安装该约束的容器。 有两种替代方法可以定义验证扩展：

- **使用项目模板在其自身 VSIX 中创建验证扩展。** 此方法更快。 如果不希望将验证约束与其他类型的扩展（如菜单命令、自定义工具箱项或笔势处理程序）组合在一起，可以采用此方法。 你可以在一个类中定义多个约束。

- **创建单独的验证类和 VSIX 项目。** 如果希望将多种类型的扩展组合到同一个 VSIX 中，可以采用此方法。 例如，如果菜单命令要求模型遵守特定的约束，则可以将该菜单命令作为一种验证方法嵌入同一 VSIX 中。

#### <a name="to-create-a-validation-extension-in-its-own-vsix"></a>若要在其自身 VSIX 中创建验证扩展

1. 在“新建项目” 对话框中，在“建模项目”下，选择“验证扩展”。

2. 在新项目中打开 **.cs** 文件并修改类，以实现验证约束。

    有关详细信息，请参阅 [评估验证约束](#Implementing)。

   > [!IMPORTANT]
   > 请确保你的 **.cs** 文件包含以下 `using` 语句：
   >
   >  `using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Uml;`

3. 你可以通过定义新的方法来添加其他约束。 若要将方法标识为验证方法，必须采用与初始验证方法相同的方式标记其特性。

4. 按 F5 以测试你的约束。 有关详细信息，请参阅 [执行验证约束](#Executing)。

5. 在另一台计算机上安装菜单命令，方法是：将文件 bin 复制\\由项目生成的 **\*\\\*。** 有关详细信息，请参阅 [安装和卸载扩展](#Installing)。

   添加其他 **.cs** 文件时，通常将需要以下 `using` 语句：

```csharp
using System.Collections.Generic;
using System.ComponentModel.Composition;
using System.Linq;
using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Uml;
using Microsoft.VisualStudio.Modeling.Validation;
using Microsoft.VisualStudio.Uml.Classes;

```

 下面是替代过程：

#### <a name="to-create-a-separate-validation-constraint-in-a-class-library-project"></a>在一个类库项目中创建单独的验证约束

1. 创建一个类库项目，将该项目添加到现有 VSIX 解决方案或创建一个新的解决方案。

    1. 在“文件” 菜单上，选择“新建”、“项目”。

    2. 在“已安装的模板”下，展开“Visual C#” 或“Visual Basic”，然后在中间栏中选择“类库”。

2. 除非你的解决方案已经包含一个项目，否则请创建一个 VSIX 项目：

    1. 在“解决方案资源管理器”中，在该解决方案的快捷菜单上依次选择“添加”、“新建项目”。

    2. 在“已安装的模板”下，展开 “Visual C#”或“Visual Basic”，然后选择“扩展性”。 在中间栏中，单击“VSIX 项目”。

3. 将 VSIX 项目设置为解决方案的启动项目。

    - 在“解决方案资源管理器”中，VSIX 项目的快捷菜单上选择“设为启动项目”。

4. 在 **source.extension.vsixmanifest**中，在“内容”下，将类库项目添加为 MEF 组件：

    1. 在“元数据” 选项卡上，设置 VSIX 的名称。

    2. 在“安装目标” 选项卡上，将 Visual Studio 版本设置为目标。

    3. 在“资产” 选项卡上，选择“新建”，并在对话框中进行如下设置：

         **类型** = **MEF 组件**

          = **当前解决方案中的项目**

          = *你的类库项目*

#### <a name="to-define-the-validation-class"></a>定义验证类

1. 如果已经根据验证项目模板创建了具有其自身 VSIX 的验证类，则无需执行此过程。

2. 在验证类项目中，添加对以下 [!INCLUDE[TLA2#tla_net](../includes/tla2sharptla-net-md.md)] 程序集的引用：

     `Microsoft.VisualStudio.Modeling.Sdk.[version]`

     `Microsoft.VisualStudio.ArchitectureTools.Extensibility.Uml`

     `Microsoft.VisualStudio.Uml.Interfaces`

     `System.ComponentModel.Composition`

3. 将文件添加到类库项目，该项目包含类似以下示例的代码。

    - 每个验证约束都包含在标记了特定特性的方法中。 该方法接受模型元素类型的参数。 调用验证时，验证框架将向符合其参数类型的每个模型元素应用每个验证方法。

    - 你可以将这些方法放在任何类和命名空间中。 将它们更改为你的首选项。

    ```
    using System.Collections.Generic;
    using System.ComponentModel.Composition;
    using System.Linq;
    using Microsoft.VisualStudio.Modeling.Validation;
    using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Uml;
    using Microsoft.VisualStudio.Uml.Classes;
    // You might also need the other Microsoft.VisualStudio.Uml namespaces.

    namespace Validation
    {
      public class MyValidationExtensions
      {
        // SAMPLE VALIDATION METHOD.
        // All validation methods have the following attributes.
        [Export(typeof(System.Action<ValidationContext, object>))]
        [ValidationMethod(
           ValidationCategories.Save
         | ValidationCategories.Open
         | ValidationCategories.Menu)]
        public void ValidateClassNames
          (ValidationContext context,
           // This type determines what elements
           // will be validated by this method:
           IClass elementToValidate)
        {
          // A validation method should not change the model.

          List<string> attributeNames = new List<string>();
          foreach (IProperty attribute in elementToValidate.OwnedAttributes)
          {
            string name = attribute.Name;
            if (!string.IsNullOrEmpty(name) && attributeNames.Contains(name))
            {
              context.LogError(
                string.Format("Duplicate attribute name '{0}' in class {1}", name, elementToValidate.Name),
                "001", elementToValidate);
            }
            attributeNames.Add(name);
          }

        }
        // Add more validation methods for different element types.
      }
    }
    ```

## <a name="Executing"></a>执行验证约束
 出于测试目的，在调试模式下执行验证方法。

#### <a name="to-test-the-validation-constraint"></a>若要测试验证约束

1. 按“F5”，或在“调试” 菜单上，选择“开始调试”。

     此时将启动 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 的实验实例。

     **疑难解答**：如果新的 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 未启动：

    - 如果你有多个项目，请确保将 VSIX 项目设置为解决方案的启动项目。

    - 在“解决方案资源管理器”中，在启动或唯一项目的快捷菜单上选择“属性”。 在项目属性编辑器中，选择 "**调试**" 选项卡。请确保 "**启动外部程序**" 字段中的字符串是 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]的完整路径名，通常为：

         `C:\Program Files\Microsoft Visual Studio [version]\Common7\IDE\devenv.exe`

2. 在实验性 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]中，打开或创建一个建模项目，然后打开或创建一个建模图。

3. 若要为上一节中给出的示例约束设置测试：

    1. 打开一个类图。

    2. 创建一个类，并添加具有相同名称的两个特性。

4. 在图上任意位置处的快捷菜单上，选择“验证”。

5. 错误窗口中将报告模型中的所有错误。

6. 双击错误报告。 如果报告中提及的元素在屏幕上可见，则将突出显示这些元素。

     **故障排除**：如果菜单上没有“验证” 命令，请确保：

    - 验证项目作为一个 MEF 组件列在 VSIX 项目的 **source.extensions.manifest** 中的在“资产” 选项卡中列出。

    - 将正确的 `Export` 和 `ValidationMethod` 特性附加到验证方法。

    - `ValidationCategories.Menu` 包含在 `ValidationMethod` 属性的自变量中，并且它由使用逻辑 OR （&#124;）的其他值构成。

    - 所有 `Import` 和 `Export` 特性的参数都有效。

## <a name="Implementing"></a>计算约束
 验证方法应确定你要应用的验证约束是 true 还是 false。 如果为 true，则不执行任何操作。 如果为 false，则应使用 `ValidationContext` 参数提供的方法报告错误。

> [!NOTE]
> 验证方法不应更改模型。 不能保证约束的执行时间和执行顺序。 如果你需要在验证运行过程中连续执行验证方法之间传递信息，则可以使用 [协调多个验证](#ContextCache)中描述的上下文缓存。

 例如，如果想要确保每种类型（类、接口或枚举器）具有长度为至少三个字符的名称，则可以使用此方法：

```
public void ValidateTypeName(ValidationContext context, IType type)
{
  if (!string.IsNullOrEmpty(type.Name) && type.Name.Length < 3)
  {
    context.LogError(
      string.Format("Type name {0} is too short", type.Name),
               "001", type);
   }
 }
```

 请参阅 [Programming with the UML API](../modeling/programming-with-the-uml-api.md) 了解可用于导航和读取模型的方法和类型的相关信息。

### <a name="about-validation-constraint-methods"></a>关于验证约束方法
 每个验证约束由如下形式的方法定义：

```
[Export(typeof(System.Action<ValidationContext, object>))]
 [ValidationMethod(ValidationCategories.Save
  | ValidationCategories.Menu
  | ValidationCategories.Open)]
public void ValidateSomething
  (ValidationContext context, IClassifier elementToValidate)
{...}
```

 每个验证方法的特性和参数如下所示：

|||
|-|-|
|`[Export(typeof(System.Action <ValidationContext, object>))]`|使用 Managed Extensibility Framework (MEF) 将方法定义为验证约束。|
|`[ValidationMethod (ValidationCategories.Menu)]`|指定将执行验证的时间。 如果要组合多&#124;个选项，请使用按位 "或" （）。<br /><br /> `Menu` = 由“验证”菜单调用。<br /><br /> `Save` = 在保存模型时调用。<br /><br /> `Open` = 在打开模型时调用。 `Load` = 在保存模型时调用，但如果违背规则，则警告用户此操作可能不会重新打开模型。 也可以在加载时（解析模型前）调用。|
|`public void ValidateSomething`<br /><br /> `(ValidationContext context,`<br /><br /> `IElement element)`|将第二个参数 `IElement` 替换为你希望向其应用约束的元素类型。 这将对指定类型的所有元素调用该约束方法。<br /><br /> 方法的名称并不重要。|

 你可以使用第二个参数中的其他类型定义所需的尽可能多的验证方法。 调用验证时，将对符合该参数类型的每个模型元素调用每个验证方法。

### <a name="reporting-validation-errors"></a>报告验证错误
 若要创建错误报告，请使用 `ValidationContext`提供的方法：

 `context.LogError("error string", errorCode, elementsWithError);`

- `"error string"` 将出现在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 错误列表中

- `errorCode` 是一个字符串，应该是错误的唯一标识符

- `elementsWithError` 标识模型中的元素。 当用户双击错误报告时，将选择代表此元素的形状。

  `LogError(),` `LogWarning()` 并 `LogMessage()` 将消息放入错误列表的不同部分。

## <a name="how-validation-methods-are-applied"></a>如何应用验证方法
 验证应用于模型中的每个元素，其中包括关系和部分较大元素，例如类的特性和操作的参数。

 每个验证方法应用于符合其第二个参数中的类型的每个元素。 这意味着，如果你使用 `IUseCase` 的第二个参数定义一个验证方法，并使用该参数的超类型 `IElement`定义另一个验证方法，则这两种方法将应用于模型中的每个用例。

 类型的层次结构在[UML 模型元素类型](../modeling/uml-model-element-types.md)中进行汇总。

 你可以按以下关系访问这些元素。 例如，如果你打算在 `IClass`上定义一个验证方法，则可以遍历其拥有的属性：

```
public void ValidateTypeName(ValidationContext context, IClass c)
{
   foreach (IProperty property in c.OwnedAttributes)
   {
       if (property.Name.Length < 3)
       {
            context.LogError(
                 string.Format(
                        "Property name {0} is too short",
                        property.Name),
                 "001", property);
        }
   }
}
```

### <a name="creating-a-validation-method-on-the-model"></a>在模型上创建验证方法
 如果希望确保在每个验证运行过程中精确调用验证方法，则可以验证 `IModel`：

```
using Microsoft.VisualStudio.Uml.AuxiliaryConstructs; ...
[Export(typeof(System.Action<ValidationContext, object>))]
[ValidationMethod(ValidationCategories.Menu)]
public void ValidateModel(ValidationContext context, IModel model)
{  foreach (IElement element in model.OwnedElements)
   { ...
```

### <a name="validating-shapes-and-diagrams"></a>验证形状和关系图
 不会对显示元素（如关系图和形状）调用验证方法，因为验证方法的主要目的是验证模型。 但是，你可以使用关系图上下文访问当前关系图。

 在验证类中，将 `DiagramContext` 声明为导入的属性：

```
using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Presentation;
...
[Import]
public IDiagramContext DiagramContext { get; set; }
```

 在验证方法中，你可以使用 `DiagramContext` 来访问当前焦点关系图（如果存在）：

```
[Export(typeof(System.Action<ValidationContext, object>))]
[ValidationMethod(ValidationCategories.Menu)]
public void ValidateModel(ValidationContext context, IModel model)
{
  IDiagram focusDiagram = DiagramContext.CurrentDiagram;
  if (focusDiagram != null)
  {
    foreach (IShape<IUseCase> useCaseShape in
              focusDiagram.GetChildShapes<IUseCase>())
    { ...
```

 若要记录错误，你必须获取形状表示的模型元素，因为你不能将形状传递到 `LogError`：

```
IUseCase useCase = useCaseShape.Element;
context.LogError(... , usecase);
```

### <a name="ContextCache"></a>协调多个验证
 调用验证时，例如当用户从关系图菜单调用验证时，每个验证方法将应用于每个模型元素。 这意味着，在单次调用验证框架时，可以将同一方法多次应用于不同的元素。

 这为处理元素间关系的验证带来了问题。 例如，你可以编写一个验证，从（例如）用例开始，遍历 **include** 关系以验证是否没有循环关系。 但是，当方法应用于具有多个 **include** 链接的模型中的每个用例时，很有可能会重复处理该模型的同一区域。

 为了避免这种情况，存在一个上下文缓存，在验证运行过程中可以将信息保留保留在其中。 你可以使用上下文缓存在验证方法的多次执行之间传递信息。 例如，你可以存储已在此验证运行过程中得到处理的元素的列表。 缓存将在每个验证运行开始时创建，并且不能用于在不同的验证运行之间传递信息。

|||
|-|-|
|`context.SetCacheValue<T> (name, value)`|存储值|
|`context.TryGetCacheValue<T> (name, out value)`|获取值。 如果成功，则返回 true。|
|`context.GetValue<T>(name)`|获取值。|
|`Context.GetValue<T>()`|获取指定类型的值。|

## <a name="Installing"></a>安装和卸载扩展
 你可以在自己的计算机和其他计算机上安装 [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] 扩展。

#### <a name="to-install-an-extension"></a>若要安装扩展

1. 在你的计算机上，找到由 VSIX 项目生成的 **.vsix** 文件。

    1. 在“解决方案资源管理器”中，在 VSIX 项目的快捷菜单上，选择“在 Windows 资源管理器中打开文件夹”。

    2. **\*\\** _项目_**中**查找文件 bin\\

2. 将 **.vsix** 文件复制到要安装该扩展的目标计算机。 该计算机可以是自己的计算机或其他计算机。

    - 目标计算机必须具有你在**source.extension.vsixmanifest**中指定的 [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] 版本之一。

3. 在目标计算机上，打开 **.vsix** 文件。

     “” 将会打开并安装扩展。

4. 启动或重启 [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)]。

#### <a name="to-uninstall-an-extension"></a>若要卸载扩展

1. 在 **“工具”** 菜单上，选择 **“扩展和更新”** 。

2. 展开“已安装的扩展”。

3. 选择扩展，然后选择“卸载”。

   在极少数情况下，有错误的扩展无法加载并在错误窗口中创建报告，但不显示在扩展管理器中。 在这种情况下，可以通过从以下位置删除文件来删除扩展，其中 *% LocalAppData%* 通常为*DriveName*： \Users\\*UserName*\AppData\Local：

   *%LocalAppData%* **\Microsoft\VisualStudio\\[version]\Extensions**

## <a name="Example"></a> 示例
 本示例查找元素间依赖关系中的循环。

 保存及验证菜单命令时都会进行验证。

```
/// <summary>
/// Verify that there are no loops in the dependency relationsips.
/// In our project, no element should be a dependent of itself.
/// </summary>
/// <param name="context">Validation context for logs.</param>
/// <param name="element">Element to start validation from.</param>
[Export(typeof(System.Action<ValidationContext, object>))]
[ValidationMethod(ValidationCategories.Menu
     | ValidationCategories.Save | ValidationCategories.Open)]
public void NoDependencyLoops(ValidationContext context, INamedElement element)
{
    // The validation framework will call this method
    // for every element in the model. But when we follow
    // the dependencies from one element, we will validate others.
    // So we keep a list of the elements that we don't need to validate again.
    // The list is kept in the context cache so that it is passed
    // from one execution of this method to another.
    List<INamedElement> alreadySeen = null;
    if (!context.TryGetCacheValue("No dependency loops", out alreadySeen))
    {
       alreadySeen = new List<INamedElement>();
       context.SetCacheValue("No dependency loops", alreadySeen);
    }

    NoDependencyLoops(context, element,
                new INamedElement[0], alreadySeen);
}

/// <summary>
/// Log an error if there is any loop in the dependency relationship.
/// </summary>
/// <param name="context">Validation context for logs.</param>
/// <param name="element">The element to be validated.</param>
/// <param name="dependants">Elements we've followed in this recursion.</param>
/// <param name="alreadySeen">Elements that have already been validated.</param>
/// <returns>true if no error was detected</returns>
private bool NoDependencyLoops(ValidationContext context,
    INamedElement element, INamedElement[] dependants,
    List<INamedElement> alreadySeen)
{
    if (dependants.Contains(element))
    {
        context.LogError(string.Format("{0} should not depend on itself", element.Name),
        "Fabrikam.UML.NoGenLoops", // unique code for this error
        dependants.SkipWhile(e => e != element).ToArray());
            // highlight elements that are in the loop
        return false;
    }
    INamedElement[] dependantsPlusElement =
        new INamedElement[dependants.Length + 1];
    dependants.CopyTo(dependantsPlusElement, 0);
    dependantsPlusElement[dependantsPlusElement.Length - 1] = element;

    if (alreadySeen.Contains(element))
    {
        // We have already validated this when we started
        // from another element during this validation run.
        return true;
    }
    alreadySeen.Add(element);

    foreach (INamedElement supplier in element.GetDependencySuppliers())
    {
        if (!NoDependencyLoops(context, supplier,
             dependantsPlusElement, alreadySeen))
        return false;
    }
    return true;
}
```

## <a name="see-also"></a>请参阅
 [使用 UML API](../modeling/programming-with-the-uml-api.md) [定义和安装建模扩展](../modeling/define-and-install-a-modeling-extension.md)编程
