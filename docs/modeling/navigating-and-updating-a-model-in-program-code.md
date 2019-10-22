---
title: 在程序代码中导航和更新模型
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language, programming domain models
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 7273019d837a9cc13f6ffb306946372f11ec1f7f
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72658360"
---
# <a name="navigate-and-update-a-model-in-program-code"></a>在程序代码中导航和更新模型

您可以编写代码来创建和删除模型元素、设置其属性以及创建和删除元素之间的链接。 所有更改都必须在事务内进行。 如果在关系图上查看元素，则在事务结束时，关系图将自动 "固定"。

## <a name="example"></a>DSL 定义示例
 本主题中的示例是 Dsldefinition.dsl 的主要部分：

 ![DSL 定义关系&#45;图系列树模型](../modeling/media/familyt_person.png)

 此模型是此 DSL 的实例：

 ![都铎王朝家谱模型](../modeling/media/tudor_familytreemodel.png)

### <a name="references-and-namespaces"></a>引用和命名空间
 若要运行本主题中的代码，你应该参考：

 `Microsoft.VisualStudio.Modeling.Sdk.11.0.dll`

 你的代码将使用此命名空间：

 `using Microsoft.VisualStudio.Modeling;`

 此外，如果您要从在其上定义 DSL 的项目中编写代码，则应导入 Dsl 项目生成的程序集。

## <a name="navigation"></a>导航模型

### <a name="properties"></a>属性
 在 DSL 定义中定义的域属性将成为可在程序代码中访问的属性：

 `Person henry = ...;`

 `if (henry.BirthDate < 1500) ...`

 `if (henry.Name.EndsWith("VIII")) ...`

 如果要设置属性，则必须在[事务](#transaction)内执行此操作：

 `henry.Name = "Henry VIII";`

 如果在 DSL 定义中**计算**属性**类型**，则不能对其进行设置。 有关详细信息，请参阅[计算的和自定义的存储属性](../modeling/calculated-and-custom-storage-properties.md)。

### <a name="relationships"></a>关系
 在 DSL 定义中定义的域关系将成为属性对，每个属性在关系的每个端点上都有一个。 属性的名称将在 Dsldefinition.dsl 关系图中显示为关系的每一侧角色上的标签。 根据角色的重数，属性的类型可以是关系的另一端的类，也可以是该类的集合。

 `foreach (Person child in henry.Children) { ... }`

 `FamilyTreeModel ftree = henry.FamilyTreeModel;`

 关系的另一端的属性始终是反向的。 当创建或删除链接时，将更新这两个元素的角色属性。 以下表达式（使用 `System.Linq` 的扩展）在示例中的 ParentsHaveChildren 关系中始终为 true：

 `(Person p) => p.Children.All(child => child.Parents.Contains(p))`

 `&& p.Parents.All(parent => parent.Children.Contains(p));`

 **ElementLinks**。 关系也由称为 "*链接*" 的模型元素表示，该元素是域关系类型的实例。 链接始终有一个源元素和一个目标元素。 源元素和目标元素可以相同。

 可以访问链接及其属性：

 `ParentsHaveChildren link = ParentsHaveChildren.GetLink(henry, edward);`

 `// This is now true:`

 `link == null || link.Parent == henry && link.Child == edward`

 默认情况下，不允许关系的多个实例链接任意一对模型元素。 但如果在 DSL 定义中，`Allow Duplicates` 标志对于关系为 true，则可能存在多个链接，并且必须使用 `GetLinks`：

 `foreach (ParentsHaveChildren link in ParentsHaveChildren.GetLinks(henry, edward)) { ... }`

 还有其他用于访问链接的方法。 例如:

 `foreach (ParentsHaveChildren link in     ParentsHaveChildren.GetLinksToChildren(henry)) { ... }`

 **隐藏的角色。** 如果在 DSL 定义中，**为**特定角色生成的属性为**false** ，则不会生成与该角色对应的属性。 不过，你仍然可以使用关系的方法访问链接和遍历链接：

 `foreach (Person p in ParentsHaveChildren.GetChildren(henry)) { ... }`

 最常使用的示例是 <xref:Microsoft.VisualStudio.Modeling.Diagrams.PresentationViewsSubject> 关系，它将模型元素链接到在关系图上显示它的形状：

 `PresentationViewsSubject.GetPresentation(henry)[0] as PersonShape`

### <a name="the-element-directory"></a>元素目录
 你可以使用元素目录访问存储区中的所有元素：

 `store.ElementDirectory.AllElements`

 还提供了一些方法用于查找元素，如下所示：

 `store.ElementDirectory.FindElements(Person.DomainClassId);`

 `store.ElementDirectory.GetElement(elementId);`

## <a name="metadata"></a>访问类信息
 可以获取有关 DSL 定义的类、关系和其他方面的信息。 例如:

 `DomainClassInfo personClass = henry.GetDomainClass();`

 `DomainPropertyInfo birthProperty =`

 `personClass.FindDomainProperty("BirthDate")`

 `DomainRelationshipInfo relationship =`

 `link.GetDomainRelationship();`

 `DomainRoleInfo sourceRole = relationship.DomainRole[0];`

 模型元素的上级类如下所示：

- ModelElement-所有元素和关系均为 ModelElements

- ElementLink-所有关系均为 ElementLinks

## <a name="transaction"></a>在事务内执行更改
 每当程序代码更改存储区中的任何内容时，它都必须在事务内执行此操作。 这适用于所有模型元素、关系、形状、关系图及其属性。 有关更多信息，请参见<xref:Microsoft.VisualStudio.Modeling.Transaction>。

 管理事务的最便捷方法是使用 `try...catch` 语句中包含的 `using` 语句：

```
Store store; ...
try
{
  using (Transaction transaction =
    store.TransactionManager.BeginTransaction("update model"))
    // Outermost transaction must always have a name.
  {
    // Make several changes in Store:
    Person p = new Person(store);
    p.FamilyTreeModel = familyTree;
    p.Name = "Edward VI";
    // end of changes to Store

    transaction.Commit(); // Don't forget this!
  } // transaction disposed here
}
catch (Exception ex)
{
  // If an exception occurs, the Store will be
  // rolled back to its previous state.
}
```

 可以在一个事务内进行任意数量的更改。 您可以在活动事务内打开新事务。

 若要使您的更改成为永久更改，应在处理事务之前 `Commit` 该事务。 如果发生未在事务中捕获的异常，则会将存储重置为其在更改前的状态。

## <a name="elements"></a>创建模型元素
 此示例向现有模型添加元素：

```csharp
FamilyTreeModel familyTree = ...; // The root of the model.
using (Transaction t =
    familyTree.Store.TransactionManager
    .BeginTransaction("update model"))
{
  // Create a new model element
  // in the same partition as the model root:
  Person edward = new Person(familyTree.Partition);
  // Set its embedding relationship:
  edward.FamilyTreeModel = familyTree;
          // same as: familyTree.People.Add(edward);
  // Set its properties:
  edward.Name = "Edward VII";
  t.Commit(); // Don't forget this!
}
```

 此示例说明了有关创建元素的基本要点：

- 在存储的特定分区中创建新元素。 对于模型元素和关系（而不是形状），这通常是默认分区。

- 使其成为嵌入关系的目标。 在此示例的 Dsldefinition.dsl 中，每个用户必须是嵌入关系 FamilyTreeHasPeople 的目标。 若要实现此目的，可以设置 Person 对象的 FamilyTreeModel role 属性，或将 Person 添加到 FamilyTreeModel 对象的 "人员" 角色属性中。

- 设置新元素的属性，尤其是 Dsldefinition.dsl 中 `IsName` 为 true 的属性。 此标志标记用于标识其所有者内唯一标识该元素的属性。 在这种情况下，Name 属性具有该标志。

- 必须已将此 DSL 的 DSL 定义加载到存储区中。 如果你正在编写一个扩展（如菜单命令），通常情况下，这是正确的。 在其他情况下，可以将模型显式加载到存储区中，或使用[ModelBus](/previous-versions/ee904639(v=vs.140))将其加载。 有关详细信息，请参阅[如何：在程序代码中从文件打开模型](../modeling/how-to-open-a-model-from-file-in-program-code.md)。

  以这种方式创建元素时，将自动创建一个形状（如果 DSL 有一个关系图）。 它显示在自动分配的位置，具有默认的形状、颜色和其他功能。 如果要控制关联形状的显示位置和方式，请参阅[创建元素及其形状](#merge)。

## <a name="links"></a>创建关系链接
 示例 DSL 定义中定义了两个关系。 每个关系在关系的每一端的类上定义一个*角色属性*。

 可以通过三种方式创建关系的实例。 这三种方法都具有相同的效果：

- 设置源角色扮演者的属性。 例如:

  - `familyTree.People.Add(edward);`

  - `edward.Parents.Add(henry);`

- 设置目标角色扮演者的属性。 例如:

  - `edward.familyTreeModel = familyTree;`

       此角色的重数为 `1..1`，因此我们分配值。

  - `henry.Children.Add(edward);`

       此角色的重数为 `0..*`，因此我们将其添加到集合中。

- 显式构造关系的实例。 例如:

  - `FamilyTreeHasPeople edwardLink = new FamilyTreeHasPeople(familyTreeModel, edward);`

  - `ParentsHaveChildren edwardHenryLink = new ParentsHaveChildren(henry, edward);`

  如果要设置关系本身的属性，则最后一种方法非常有用。

  以这种方式创建元素时，将自动创建关系图上的连接线，但它具有默认的形状、颜色和其他功能。 若要控制关联连接器的创建方式，请参阅[创建元素及其形状](#merge)。

## <a name="deleteelements"></a>删除元素

通过调用 `Delete()` 删除元素：

`henry.Delete();`

此操作还将删除：

- 与元素之间的关系链接。 例如，`edward.Parents` 将不再包含 `henry`。

- @No__t_0 标志为 true 的角色所在的元素。 例如，将删除显示该元素的形状。

默认情况下，每个嵌入关系在目标角色上都 `PropagatesDelete` 为 true。 删除 `henry` 不会删除 `familyTree`，但 `familyTree.Delete()` 会删除 `Persons`。

默认情况下，对于引用关系的角色，`PropagatesDelete` 不是 true。

删除对象时，可能会导致删除规则忽略特定的传播。 如果要将一个元素替换为另一个元素，这会很有用。 提供一个或多个不应传播删除的角色的 GUID。 可以从关系类中获取 GUID：

`henry.Delete(ParentsHaveChildren.SourceDomainRoleId);`

（此特定示例不起作用，因为 `ParentsHaveChildren` 关系的角色 `false` `PropagatesDelete`。）

在某些情况下，通过在元素上或在将被传播删除的元素上存在锁，可以防止删除。 您可以使用 `element.CanDelete()` 来检查元素是否可以删除。

## <a name="deletelinks"></a>删除关系链接
 可以通过从角色属性中删除元素来删除关系链接：

 `henry.Children.Remove(edward); // or:`

 `edward.Parents.Remove(henry);  // or:`

 还可以显式删除链接：

 `edwardHenryLink.Delete();`

 这三种方法都具有相同的效果。 只需使用其中一个。

 如果角色的值为 0 ..1 或 1 ..1，则可以将其设置为 `null` 或其他值：

 `edward.FamilyTreeModel = null;`//或：

 `edward.FamilyTreeModel = anotherFamilyTree;`

## <a name="reorder"></a>重新排序关系的链接
 特定关系的来源或目标的特定关系的链接具有特定的序列。 它们按照添加顺序显示。 例如，此语句将始终按相同顺序生成子项：

 `foreach (Person child in henry.Children) ...`

 可以更改链接的顺序：

 `ParentsHaveChildren link = GetLink(henry,edward);`

 `ParentsHaveChildren nextLink = GetLink(henry, elizabeth);`

 `DomainRoleInfo role =`

 `link.GetDomainRelationship().DomainRoles[0];`

 `link.MoveBefore(role, nextLink);`

## <a name="locks"></a>住
 您所做的更改可能会受到锁定的阻止。 可以在单个元素、分区和存储区上设置锁。 如果这些级别中有任何一个锁锁定了您要进行的更改类型，则在您尝试时可能会引发异常。 可以通过使用元素来发现是否设置了锁。GetLocks （），它是在命名空间 <xref:Microsoft.VisualStudio.Modeling.Immutability> 中定义的扩展方法。

 有关详细信息，请参阅[定义锁定策略以创建只读段](../modeling/defining-a-locking-policy-to-create-read-only-segments.md)。

## <a name="copy"></a>复制和粘贴
 可以将元素或元素组复制到 <xref:System.Windows.Forms.IDataObject>：

```csharp
Person person = personShape.ModelElement as Person;
Person adopter = adopterShape.ModelElement as Person;
IDataObject data = new DataObject();
personShape.Diagram.ElementOperations
      .Copy(data, person.Children.ToList<ModelElement>());
```

 元素以序列化的元素组的形式进行存储。

 可以将 IDataObject 中的元素合并到模型中：

```csharp
using (Transaction t = targetDiagram.Store.
        TransactionManager.BeginTransaction("paste"))
{
  adopterShape.Diagram.ElementOperations.Merge(adopter, data);
}
```

 `Merge ()` 可以接受 `PresentationElement` 或 `ModelElement`。 如果为其指定 `PresentationElement`，还可以在目标关系图上指定一个位置作为第三个参数。

## <a name="diagrams"></a>导航和更新关系图
 在 DSL 中，表示概念（如 Person 或歌曲）的域模型元素与 shape 元素不同，后者表示在关系图上看到的内容。 域模型元素存储概念的重要属性和关系。 Shape 元素存储对象视图在关系图上的大小、位置和颜色以及其组件部分的布局。

### <a name="presentation-elements"></a>表示元素
 ![基本形状和元素类型的类图](../modeling/media/dslshapesandelements.png)

 在 DSL 定义中，指定的每个元素都会创建一个派生自以下标准类之一的类。

|元素类型|基类|
|-|-|
|域类|<xref:Microsoft.VisualStudio.Modeling.ModelElement>|
|域关系|<xref:Microsoft.VisualStudio.Modeling.ElementLink>|
|形状|<xref:Microsoft.VisualStudio.Modeling.Diagrams.NodeShape>|
|连接符|<xref:Microsoft.VisualStudio.Modeling.Diagrams.BinaryLinkShape>|
|关系图|<xref:Microsoft.VisualStudio.Modeling.Diagrams.Diagram>|

 关系图上的元素通常表示一个模型元素。 通常（但不总是），<xref:Microsoft.VisualStudio.Modeling.Diagrams.NodeShape> 表示域类实例，而 <xref:Microsoft.VisualStudio.Modeling.Diagrams.BinaryLinkShape> 表示域关系实例。 @No__t_0 关系将节点或链接形状链接到它所表示的模型元素。

 每个节点或链接形状都属于一个关系图。 二进制链接形状连接两个节点形状。

 形状可以有两个集中的子形状。 @No__t_0 集内的形状局限于其父级的边界框。 @No__t_0 列表中的形状可能出现在父级边界以外或部分之外，例如标签或端口。 关系图没有 `RelativeChildShapes` 且没有 `Parent`。

### <a name="views"></a>在形状和元素之间导航
 域模型元素和形状元素由 <xref:Microsoft.VisualStudio.Modeling.Diagrams.PresentationViewsSubject> 关系相关。

```csharp
// using Microsoft.VisualStudio.Modeling;
// using Microsoft.VisualStudio.Modeling.Diagrams;
// using System.Linq;
Person henry = ...;
PersonShape henryShape =
  PresentationViewsSubject.GetPresentation(henry)
    .FirstOrDefault() as PersonShape;
```

 关系图上的连接器的相同关系链接关系：

```
Descendants link = Descendants.GetLink(henry, edward);
DescendantConnector dc =
   PresentationViewsSubject.GetPresentation(link)
     .FirstOrDefault() as DescendantConnector;
// dc.FromShape == henryShape && dc.ToShape == edwardShape
```

 此关系还将模型的根链接到关系图：

```
FamilyTreeDiagram diagram =
   PresentationViewsSubject.GetPresentation(familyTree)
      .FirstOrDefault() as FamilyTreeDiagram;
```

 若要获取形状表示的模型元素，请使用：

 `henryShape.ModelElement as Person`

 `diagram.ModelElement as FamilyTreeModel`

### <a name="navigating-around-the-diagram"></a>围绕关系图导航
 通常，不建议在关系图上的形状和连接线之间导航。 最好是在模型中导航关系，只在需要处理关系图的外观时才在形状和连接线之间移动。 这些方法将连接器链接到每一端的形状：

 `personShape.FromRoleLinkShapes, personShape.ToRoleLinkShapes`

 `connector.FromShape, connector.ToShape`

 许多形状是复合的;它们由一个父形状和一个或多个子级层构成。 相对于另一个形状定位的形状*称为其子级。* 父形状移动时，子元素将随之移动。

 *相对子级*可以出现在父形状的边界框的外部。 *嵌套*子级严格显示在父级的边界内。

 若要在关系图上获取顶部形状集，请使用：

 `Diagram.NestedChildShapes`

 形状和连接线的上级类如下：

 <xref:Microsoft.VisualStudio.Modeling.ModelElement>

 -- <xref:Microsoft.VisualStudio.Modeling.Diagrams.PresentationElement>

 -- <xref:Microsoft.VisualStudio.Modeling.Diagrams.ShapeElement>

 ----- <xref:Microsoft.VisualStudio.Modeling.Diagrams.NodeShape>

 ------- <xref:Microsoft.VisualStudio.Modeling.Diagrams.Diagram>

 ------- *YourShape*

 ----- <xref:Microsoft.VisualStudio.Modeling.Diagrams.LinkShape>

 ------- <xref:Microsoft.VisualStudio.Modeling.Diagrams.BinaryLinkShape>

 --------- *YourConnector*

### <a name="shapeProperties"></a>形状和连接线的属性
 在大多数情况下，不需要对形状进行显式更改。 更改模型元素后，"修复" 规则会更新形状和连接线。 有关详细信息，请参阅[响应和传播更改](../modeling/responding-to-and-propagating-changes.md)。

 但是，对独立于模型元素的属性中的形状做出某些显式更改很有用。 例如，你可以更改这些属性：

- <xref:Microsoft.VisualStudio.Modeling.Diagrams.NodeShape.Size%2A>-确定形状的高度和宽度。

- 相对于父形状或关系图的 <xref:Microsoft.VisualStudio.Modeling.Diagrams.NodeShape.Location%2A> 位置

- <xref:Microsoft.VisualStudio.Modeling.Diagrams.ShapeElement.StyleSet%2A>-用于绘制形状或连接符的笔和画笔集

- <xref:Microsoft.VisualStudio.Modeling.Diagrams.ShapeElement.Hide%2A>-使形状不可见

- <xref:Microsoft.VisualStudio.Modeling.Diagrams.ShapeElement.Show%2A>-使形状在 `Hide()` 之后可见

### <a name="merge"></a>创建元素及其形状

当你创建一个元素并将其链接到嵌入关系树时，将自动创建并关联一个形状。 这是通过在事务结束时执行的 "修复" 规则来完成的。 但是，形状将显示在自动分配的位置，并且其形状、颜色和其他功能将具有默认值。 若要控制如何创建形状，您可以使用 merge 函数。 必须先将要添加的元素添加到 ElementGroup 中，然后再将该组合并到关系图中。

此方法：

- 如果已将属性指定为元素名称，则设置名称。

- 观察在 DSL 定义中指定的任何元素合并指令。

当用户双击关系图时，此示例在鼠标位置创建一个形状。 在此示例的 DSL 定义中，已公开 `ExampleShape` 的 `FillColor` 属性。

```csharp
using Microsoft.VisualStudio.Modeling;
using Microsoft.VisualStudio.Modeling.Diagrams;
partial class MyDiagram
{
  public override void OnDoubleClick(DiagramPointEventArgs e)
  {
    base.OnDoubleClick(e);

    using (Transaction t = this.Store.TransactionManager
        .BeginTransaction("double click"))
    {
      ExampleElement element = new ExampleElement(this.Store);
      ElementGroup group = new ElementGroup(element);

      { // To use a shape of a default size and color, omit this block.
        ExampleShape shape = new ExampleShape(this.Partition);
        shape.ModelElement = element;
        shape.AbsoluteBounds = new RectangleD(0, 0, 1.5, 1.0);
        shape.FillColor = System.Drawing.Color.Azure;
        group.Add(shape);
      }

      this.ElementOperations.MergeElementGroupPrototype(
        this,
        group.CreatePrototype(),
        PointD.ToPointF(e.MousePosition));
      t.Commit();
    }
  }
}
```

 如果提供了多个形状，请使用 `AbsoluteBounds` 设置其相对位置。

 你还可以使用此方法设置连接器的颜色和其他公开的属性。

### <a name="use-transactions"></a>使用事务
 形状、连接符和关系图是应用商店中 <xref:Microsoft.VisualStudio.Modeling.ModelElement> 和 live 的子类型。 因此，你必须仅在事务中对它们进行更改。 有关详细信息，请参阅[如何：使用事务更新模型](../modeling/how-to-use-transactions-to-update-the-model.md)。

## <a name="docdata"></a>文档视图和文档数据
 ![标准关系图类型的类图](../modeling/media/dsldiagramsanddocs.png)

## <a name="store-partitions"></a>存储分区
 加载模型时，将同时加载随附的关系图。 通常情况下，模型会加载到 DefaultPartition 中，关系图内容会加载到另一个分区中。 通常会加载每个分区的内容并将其保存到单独的文件中。

## <a name="see-also"></a>请参阅

- <xref:Microsoft.VisualStudio.Modeling.ModelElement>
- [域特定语言中的验证](../modeling/validation-in-a-domain-specific-language.md)
- [从域特定语言生成代码](../modeling/generating-code-from-a-domain-specific-language.md)
- [如何：使用事务更新模型](../modeling/how-to-use-transactions-to-update-the-model.md)
- [使用 Visual Studio Modelbus 集成模型](../modeling/integrating-models-by-using-visual-studio-modelbus.md)
- [响应并传播更改](../modeling/responding-to-and-propagating-changes.md)
