---
title: 域特定语言中的验证
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language, constraints
- Domain-Specific Language, validation
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 9737c9f02f9231aae5d20bd22321024fcfd7fd69
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72663729"
---
# <a name="validation-in-a-domain-specific-language"></a>域特定语言中的验证
作为域特定语言 (DSL) 的作者，你可以定义验证约束，以验证由用户创建的模型是否有意义。 例如，如果你的 DSL 允许用户绘制人员及其祖先的家族树，你可以编写一个约束，用于确保孩子的出生日期在其父母之后。

 在保存模型时、打开模型时，以及当用户显式运行 "**验证**" 菜单命令时，可以执行验证约束。 还可以在程序控制下执行验证。 例如，你可以执行验证以响应属性值或关系中的某个更改。

 如果要编写文本模板或其他处理用户模型的工具，则验证尤为重要。 验证可确保模型满足由这些工具假定的前提条件。

> [!WARNING]
> 还可以允许验证约束以及扩展菜单命令和笔势处理程序一起定义在对 DSL 的单独扩展中。 除了 DSL，用户还可以选择安装这些扩展。 有关详细信息，请参阅[使用 MEF 扩展 DSL](../modeling/extend-your-dsl-by-using-mef.md)。

## <a name="running-validation"></a>运行验证
 当用户编辑模型时（即域特定语言的实例），以下操作可运行验证：

- 右键单击关系图，然后选择 "**全部验证**"。

- 在 DSL 的资源管理器中右键单击顶部节点，然后选择 "**全部验证**"

- 保存模型。

- 打开模型。

- 此外，还可编写运行验证的程序代码，例如，作为菜单命令的一部分或响应更改。

  任何验证错误都将显示在 "**错误列表**" 窗口中。 用户可以双击错误消息，以选中引起错误的模型元素。

## <a name="defining-validation-constraints"></a>定义验证约束
 通过将验证方法添加到 DSL 的域类或关系中定义验证约束。 当验证运行时，可由用户或在程序控制下执行一些或所有验证方法。 每个方法都将应用到其类的每个实例，并且在每个类中可以有多个验证方法。

 每个验证方法都将报告它找到的所有错误。

> [!NOTE]
> 验证方法报告错误，但不更改模型。 如果要调整或阻止某些更改，请参阅[验证的替代](#alternatives)项。

#### <a name="to-define-a-validation-constraint"></a>定义验证约束

1. 在**编辑器 \ 验证**节点中启用验证：

   1. 打开**Dsl\DslDefinition.dsl**。

   2. 在 DSL 资源管理器中，展开 "**编辑器**" 节点，然后选择 "**验证**"。

   3. 在属性窗口中，将 "**使用**属性" 设置为 `true`。 设置所有这些属性非常方便。

   4. 单击 "**解决方案资源管理器**" 工具栏中的 "**转换所有模板**"。

2. 为一个或多个域类或域关系编写分部类定义。 在**Dsl**项目中的新代码文件中编写这些定义。

3. 为每个类添加带有此特性的前缀：

   ```csharp
   [ValidationState(ValidationState.Enabled)]
   ```

   - 默认情况下，此特性还将针对派生类启用验证。 如果想要针对特定派生类禁用验证，则可以使用 `ValidationState.Disabled`。

4. 将验证方法添加到类。 每个验证方法都可以具有任何名称，但要具有类型 <xref:Microsoft.VisualStudio.Modeling.Validation.ValidationContext> 的一个参数。

    必须为它添加带有一个或多个 `ValidationMethod` 特性的前缀：

   ```csharp
   [ValidationMethod (ValidationCategories.Open | ValidationCategories.Save | ValidationCategories.Menu ) ]
   ```

    ValidationCategories 指定何时执行该方法。

   例如:

```csharp
using Microsoft.VisualStudio.Modeling;
using Microsoft.VisualStudio.Modeling.Validation;

// Allow validation methods in this class:
[ValidationState(ValidationState.Enabled)]
// In this DSL, ParentsHaveChildren is a domain relationship
// from Person to Person:
public partial class ParentsHaveChildren
{
  // Identify the method as a validation method:
  [ValidationMethod
  ( // Specify which events cause the method to be invoked:
    ValidationCategories.Open // On file load.
  | ValidationCategories.Save // On save to file.
  | ValidationCategories.Menu // On user menu command.
  )]
  // This method is applied to each instance of the
  // type (and its subtypes) in a model:
  private void ValidateParentBirth(ValidationContext context)
  {
    // In this DSL, the role names of this relationship
    // are "Child" and "Parent":
     if (this.Child.BirthYear < this.Parent.BirthYear
        // Allow user to leave the year unset:
        && this.Child.BirthYear != 0)
      {
        context.LogError(
             // Description:
                       "Child must be born after Parent",
             // Unique code for this error:
                       "FAB001ParentBirthError",
              // Objects to select when user double-clicks error:
                       this.Child,
                       this.Parent);
    }
  }
```

 请注意有关此代码的以下几点：

- 可以将验证方法添加到域类或域关系。 这些类型的代码在**Dsl\Generated Code\Domain \*。**

- 每个验证方法都将应用到它的类和子类的每个实例。 对于域关系，每个实例都是两个模型元素之间的链接。

- 验证方法不按任何指定的顺序进行应用，并且每个方法都不按任何可预知的顺序应用到它的类的实例。

- 通常情况下，验证方法最好不要更新存储内容，因为这会导致不一致的结果。 相反，该方法应通过调用 `context.LogError`、`LogWarning` 或 `LogInfo` 报告任何错误。

- 在 LogError 调用中，可以提供将在用户双击错误消息时选中的模型元素或关系链接的列表。

- 有关如何在程序代码中读取模型的信息，请参阅[在程序代码中导航和更新模型](../modeling/navigating-and-updating-a-model-in-program-code.md)。

  该示例将应用到以下域模型。 ParentsHaveChildren 关系具有称为 Child 和 Parent 的角色。

  ![DSL 定义关系&#45;图系列树模型](../modeling/media/familyt_person.png)

## <a name="validation-categories"></a>验证类别
 在 <xref:Microsoft.VisualStudio.Modeling.Validation.ValidationMethodAttribute> 特性中，指定应何时执行验证方法。

|类别|执行|
|-|-|
|<xref:Microsoft.VisualStudio.Modeling.Validation.ValidationCategories>|当用户调用验证菜单命令时。|
|<xref:Microsoft.VisualStudio.Modeling.Validation.ValidationCategories>|当打开模型文件时。|
|<xref:Microsoft.VisualStudio.Modeling.Validation.ValidationCategories>|当保存该文件时。 如果存在验证错误，则将向用户提供取消保存操作的选项。|
|<xref:Microsoft.VisualStudio.Modeling.Validation.ValidationCategories>|当保存该文件时。 如果存在来自此类别中的方法的错误，则警告用户可能无法重新打开该文件。<br /><br /> 将此类别用于测试重复名称或 ID 的验证方法，或者可能引起加载错误的其他条件。|
|<xref:Microsoft.VisualStudio.Modeling.Validation.ValidationCategories>|当调用 ValidateCustom 方法时。 只能从程序代码中调用此类别中的验证。<br /><br /> 有关详细信息，请参阅[自定义验证类别](#custom)。|

## <a name="where-to-place-validation-methods"></a>放置验证方法的位置
 通过将验证方法放置在不同的类型上，通常可达到同样的效果。 例如，可以将方法添加到“Person”类，而不是“ParentsHaveChildren”关系，并使它循环访问链接：

```
[ValidationState(ValidationState.Enabled)]
public partial class Person
{[ValidationMethod
 ( ValidationCategories.Open
 | ValidationCategories.Save
 | ValidationCategories.Menu
 )
]
  private void ValidateParentBirth(ValidationContext context)
  {
    // Iterate through ParentHasChildren links:
    foreach (Person parent in this.Parents)
    {
        if (this.BirthYear <= parent.BirthYear)
        { ...
```

 **聚合验证约束。** 若要以可预测的顺序应用验证，请在所有者类上定义单个验证方法，如模型的根元素。 此技术还允许你将多个错误报告聚合到单个消息中。

 缺点是组合的方法不易于管理，并且约束必须都具有相同的 `ValidationCategories`。 因此，建议你将每个约束保留在单独的方法中（如果可能）。

 **在上下文缓存中传递值。** 上下文参数包含一个字典，你可以在其中放置任意值。 该字典将在验证运行的生存期内持续存在。 例如，特定验证方法可以将错误计数保留在上下文中，并使用它来避免错误窗口被重复的消息所淹没。 例如:

```csharp
List<ParentsHaveChildren> erroneousLinks;
if (!context.TryGetCacheValue("erroneousLinks", out erroneousLinks))
erroneousLinks = new List<ParentsHaveChildren>();
erroneousLinks.Add(this);
context.SetCacheValue("erroneousLinks", erroneousLinks);
if (erroneousLinks.Count < 5) { context.LogError( ... ); }
```

## <a name="validation-of-multiplicities"></a>重数的验证
 将为你的 DSL 自动生成用于检查最小重数的验证方法。 此代码将写入**Dsl\Generated Code\MultiplicityValidation.cs**。 当你在 DSL 资源管理器的**编辑器 \ 验证**节点中启用验证时，这些方法生效。

 如果你将域关系的角色的重数设置为 1..* 或 1..1，但用户未创建此关系的链接，则将显示验证错误消息。

 例如，如果你的 DSL 具有类 Person 和城镇，并且关系**1. \\** * 的关系 PersonLivesInTown 为 "城镇" 角色，则对于每个不是城镇的人员，将显示一条错误消息。

## <a name="running-validation-from-program-code"></a>从程序代码运行验证
 通过访问或创建 ValidationController，可运行验证。 如果要在错误窗口中向用户显示错误，请使用附加到关系图的 DocData 的 ValidationController。 例如，如果你要编写菜单命令，则命令集类中提供了 `CurrentDocData.ValidationController`：

```csharp
using Microsoft.VisualStudio.Modeling;
using Microsoft.VisualStudio.Modeling.Validation;
using Microsoft.VisualStudio.Modeling.Shell;
...
partial class MyLanguageCommandSet
{
  private void OnMenuMyContextMenuCommand(object sender, EventArgs e)
  {
   ValidationController controller = this.CurrentDocData.ValidationController;
...
```

 有关详细信息，请参阅[如何：向快捷菜单中添加命令](../modeling/how-to-add-a-command-to-the-shortcut-menu.md)。

 还可以创建单独的验证控制器，并自行管理错误。 例如:

```csharp
using Microsoft.VisualStudio.Modeling;
using Microsoft.VisualStudio.Modeling.Validation;
using Microsoft.VisualStudio.Modeling.Shell;
...
Store store = ...;
VsValidationController validator = new VsValidationController(s);
// Validate all elements in the Store:
if (!validator.Validate(store, ValidationCategories.Save))
{
  // Deal with errors:
  foreach (ValidationMessage message in validator.ValidationMessages) { ... }
}
```

## <a name="running-validation-when-a-change-occurs"></a>当发生更改时运行验证
 如果你想要确保用户在该模型变为无效时立即收到警告，可以定义运行验证的存储事件。 有关存储事件的详细信息，请参阅[事件处理程序在模型外部传播更改](../modeling/event-handlers-propagate-changes-outside-the-model.md)。

 除了验证代码外，还应将自定义代码文件添加到**DslPackage**项目，其中包含类似于以下示例的内容。 此代码使用附加到文档的 `ValidationController`。 此控制器在 Visual Studio 错误列表中显示验证错误。

```csharp
using System;
using System.Linq;
using Microsoft.VisualStudio.Modeling;
using Microsoft.VisualStudio.Modeling.Validation;
namespace Company.FamilyTree
{
  partial class FamilyTreeDocData // Change name to your DocData.
  {
    // Register the store event handler:
    protected override void OnDocumentLoaded()
    {
      base.OnDocumentLoaded();
      DomainClassInfo observedLinkInfo = this.Store.DomainDataDirectory
         .FindDomainClass(typeof(ParentsHaveChildren));
      DomainClassInfo observedClassInfo = this.Store.DomainDataDirectory
         .FindDomainClass(typeof(Person));
      EventManagerDirectory events = this.Store.EventManagerDirectory;
      events.ElementAdded
         .Add(observedLinkInfo, new EventHandler<ElementAddedEventArgs>(ParentLinkAddedHandler));
      events.ElementDeleted.Add(observedLinkInfo, new EventHandler<ElementDeletedEventArgs>(ParentLinkDeletedHandler));
      events.ElementPropertyChanged.Add(observedClassInfo, new EventHandler<ElementPropertyChangedEventArgs>(BirthDateChangedHandler));
    }
    // Handler will be called after transaction that creates a link:
    private void ParentLinkAddedHandler(object sender,
                                ElementAddedEventArgs e)
    {
      this.ValidationController.Validate(e.ModelElement,
           ValidationCategories.Save);
    }
    // Called when a link is deleted:
    private void ParentLinkDeletedHandler(object sender,
                                ElementDeletedEventArgs e)
    {
      // Don't apply validation to a deleted item!
      // - Validate store to refresh the error list.
      this.ValidationController.Validate(this.Store,
           ValidationCategories.Save);
    }
    // Called when any property of a Person element changes:
    private void BirthDateChangedHandler(object sender,
                      ElementPropertyChangedEventArgs e)
    {
      Person person = e.ModelElement as Person;
      // Not interested in changes in other properties:
      if (e.DomainProperty.Id != Person.BirthYearDomainPropertyId)
          return;

      // Validate all parent links to and from the person:
      this.ValidationController.Validate(
        ParentsHaveChildren.GetLinksToParents(person)
        .Concat(ParentsHaveChildren.GetLinksToChildren(person))
        , ValidationCategories.Save);
    }
  }
}
```

 在影响链接或元素的“撤消”或“重做”操作后，还将调用处理程序。

## <a name="custom"></a>自定义验证类别
 除了标准验证类别（如“菜单”和“打开”），还可以定义自己的类别。 可以从程序代码调用这些类别。 用户无法直接调用它们。

 自定义类别通常用于定义测试模型是否满足特定工具的前提条件的类别。

 若要将验证方法添加到特定类别，请为它添加带有如下特性的前缀：

```csharp
[ValidationMethod(CustomCategory = "PreconditionsForGeneratePartsList")]
[ValidationMethod(ValidationCategory.Menu)]
private void TestForCircularLinks(ValidationContext context)
{...}
```

> [!NOTE]
> 你可以为方法添加带有任意数目的 `[ValidationMethod()]` 特性的前缀。 可以将方法同时添加到自定义类别和标准类别。

 若要调用自定义验证，请执行以下操作：

```csharp

// Invoke all validation methods in a custom category:
validationController.ValidateCustom
  (store, // or a list of model elements
   "PreconditionsForGeneratePartsList");
```

## <a name="alternatives"></a>验证的替代方法
 验证约束报告错误，但不更改模型。 相反，如果你想要防止模型变为无效，则可以使用其他技术。

 但是，不建议使用这些技术。 通常，最好让用户决定如何更正无效的模型。

 **调整更改以便将模型还原到有效性。** 例如，如果用户将属性设置为超过允许的最大值，则可以将属性重置为最大值。 若要实现此目的，请定义一个规则。 有关详细信息，请参阅[规则在模型内部传播更改](../modeling/rules-propagate-changes-within-the-model.md)。

 **如果尝试无效的更改，则回滚事务。** 你还可以为此目的定义规则，但在某些情况下，可以重写属性处理程序**OnValueChanging （）** ，或重写方法（如 `OnDeleted().` 回滚事务，使用 `this.Store.TransactionManager.CurrentTransaction.Rollback().` 有关详细信息，请参阅[域属性值更改处理程序](../modeling/domain-property-value-change-handlers.md)。

> [!WARNING]
> 请确保用户知道更改已调整或已回滚。 例如，使用 `System.Windows.Forms.MessageBox.Show("message").`

## <a name="see-also"></a>请参阅

- [在程序代码中导航和更新模型](../modeling/navigating-and-updating-a-model-in-program-code.md)
- [事件处理程序在模型外部传播更改](../modeling/event-handlers-propagate-changes-outside-the-model.md)