---
title: 'UML Class Diagrams: Guidelines | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
f1_keywords:
- vs.teamarch.logicalclassdiagram.overrideoperationsdialog
helpviewer_keywords:
- UML diagrams, class
- diagrams - modeling, class
- UML, class diagrams
- class diagrams - UML
- diagrams - modeling, UML class
ms.assetid: 94dbfd55-b300-4b49-9049-0831ed849486
caps.latest.revision: 56
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: c170827825d772f4d97cd22f0b5754232e8d2257
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74297292"
---
# <a name="uml-class-diagrams-guidelines"></a>UML 类图：准则
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

In Visual Studio, you can use a *UML class diagram* to describe data types and their relationships separately from their implementation. 该关系图主要用来描述类的逻辑方面，而不是它们的实现。

 To create a UML class diagram, on the **Architecture** menu, choose **New UML Diagram or Layer Diagram**.

 若要查看支持此功能的 Visual Studio 的版本，请参阅 [Version support for architecture and modeling tools](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)。

> [!NOTE]
> 本主题针对 UML 类图。 还可以创建另一种类图，它用于可视化程序代码。 See [Designing and Viewing Classes and Types](https://go.microsoft.com/fwlink/?LinkId=142231).

## <a name="Using"></a> Using UML Class Diagrams
 UML 类图有多种用途：

- 可提供对系统中所使用类型以及系统组件间所传递类型的与实现无关的描述。

     例如，“订餐”类型可在业务层以 .NET 代码实现，在组件间的接口中以 XML 实现，在数据库中以 SQL 实现，在用户界面中以 HTML 实现。 尽管这些实现在细节上有所不同，但“订餐”类型和其他类型（如“菜单”和“付款”）之间的关系始终相同。 通过 UML 类图就可将这些关系与实现分开讨论。

- 可阐明应用程序及其用户之间沟通所用词汇的词汇表，并描述用户需求。 See [Model user requirements](../modeling/model-user-requirements.md).

     例如，考虑餐馆应用程序的用户情景、用例或其他需求描述。 在此描述中，你将发现如“菜单”、“订单”、“餐饮”、“价格”、“付款”等词汇。 你可绘制定义这些词汇间关系的 UML 类图。 这可降低需求描述、用户界面和帮助文档中出现不一致的风险。

### <a name="relationship-to-other-diagrams"></a>与其他关系图的关系
 UML 类图通常与其他建模图一起绘制来描述这些关系图所使用的类型。 在任何情况下，类型的物理表示形式都不在任何关系图中表示。

 活动图

 通过对象节点传递的数据的类型。

 输入和输出插针的类型以及活动参数节点的类型。

 See [UML Activity Diagrams: Guidelines](../modeling/uml-activity-diagrams-guidelines.md).

 序列图

 消息的参数和返回值的类型。

 生命线的类型。 生命线的类应包含它可接收的所有消息的操作。

 See [UML Sequence Diagrams: Guidelines](../modeling/uml-sequence-diagrams-guidelines.md).

 组件图

 组件接口，列出它们的操作。

 See [UML Component Diagrams: Guidelines](../modeling/uml-component-diagrams-guidelines.md).

 用例图

 用例的目标和步骤说明中提到的类型。

 See [UML Use Case Diagrams: Guidelines](../modeling/uml-use-case-diagrams-guidelines.md).

## <a name="BasicSteps"></a> Basic Steps for Drawing Class Diagrams
 For reference information about the elements on UML class diagrams, see [UML Class Diagrams: Reference](../modeling/uml-class-diagrams-reference.md).

> [!NOTE]
> Detailed steps for creating any of the modeling diagrams are described in [Edit UML models and diagrams](../modeling/edit-uml-models-and-diagrams.md).

#### <a name="to-create-a-uml-class-diagram"></a>创建 UML 类图

1. On the **Architecture** menu, choose **New UML or Layer Diagram**.

2. Under **Templates**, choose **UML Class Diagram**.

3. 命名该关系图。

4. In **Add to Modeling Project**, select an existing modeling project in your solution, or **Create a New Modeling Project**, and then choose **OK**.

     A new class diagram appears with the **UMLClass Diagram** Toolbox. 该工具箱中包含所需的元素和关系。

#### <a name="to-draw-a-uml-class-diagram"></a>绘制 UML 类图

1. To create a type, choose the **Class**, **Interface** or **Enumeration** tool on the Toolbox, and then click a blank part of the diagram. （如果你看不到工具箱，请按 Ctrl+Alt+X。）

2. To add attributes or operations to the types, or literals to an enumeration, choose the **Attributes**, **Operations** or **Literals** heading in the type, and press ENTER.

     你可以写入签名，如 `f(x:Boolean):Integer`。 See [Attributes and Operations](#AttributesAndOperations).

     若要快速添加多个项，请在每一项的最后按两次 Enter。 可以使用箭头键在列表中上下移动。

3. 若要展开或折叠某个类型，请选择其左上角的 V 形图标。 You can also expand and collapse the **Attributes** and **Operations** section of a class or interface.

4. 若要绘制类型之间的关联、继承或依赖项链接，请单击相应工具，再单击源类型，然后单击目标类型。

5. To create types in a package, create a package using the **Package** tool, and then create new types and packages within the package. 还可以使用复制命令复制类型，然后将它们粘贴到包中。

6. 每个关系图都是模型中的视图，可在同一项目中的其他关系图之间共享。 To see a tree view of the complete model, choose **View**, **Other Windows**, **UML Model Explorer**.

## <a name="UsingTypes"></a> Using Classes, Interfaces, and Enumerations
 在工具箱上有三种标准分类器可供使用。 These are referred to as *types* throughout this document.

 ![A class, an enumeration, and an interface](../modeling/media/uml-classguidetypes.png "UML_ClassGuideTypes")

- Use **Classes** (1) to represent data or object types for most purposes.

- Use **Interfaces** (2) in a context where you have to differentiate between pure interfaces and concrete classes that have internal implementations. 这一区别在关系图用于描述软件实现时非常有用。 但当对被动数据进行建模或者定义用于描述用户需求的概念时，这一区别用处不大。

- Use an **Enumeration** (3) to represent a type that has a limited number of literal values, for example `Stop` and `Go`.

  - 向枚举添加文本值。 为每个文本值指定一个单独的名称。

  - 还可根据需要为每个文本值提供一个数值。 Open the shortcut menu for the literal in the enumeration, choose **Properties**, and then type a number in the **Value** field in the **Properties** window.

  为每个类型指定一个唯一的名称。

### <a name="getting-types-from-other-diagrams"></a>从其他关系图获取类型
 可以使来自其他关系图的类型显示在 UML 类图中。

 UML 类图

 可以使一个类显示在多个 UML 类图中。 When you have created a class on one diagram, drag the class from **UML Model Explorer** onto the other diagram.

 如果你希望每个关系图针对一组特定关系，这将非常有用。

 例如，你可以在一个关系图中显示“订餐”和餐馆“菜单”之间的关联，在另一个关系图中显示“订餐”和“付款”之间的关联。

 组件图

 If you have defined interfaces on the components in a component diagram, you can drag an interface from **UML Model Explorer** onto the class diagram. 在类图中，你可以定义接口包含的方法。

 See [UML Component Diagrams: Guidelines](../modeling/uml-component-diagrams-guidelines.md).

 UML 序列图

 You can create classes and interfaces from lifelines in a sequence diagram, and then drag the class from **UML Model Explorer** to a UML class diagram. 序列图中的每个生命线表示对象、组件或参与者的一个实例。

 To create a class from a lifeline, open the shortcut menu for the lifeline, and then choose **Create Class** or **Create Interface**. See [UML Sequence Diagrams: Guidelines](../modeling/uml-sequence-diagrams-guidelines.md).

## <a name="AttributesAndOperations"></a> Attributes and Operations
 特性 (4) 是类型的每个实例可具有的命名值。 访问特性不会更改实例的状态。

 操作 (5) 是类型的实例可执行的方法或函数。 它可返回一个值。 If its **isQuery** property is true, it cannot change the state of the instance.

 To add an attribute or operation to a type, open the shortcut menu for the type, choose **Add**, and then choose **Attribute** or **Operation**.

 To see its properties, open the shortcut menu for the attribute or operation, and then choose **Properties**. The properties appear in the **Properties** window.

 To see the properties of an operation's parameters, choose <strong>[…]</strong>in the **Parameters** property. 此时将显示一个新的属性对话框。

 有关你可以设置的所有属性的详细信息，请参阅：

- [UML 类图上特性的属性](../modeling/properties-of-attributes-on-uml-class-diagrams.md)

- [UML 类图中操作的属性](../modeling/properties-of-operations-on-uml-class-diagrams.md)

### <a name="types-of-attributes-and-operations"></a>特性和操作的类型
 Each *Type* of an attribute or operation, and each parameter type, can be one of the following:

- **(none)** - You can leave a type unspecified in the signature by omitting the preceding colon (`:`).

- One of the standard primitive types: **Boolean**, **Integer**, **String**.

- 模型中定义的类型。

- A parameterized value of a template type, written Template\<Parameter>. See [Template Types](#Templates).

  还可以写入尚未在模型中定义的类型的名称。 The name will be listed under **Unspecified Types** in UML Model Explorer.

> [!NOTE]
> 如果你随后在模型中定义一个具有此名称的类或接口，则以前的特性和操作仍将引用“未指定的类型”中的元素。 如果你希望将其更改为引用新类，则必须访问每个特性或操作，并通过从下拉菜单中选择新类来重新设置类型。

#### <a name="multiple-types"></a>多个类型
 可以设置任何特性、操作或参数类型的重数。

 允许的值如下所示：

 `[1]`

 给定类型的一个值。 这是默认设置。

 `[0..1]`

 **Null** or a value of the given type.

 `[*]`

 一个集合，其中包含任意数目的给定类型实例。

 `[1..*]`

 一个集合，其中包含至少一个给定类型实例。

 `[n..m]`

 一个集合，其中包含数目介于 `n` 和 `m` 之间的给定类型实例。

 如果重数大于 1，还可以设置以下属性：

- **IsOrdered** - If true, the collection has a defined order.

- **IsUnique** - If true, there are no duplicate values in the collection.

### <a name="visibility"></a>可见性
 *Visibility* indicates whether the attribute or operation can be accessed outside the class definition. 允许的值如下所示：

 **COMClassAttribute**

 **+**

 可从所有其他类型访问。

 **Private**

 **-**

 只能由此类型的内部定义访问。

 **包**

 **~**

 只能在包含此类型的包以及显式导入此类型的所有包中访问。 See [Defining Namespaces and Packages](#Packages).

 **Protected**

 **#**

 只能由此类型以及从其继承的类型访问。 See [Inheritance](#Inheritance).

### <a name="setting-the-signature-of-an-attribute-or-an-operation"></a>设置特性或操作的签名
 特性或操作的签名是一个包含其可见性、名称、参数（用于操作）和类型的属性集合。

 可在关系图中直接写入签名。 单击特性或操作以将其选中，然后再次单击它。

 请按以下格式写入签名：

```
visibility attribute-name : Type
```

 \- 或 -

```
visibility operation-name (parameter1 : Type1, ...) : Type
```

 例如:

```
+ AddItem (item : MenuItem, quantity : Integer) : Boolean
```

 使用可见性的缩写形式。 默认值为 `+` (public)。

 每个类型都可为模型中已定义的类型、诸如 Integer 或 String 之类的标准类型或者尚未定义的新类型的名称。

> [!NOTE]
> 如果在参数列表中写入名称而不带类型，则该名称指示参数的名称而不是参数的类型。 在下例中，MenuItem 和 Integer 成为没有指定类型的两个参数的名称：
>
> `AddItem(MenuItem, Integer) /* parameter names, not types! */`

 若要在签名中设置类型的重数，请将重数写入方括号，放在类型名称之后，例如：

```
+ AddItems (items : MenuItem [1..*])
+ MenuContent : MenuItem [*]
```

 如果特性或操作是静态的，则其名称将在签名中显示为带有下划线。 如果特性或操作是抽象的，则其名称将显示为斜体。

 However, you can only set the **Is Static** and **Is Abstract** properties in the **Properties** window.

#### <a name="full-signature"></a>完全签名
 编辑特性或操作的签名时，可能会在行尾所有参数之后出现某些附加属性。 它们显示在一对大括号 {…} 内。 可以编辑或添加这些属性。 例如:

```
+ AddItems (items: MenuItem [1..*] {unique, ordered})
+ GetItems (filter: String) : MenuItem [*] {ordered, query}
```

 这些属性如下所示：

 `unique`

 **Is Unique**

 集合中没有重复值。 适用于重数大于 1 的类型。

 `ordered`

 **Is Ordered**

 该集合是一个序列。 如果为 False，则没有明确的第一项。 适用于重数大于 1 的类型。

 `query`

 **Is Query**

 此操作不会更改其实例的状态。 仅应用于操作。

 `/`

 **Is Derived**

 该特性是从其他特性或关联计算得出的。

 “/”显示在特性名称的前面。 例如:

```
/TotalPrice: Integer
```

 通常，完全签名仅在你对其进行编辑时才显示在关系图上。 完成编辑后，会隐藏附加属性。 If you want to see the full signature all the time, open the shortcut menu for the type, and then choose **Show Full Signature**.

## <a name="Associations"></a> Drawing and Using Associations
 关联用于表示两个元素间任何类型的链接，而与该链接在软件中的实现方式无关。 例如，可以使用关联来表示 C# 中的指针、数据库中的关系或 XML 文件中从一部分到另一部分的交叉引用。 它还可以表示现实世界中对象间的关联，如地球和太阳。 关联并不定义链接的表示方式，而仅表示存在信息交流。

### <a name="properties-of-an-association"></a>关联的属性
 创建关联后可设置其属性。 Open the shortcut menu for the association, and then choose **Properties**.

 In addition to the properties of the association as a whole, each *role*, that is, each end of the association, has some properties of its own. To view them, expand the **First Role** and **Second Role** properties.

 每个角色的某些属性会直接显示在关系图上。 它们是：

- 角色名称。 它显示在关系图中相应的关联端处。 You can set it either on the diagram or in the **Properties** window.

- **Multiplicity**, which defaults to **1**. 它也显示在关系图中相应关联端附近。

- **Aggregation**. 它在连接线一端以菱形显示。 可以使用聚合来指示实例属于聚合角色自身还是包含另一角色的实例。

- **Is Navigable**. 如果只对一个角色为 True，则箭头将朝向可导航方向。 可用于指示软件中链接和数据库关系的可导航性。

  For the full details of these and other properties, see [Properties of associations on UML class diagrams](../modeling/properties-of-associations-on-uml-class-diagrams.md).

### <a name="navigability"></a>可导航性
 在绘制关联时，其一端为箭头，表明关联可沿该方向导航。 这在类图表示软件类且关联表示指针或引用的情况下很有用。 但当你使用类图表示实体和关系或业务概念时，它与可导航性不太相关。 在此情况下，你可能更愿意绘制不带箭头的关联。 You can do so by setting the **Is Navigable** property on both ends of the association to True.

### <a name="attributes-and-associations"></a>特性和关联
 关联是特性的图形化显示形式。 例如，你可以在“餐馆”与“菜单”之间绘制一个关联，而不是创建具有 Menu 类型特性的 Restaurant 类。

 每个特性名称成为一个角色名称。 它显示在关联中与所属类型相对的一端。 例如，参阅图示中的 `myMenu`。

 通常，最好只对不会在关系图中绘制的类型（如基元类型）使用特性。

 ![Equivalent association and attributes](../modeling/media/uml-classguideattrib.png "UML_ClassGuideAttrib")

## <a name="Inheritance"></a> 继承
 Use the **Inheritance** tool to create the following relationships:

- A *generalization* relationship between a specialized type and a general type

   \- 或 -

- A *realization* relation between a class and an interface that it implements.

  不能在继承关系中创建循环。

### <a name="generalization"></a>泛化
 泛化意味着专用类型或派生类型继承通用类型或基类型的特性、操作和关联。

 通用类型显示在关系的箭头端。

 继承的操作和特性通常不在专用类型中显示。 但是可将继承的操作添加到专用类型的操作列表中。 这对希望在专用类型中重写某些操作的属性或希望指示实现代码应这样做时是非常有用的。

##### <a name="to-override-an-operations-definition-in-a-specializing-type"></a>在专用类型中重写操作的定义

1. 单击泛化关系。

    它将会突出显示，并且其附近会出现一个操作标记。

2. Click the Action tag, and then click **Override Operations**.

    The **Override Operations** dialog box appears.

3. Select the operations that you want to appear in the specializing type, and then click **OK**.

   你选中的操作将出现在专用类型中。

### <a name="realization"></a>实现
 实现意味着类将实现由接口指定的特性和操作。 接口位于连接线的箭头端。

 创建实现连接线时，会自动在实现类中复制接口的操作。 如果向接口添加新操作，则会在该接口的实现类中复制这些操作。

 创建实现关系后，可以将该关系转换为棒糖形表示法。 Right-click the relationship and choose **Show as Lollipop**.

 这样就可以显示类所实现的接口，而不干扰具有实现链接的类图。 还可以显示在其他关系图中实现的接口和类。

 ![Realization shown with conector and lollipop](../modeling/media/uml-classguiderealize.png "UML_ClassGuideRealize")

## <a name="Templates"></a> Template Types
 你可以定义一个可由其他类型或值参数化的泛型类型或模板类型。

 例如，你可以创建由键类型和值类型参数化的泛型字典：

 ![Template class with two parameters](../modeling/media/uml-classguidetemplate1.png "UML_ClassGuideTemplate1")

#### <a name="to-create-a-template-type"></a>创建模板类型

1. 创建一个类或接口。 这将成为你的模板类型。 对它进行相应命名，例如，命名为 `Dictionary`。

2. Open the shortcut menu for the new type, and then choose **Properties**.

3. In the **Properties** window, click **[…]** in the **Template Parameters** field.

    The **Template Parameter Collection Editor** dialog box appears.

4. 选择“添加”。

5. 将名称属性设置为模板类型的参数名称，例如 `Key`。

6. Set **Parameter Kind**. The default is **Class**.

7. If you want the parameter to accept only derived classes of a particular base class, set **Constrained Value** to the base class that you want.

8. Add as many parameters as you need, then choose **OK**.

9. 与对待其他类一样将特性和操作添加到模板类型中。

     You can use parameters whose kind is **Class**, **Interface** or **Enumeration** in the definition of attributes and operations. 例如，通过使用参数类 `Key` 和 `Value`，可以在 `Dictionary` 中定义此操作：

     `Get(k : Key) : Value`

     You can use a parameter whose kind is **Integer** as a bound in a multiplicity. 例如，参数最大整数值可用于将特性的重数定义为 `[0..max]`。

   创建模板类型后，可以使用它们来定义模板绑定：

   ![A  class bound from the Dictionary template](../modeling/media/uml-classguidetemplate2.png "UML_ClassGuideTemplate2")

#### <a name="to-use-a-template-type"></a>使用模板类型

1. 创建一个新类型，例如 `AddressTable`。

2. Open the shortcut menu for the new type, and then choose **Properties**.

3. In the **Template Binding** property, select the template type, for example `Dictionary`, from the drop-down list.

4. Expand the **Template Binding** property.

     该模板类型的每个参数将显示一行。

5. 将每个参数都设置为合适的值。 例如，将 `Key` 参数设置为名为 `Name` 的类。

## <a name="Packages"></a> Packages
 可以在 UML 类图中查看包。 包是其他模型元素的容器。 可以在包中创建任何元素。 在关系图中，当你移动包时，包内的元素也将随之移动。

 可以使用折叠/展开控件隐藏或显示包的内容。

 See [Define packages and namespaces](../modeling/define-packages-and-namespaces.md).

## <a name="generating"></a> Generating Code from UML Class Diagrams
 若要开始实现 UML 类图上的类，你可生成 C# 代码或自定义代码生成模板。 通过使用提供的 C# 模板开始生成代码：

- Open the shortcut menu for the diagram or an element, choose **Generate Code**, and then set the necessary properties.

     For more information about how to set these properties and customize the provided templates, see [Generate code from UML class diagrams](../modeling/generate-code-from-uml-class-diagrams.md).

## <a name="see-also"></a>请参阅
 [Edit UML models and diagrams](../modeling/edit-uml-models-and-diagrams.md) [UML Class Diagrams: Reference](../modeling/uml-class-diagrams-reference.md) [Model user requirements](../modeling/model-user-requirements.md) [UML Component Diagrams: Reference](../modeling/uml-component-diagrams-reference.md) [UML Sequence Diagrams: Reference](../modeling/uml-sequence-diagrams-reference.md) [UML Use Case Diagrams: Reference](../modeling/uml-use-case-diagrams-reference.md) [UML Component Diagrams: Reference](../modeling/uml-component-diagrams-reference.md)
