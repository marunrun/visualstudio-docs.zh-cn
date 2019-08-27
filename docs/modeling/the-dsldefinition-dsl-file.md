---
title: DslDefinition.dsl 文件
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- Domain-Specific Language, definition file
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c43ed1fa156c77edc89b8d40185cc7436cce5d7a
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63001482"
---
# <a name="the-dsldefinitiondsl-file"></a>DslDefinition.dsl 文件

本主题介绍的 Dsl 项目中 DslDefinition.dsl 文件的结构[!INCLUDE[dsl](../modeling/includes/dsl_md.md)]定义的解决方案*域特定语言*。 DslDefinition.dsl 文件介绍的类和关系的域特定语言，以及关系图、 形状、 连接符、 序列化格式，并**工具箱**域特定语言的并将其编辑工具。 在域特定语言解决方案中，将根据 DslDefinition.dsl 文件中的信息生成可定义这些工具的代码。

通常情况下，使用*域特定语言设计器*编辑 DslDefinition.dsl 文件。 但是，它的原始格式为 XML，你可以在 XML 编辑器中打开 DslDefinition.dsl 文件。 在了解该文件所包含的信息以及如何组织它以供调试和扩展时，你会发现该文件很有用。

本主题中的示例取自“组件图”解决方案模板。 若要查看示例，请创建基于“组件模型”解决方案模板的域特定语言解决方案。 在创建该解决方案后，DslDefinition.dsl 文件将显示在域特定语言设计器中。 关闭该文件中，右键单击它**解决方案资源管理器**，依次指向**打开**，单击**XML 编辑器**，然后单击**确定**。

## <a name="sections-of-the-dsldefinitiondsl-file"></a>DslDefinition.dsl 文件的各个部分

根元素是\<Dsl >，其特性可标识域特定语言，在命名空间的名称和主版本号和次版本号进行版本控制。 `DslDefinitionModel` 架构将定义有效 DslDefinition.dsl 文件的内容和结构。

子元素的\<Dsl > 根元素如下所示：

### <a name="classes"></a>类

本部分将定义用于在生成的代码中生成类的每个域类。

### <a name="relationships"></a>关系

本部分将定义模型中的每个关系。 源和目标表示关系的两个方面。

### <a name="types"></a>类型

本部分将定义每个类型及其命名空间。 域属性具有两种类型。 `DomainEnumerations` 在模型中定义并将各个类型生成到 DomainModel.cs 中。 `ExternalTypes` 是指在其他位置定义的类型（例如 `String` 或 `Int32`），不会生成任何内容。

### <a name="shapes"></a>形状

本部分将定义用于描述模型在设计器中的显示方式的形状。 在“关系图”部分中，这些几何形状将映射到模型中的类。

### <a name="connectors"></a>连接符

本部分将定义显示在设计器中的连接符的外观。 在“关系图”部分中，这些几何样式说明将映射到模型中的特定关系。

### <a name="xmlserializationbehavior"></a>XmlSerializationBehavior

本部分将定义一个序列化方案，并提供有关如何将每个类保存到文件中的附加信息。

### <a name="explorerbehavior"></a>ExplorerBehavior

本部分将定义如何**DSL 资源管理器**窗口出现时用户正在编辑模型。

### <a name="connectionbuilders"></a>ConnectionBuilders

本部分将定义每个连接符工具的连接生成器（用于在任意两个可以连接的类之间建立链接的工具）。 本部分将确定你是否可以连接源类和目标类。

### <a name="diagram"></a>关系图

本部分将定义一个关系图，你可以使用它来指定背景色和根类等属性。 （根类是由整个关系图表示的域类。）“关系图”部分还包含 ShapeMap 和 ConnectorMap 元素，用于指定表示每个域类或关系的形状或连接符。

### <a name="designer"></a>Designer

本部分将定义一个设计器 （编辑器），它结合了**工具箱**，验证设置、 关系图和序列化方案。 “设计器”部分还将定义模型的根类，此根类通常也是关系图的根类。

### <a name="explorer"></a>资源管理器

本部分介绍**DSL 资源管理器**行为 （在 XmlSerializationBehavior 部分中定义）。

## <a name="monikers-in-the-dsldefinitiondsl-file"></a>DslDefinition.dsl 文件中的名字对象

在整个 DslDefinition.dsl 文件中，你可以使用名字对象对特定项进行交叉引用。 例如，每个关系定义都包含一个源子节和目标字节。 每个子节都包含可与该关系建立链接的对象类的名字对象：

```xml
<DomainRelationship ...        Name="LibraryHasMembers" Namespace="ExampleNamespace" >    <Source>      <DomainRole ...>
       <RolePlayer>
         <DomainClassMoniker Name="Library" />
       </RolePlayer>
     </DomainRole>
   </Source>
```

通常，引用项的命名空间（在本例中为 `Library` 域类）与进行引用的项的命名空间相同（在本例中为 LibraryHasMembers 域关系）。 在这些情况下，名字对象必须仅提供类的名称。 否则，应使用完整形式 /Namespace/Name：

```xml
<DomainClassMoniker Name="/ExampleNameSpace/Library" />
```

名字对象系统要求 XML 树中的同级类具有不同的名称。 因此，如果你尝试保存某个域特定语言定义（例如，它具有两个名称相同的类），则会发生验证错误。 在保存 DslDefinition 文件前，应始终更正此类重复名称错误，以便稍后可正确地重新加载该文件。

每个类型具有其自己的名字对象类型：DomainClassMoniker、 DomainRelationshipMoniker 等等。

## <a name="types"></a>类型

“类型”部分将 DslDefinition.dsl 文件包含的所有类型都指定为属性类型。 这些类型分为两类：外部类型（如 System.String）和枚举类型。

### <a name="external-types"></a>外部类型

组件图示例列出了一组标准基元类型，尽管只使用它们中的某些类型。

每个外部类型定义都仅由名称和命名空间组成，例如 String 和 System：

```xml
<ExternalType Name="String" Namespace="System" />
```

使用类型的全名，而不使用等效编译器关键字，如“string”。

外部类型并不仅限于标准库类型。

### <a name="enumerations"></a>枚举

典型的枚举规范与以下示例类似：

```xml
<DomainEnumeration IsFlags="true" Name="PageSort"          Namespace="Fabrikam.Wizard">
  <Literals>
    <EnumerationLiteral Name="Start" Value="1"/>
    <EnumerationLiteral Name="Decision" Value="2"/>
  </Literals>
</DomainEnumeration>
```

`IsFlags` 特性控制生成的代码是否带有 `[Flags]` 公共语言运行时 (CLR) 特性（可确定枚举值是否可按位进行组合）的前缀。 如果该特性设置为 true，则应为文本值指定 2 的幂的值。

## <a name="classes"></a>类

域特定语言的任意定义中的大多数元素都直接或间接为 `DomainClass` 的实例。 `DomainClass` 的子类包括 `DomainRelationship`、`Shape`、`Connector` 和 `Diagram`。 DslDefinition.dsl 文件的 `Classes` 部分列出了域类。

每个类都具有一组属性，并且可能具有一个基类。 在组件图示例中，`NamedElement` 是一个具有 `Name` 属性的抽象类，其类型为字符串：

```xml
<DomainClass Id="ee3161ca-2818-42c8-b522-88f50fc72de8"  Name="NamedElement" Namespace="Fabrikam.CmptDsl5"      DisplayName="Named Element"  InheritanceModifier="Abstract">
  <Properties>
    <DomainProperty Id="ef553cf0-33b5-4e34-a30b-cfcfd86f2261"   Name="Name" DisplayName="Name"  DefaultValue="" Category="" IsElementName="true">
      <Type>
        <ExternalTypeMoniker Name="/System/String" />
      </Type>
    </DomainProperty>
  </Properties>
</DomainClass>
```

`NamedElement` 是其他几个类（如 `Component`）的基类；对于该基类，除了继承自 `Name` 的 `NamedElement` 属性外，它还具有自己的属性。 BaseClass 子节点包含名字对象引用。 由于引用的类位于同一命名空间中，因此名字对象中仅需要其名称：

```xml
<DomainClass Name="Component" Namespace="Fabrikam.CmptDsl5"              DisplayName="Component">
  <BaseClass>
    <DomainClassMoniker Name="NamedElement" />
  </BaseClass>
  <Properties>
    <DomainProperty Name="Kind" DisplayName="Kind" >
      <Type>
        <ExternalTypeMoniker Name="/System/String" />
      </Type>
    </DomainProperty>
  </Properties>
```

每个域类（包括关系、形状、连接符和关系图）都可能具有以下特性和子节点：

- **Id.** 此属性是一个 GUID。 如果文件中未提供值，则域特定语言设计器将创建一个值。 （在本文档的插图中，通常忽略此特性以节省空间。）

- **名称和 Namespace。** 这些属性生成的代码中指定的名称和命名空间的类。 在域特定语言中它们必须都是唯一的。

- **InheritanceModifier。** 此属性是"抽象"、"密封"或 none。

- **显示名称。** 此属性是名称，将出现在**属性**窗口。 DisplayName 特性可以包含空格和其他标点。

- **GeneratesDoubleDerived.** 如果此属性设置为 true，将生成两个类，且其中一个是另一个的子类。 所有生成的方法都位于基类中，而构造函数位于子类中。 通过设置此特性，你可以在自定义代码中重写任何生成的方法。

- **HasCustomConstructor**。 如果将此特性设置为 true，则从生成的代码中忽略构造函数，以便你可以编写自己的版本。

- **属性**。 此特性包含生成的类的 CLR Attributes。

- **BaseClass**。 如果指定基类，它必须属于同一类型。 例如，域类必须具有另一个域类作为其基类，而隔离舱形状也必须具有一个隔离舱形状。 如果没有指定基类，则生成的代码中的类派生自标准框架类。 例如，域类派生自 `ModelElement`。

- **属性**。 此特性包含在事务控制下维护的且在保存模型时保留的属性。

- **ElementMergeDirectives**。 每个元素合并指令都可以控制将其他类的不同实例添加到父类的实例的方式。 你可以在本主题后面找到有关元素合并指令的详细信息。

- 为在 `Classes` 部分中列出的每个域类生成 C# 类。 在 Dsl\GeneratedCode\DomainClasses.cs 中生成 C# 类。

### <a name="properties"></a>属性

每个域属性都具有名称和类型。 该名称在域类及其可传递的基类中必须是唯一的。

该类型必须引用在 `Types` 部分中列出的某个类型。 通常，名字对象必须包含命名空间。

```xml
<DomainProperty Name="Name" DisplayName="Name"  DefaultValue="" Category="" IsElementName="true">
  <Type>
    <ExternalTypeMoniker Name="/System/String" />
  </Type>
</DomainProperty>
```

每个域属性还可以具有以下特性：

- **IsBrowsable**。 此属性确定该属性是否显示在**属性**窗口，当用户单击父类的对象。

- **IsUIReadOnly**。 此属性确定用户是否可以更改中的属性**属性**窗口或通过在其中显示该属性的修饰器。

- **类型**。 可以将此特性设置为 Normal、Calculated 或 CustomStorage。 如果将此特性设置为 Calculated，则你必须提供可确定该值的自定义代码，并且该属性将是只读的。 如果将此特性设置为 CustomStorage，则你必须提供可获取并设置值的代码。

- **IsElementName**。 如果将此特性设置为 true，则其值会在创建父类的实例时自动设置为唯一值。 仅针对每个类中的一个属性（必须具有字符串类型），将此特性设置为 true。 在组件图示例中，`Name` 中的 `NamedElement` 属性已将 `IsElementName` 设置为 true。 只要用户创建 `Component` 元素（派生自 `NamedElement`），该名称就会自动初始化为类似于“Component6”的名称。

- `DefaultValue`。 如果已指定此特性，则指定的值将分配给此类的新实例的特性。 如果设置 `IsElementName`，则 DefaultValue 特性将指定新字符串的初始部分。

- **类别**是在显示该属性将在其下的标头**属性**窗口。

## <a name="relationships"></a>关系

`Relationships` 部分列出了域特定语言中的所有关系。 每个 `Domain Relationship` 都是二进制的且定向的，以便将源类的成员链接到目标类的成员。 源类和目标类通常为域类，但也可以是与其他关系的关系。

例如，连接关系可将 OutPort 类的成员链接到 InPort 类的成员。 关系的每个链接实例都可以将 OutPort 的实例连接到 InPort 的实例。 由于关系是多对多的关系，因此每个 OutPort 都可能具有来自其上的许多连接链接，而且每个 InPort 实例都可能具有面向该实例的许多连接链接。

### <a name="source-and-target-roles"></a>源和目标角色

每个关系都包含具有以下特性的源和目标角色：

- `RolePlayer`属性引用了链接实例的域类：Outport 对应于源，inport 对应于目标。

- `Multiplicity` 特性具有四个可能值（ZeroMany、ZeroOne、One 和 OneMany）。 此特性是指可与一个角色扮演者关联的关系的链接数。

- `PropertyName` 特性将指定在角色扮演类中用于访问另一端的对象的名称。 在模板或自定义代码中使用此名称以遍历关系。 例如，将源角色的 `PropertyName` 特性设置为 `Targets`。 因此，以下代码将适用：

    ```
    OutPort op = ...; foreach (InPort ip in op.Targets) ...
    ```

     根据约定，如果重数为 ZeroMany 或 OneMany，则属性名称应采用复数形式。

     角色的重数是指可以与此角色的每个实例都关联的对方角色的个数。 例如，在关系 ComponentHasPorts 中，目标角色将 `RolePlayer` 特性设置为 Port、将 `PropertyName` 特性设置为 Component，并将 `Multiplicity` 特性设置为 ZeroOne。 因此，要使用此角色的相应代码是：

    ```
    ComponentPort p = ...; Component c = p.Component; if (c != null) ...
    ```

- 该角色的 `Name` 为在关系类中用于引用链接端的名称。 根据约定，角色名称应始终采用单数形式，因为每个链接在每一端上都仅具有一个实例。 以下代码将适用：

    ``` 
    Connection connectionLink = ...; OutPort op = connectionLink.Source;
    ```

- 默认情况下，将 `IsPropertyGenerator` 特性设置为 true。 如果将其设置为 false，则不会在角色扮演者类上创建任何属性。 （例如，在这种情况下，`op.Targets` 将不适用）。 但是，如果自定义代码显式使用此关系，则仍可以使用自定义代码来遍历关系或获取对链接本身的访问权限：

    ``` 
    OutPort op = ...; foreach (InPort ip in Connection.GetTargets(op)) ...
    foreach (Connection link in Connection.GetLinksToTargets(op)) ...
    ```

### <a name="relationship-attributes"></a>关系特性

除适用于所有类的特性和子节点外，每个关系还具有以下特性：

- **IsEmbedding**。 此布尔值特性指定该关系是否为嵌入树的一部分。 每个模型都必须通过其嵌入关系形成一个树。 因此，除非域类是某个模型的根，否则每个域类都必须至少是一个嵌入关系的目标类。

- **AllowsDuplicates**。 布尔值特性（在默认情况下为 false）仅适用于在源和目标元素处具有“多个”重数的关系。 它将确定语言用户是否可以通过同一关系的多个链接连接一对源和目标元素。

## <a name="designer-and-toolbox-tabs"></a>设计器和工具箱选项卡

主要部分**设计器**DslDefinition.dsl 文件的节是**ToolboxTab**元素。 一个设计器可以有多个这些元素，其中每个表示生成的设计器中的标题的部分**工具箱**。 每个**ToolboxTab**元素可以包含一个或多个**ElementTool**元素**ConnectionTool**和 / 或元素。

元素工具可以创建特定域类的实例。 当用户将元素工具拖到关系图上时，结果将由元素合并指令来确定，如本主题后面中有关元素合并指令的部分所述。

每个连接工具都可以调用特定的连接生成器。 一个连接生成器可以创建多个关系类型，具体取决于用户使用鼠标进行单击的位置，如连接生成器部分中所述。

这两种类型的工具都不能直接构造形状或连接符。 每个工具都可以实例化域类或域关系；然后，形状和连接符映射将确定该域类或域关系的显示方式。

## <a name="paths"></a>路径

域路径会在 DslDefinition.dsl 文件的多个位置中显示。 这些路径指定从某个模型（即域特定语言的实例）中的一个元素到另一个元素的一系列链接。 路径语法简单但很详细。

路径将以 `<DomainPath>...</DomainPath>` 标记的形式显示在 DslDefinition.dsl 文件中。 尽管路径可以通过多个链接导航，但在实际操作中大多数示例都仅遍历一个链接。

路径由一系列路径段组成。 每个路径段都是从对象到链接或者从链接到对象的跳跃。 因此，跳跃通常交替出现在较长的路径中。 第一次跳跃是从对象到链接，第二次跳跃是到该链接另一端的对象，第三次跳跃是到下一个链接，依此类推。 在关系本身为源或者为另一个关系的目标时，此序列偶尔会出现异常。

每个路径段都以关系名称开头。 在从对象到链接的跳跃中，关系位于句点和属性名称之前：“`Relationship . Property`”。 在从链接到对象的跳跃中，关系位于惊叹号和角色名称之前：“`Relationship ! Role`”。

组件图示例包含适用于 InPort 的 ShapeMap 的 ParentElementPath 中的路径。 此路径的开头如下所示：

``` 
    ComponentHasPorts.Component
```

在此示例中，InPort 是 ComponentPort 的子类且具有关系 ComponentHasPorts。 该属性称为 Component。

编写 C# 时对此模型，可以通过使用关系生成的属性上的每个相关类跳过一个步骤中的链接：

``` 
     InPort port; ...  Component c = port.Component;
```

但是，必须在路径语法中显式执行这两次跳跃。 由于此要求，你可以更容易地访问中间链接。 以下代码完成了从链接到 Component 的跳跃：

``` 
    ComponentHasPorts.Component / ! Component
```

（你可以省略与上一个路径段相同的关系名称。）

## <a name="element-merge-directives"></a>元素合并指令

当语言用户将某个项从**工具箱**拖到关系图中，构造此工具的类的实例。 此外，将在该实例和现有模型元素之间建立链接。 当语言用户将其从创建一些项，如组件或注释，**工具箱**拖动到关系图的空白部分。 其他项是在语言用户将其拖至其他主机元素上时创建的。 例如，OutPort 或 InPort 是在语言用户将其拖至组件上时创建的。

一个可能的主机类（如 Component）仅在其具有某个新元素类的元素合并指令时才接受该新元素。 例如，具有 Name="Component" 的 DomainClass 节点包含：

```xml
<DomainClass Name="Component" ...> ...
    <ElementMergeDirective>
      <Index>
        <DomainClassMoniker Name="ComponentPort" />
      </Index>
      <LinkCreationPaths>
        <DomainPath>ComponentHasPorts.Ports</DomainPath>
      </LinkCreationPaths>
    </ElementMergeDirective> ...
```

索引节点下的类名字对象引用可以接受的元素的类。 在这种情况下，ComponentPort 为 InPort 和 OutPort 的抽象基类。 因此，任一元素都是可接受的。

ComponentModel（语言的根类）具有适用于组件和注释的元素合并指令。 语言用户可以将这些类的项直接拖至关系图上，因为关系图的空白部分表示根类。 但是，ComponentModel 没有适用于 ComponentPort 的元素合并指令。 因此，语言用户无法将 InPorts 或 OutPorts 直接拖至关系图上。

元素合并指令确定创建哪个链接或哪些链接，以便新元素可以集成或合并到现有模型中。 对于 ComponentPort，将创建 ComponentHasPorts 的实例。 DomainPath 将同时标识可向其添加新类的父类 Ports 的关系和属性。

通过包含多个链接创建路径，你可以在元素合并指令上创建多个链接。 必须嵌入其中一个路径。

可以在一个链接创建路径中使用多个路径段。 在这种情况下，最后一个路径段定义必须创建的链接。 前面的路径段从父类导航到新链接应创建的对象。

例如，你可以将此元素合并指令添加到 Component 类：

```xml
<DomainClass Name="Component" ...> ...
  <ElementMergeDirective>
    <Index>
       <DomainClassMoniker Name="Comment"/>
    </Index>
    <LinkCreationPaths>
       <DomainPath>          ComponentModelHasComponents . ComponentModel / !ComponentModel         / ComponentModelHasComments.Comments       </DomainPath>
       <DomainPath>CommentsReferenceComponents.Comments</DomainPath>
    </LinkCreationPaths>
  </ElementMergeDirective>
```

然后，语言用户可以将注释拖至组件上，并且通过指向该组件的链接自动创建新的注释。

第一个链接创建路径将从 `Component` 导航至 `ComponentModel`，然后创建嵌入关系 `ComponentModelHasComments` 的实例。 第二个链接创建路将创建从主机组件到新注释的引用关系 CommentsReferenceComponents 的链接。 所有链接创建路径都必须从主机类开始，并且必须在指向新实例化的类的链接处结束。

## <a name="xmlclassdata"></a>XmlClassData

每个域类（包括关系和其他子类型）都可以具有在 `XmlClassData` 节点中提供的额外信息，该信息显示在 DslDefinition.dsl 文件的 `XmlSerializationBehavior` 部分下。 此信息特别涉及到如何在将模型保存到文件中时以序列化形式存储类的实例。

`XmlSerializationBehavior` 影响的大多数生成代码都位于 `Dsl\GeneratedCode\Serializer.cs` 中。

每个 `XmlClassData` 节点都包括以下子节点和特性：

- 名字对象节点，用于引用数据应用到的类。

- **XmlPropertyData**类上定义每个属性。

- **XmlRelationshipData**源于类的每个关系。 （关系还具有其自己的 XmlClassData 节点。）

- **TypeName**字符串属性，以确定生成的代码中的序列化帮助器类的名称。

- **ElementName**字符串，用于确定此类的序列化实例的 XML 标记。 根据约定，ElementName 通常与类名相同，不同之处在于首字母为小写。 例如，示例模型文件从以下内容开始：

    ```xml
    <componentModel ...
    ```

- **MonikerElementName**中用户的序列化的模型文件。 此特性引入了可引用此类的名字对象。

- **MonikerAttributeName**，用于标识名字对象内的 XML 属性的名称。 在此片段中的用户的序列化文件，定义特定于域的语言的作者**MonikerElementName**为"inPortMoniker"并**MonikerAttributeName**为"path":

    ```xml
    <inPortMoniker path="//Component2/InPort1" />
    ```

### <a name="connectionbuilders"></a>ConnectionBuilders

为每个连接工具定义一个连接生成器。 每个连接生成器都由一个或多个 LinkConnectDirective 元素组成，其中每个元素都包含一个或多个 SourceDirective 元素以及一个或多个 TargetDirective 元素。 在单击连接工具之后，用户可以从映射到 SourceDirective 元素列表中显示的某个模型元素的任何形状开始连接。 然后，可以在映射到 TargetDirective 元素列表中显示的某个元素的形状上完成该连接。 实例化的关系类取决于开始连接的位置所指定的 LinkConnectDirective 元素。

### <a name="xmlpropertydata"></a>XmlPropertyData

一个**DomainPropertyMoniker**属性标识该数据所引用的属性。 此特性必须为封闭 ClassData 的类的属性。

**XmlName**特性提供了相应的属性名称，应显示在 XML 中。 根据约定，此字符串与属性名称相同，不同之处在于首字母为小写。

默认情况下**表示形式**属性设置为属性。 如果**表示形式**子级设置为元素，在 XML 中创建节点。 如果**表示形式**是设置为 Ignore，该属性不序列化。

**IsMonikerKey**并**IsMonikerQualifier**属性提供属性中标识父类的实例的角色。 可以设置**IsMonikerKey**为 true 是中定义或继承的类的一个属性。 此特性将标识父类的单个实例。 设置为 `IsMonikerKey` 的属性通常为一个名称或其他密钥标识符。 例如，`Name` 字符串属性是 NamedElement 及其派生类的名字对象密钥。 当用户将模型保存到文件中时，此特性必须包含每个实例的值，并且在嵌入关系的树中这些值在同级中是唯一的。

在序列化模型文件中，元素的完整名字对象是一个路径，该路径从模型根沿着嵌入关系的树向下，从而在每个位置处引用名字对象密钥。 例如，InPorts 嵌入在 Components 中，Components 又反过来嵌入在模型根中。 因此，一个有效的名字对象为：

```xml
<inPortMoniker name="//Component2/InPort1" />
```

可以设置**IsMonikerQualifier**属性为字符串属性，并提供了另外一种构造元素的完整名称。 例如，在 DslDefinition.dsl 文件中， **Namespace**是一个名字对象限定符。

### <a name="xmlrelationshipdata"></a>XmlRelationshipData

在序列化模型文件中，（嵌入关系和引用关系中的）链接由关系源端的子节点表示。 对于嵌入关系，子节点包含一个子树。 对于引用关系，子节点包含一个引用树的其他部分的名字对象。

**XmlRelationshipData**属性中**XmlClassData**属性定义完全如何嵌套子节点的源元素中。 源域类上的每个关系具有一个**XmlRelationshipData**属性。

**DomainRelationshipMoniker**属性标识源自该类的关系之一。

**RoleElementName**特性提供了在序列化数据中包含的子节点的 XML 标记名称。

例如，DslDefinition.dsl 文件包含：

```xml
<XmlClassData ElementName="component" ...>
  <DomainClassMoniker Name="Component" />
  <ElementData>
    <XmlRelationshipData RoleElementName="ports">
      <DomainRelationshipMoniker Name="ComponentHasPorts" />
    </XmlRelationshipData>
```

因此，序列化文件包含：

```xml
<component name="Component1"> <!-- parent -->
   <ports> <!-- role -->
     <outPort name="OutPort1"> <!-- child element -->
       ...
     </outPort>
   </ports> ...
```

如果**UseFullForm**属性设置为 true，引入额外的嵌套层。 该层表示关系本身。 如果该关系具有属性，则必须将该特性设置为 true。

```xml
<XmlClassData ElementName="outPort">
   <DomainClassMoniker Name="OutPort" />
   <ElementData>
     <XmlRelationshipData UseFullForm="true" RoleElementName="targets">
       <DomainRelationshipMoniker Name="Connection" />
     </XmlRelationshipData>
   </ElementData>
 </XmlClassData>
```

序列化文件包含：

```xml
<outPort name="OutPort1">  <!-- Parent -->
   <targets>  <!-- role -->
     <connection sourceRoleName="X">  <!-- relationship link -->
         <inPortMoniker name="//Component2/InPort1" /> <!-- child -->
     </connection>
    </targets>
  </outPort>
```

（连接关系具有其自己的 XML 类数据，该数据提供了此关系的元素和特性名称。）

如果**OmitElement**属性设置为 true 时，关系角色省略名称时，它缩写序列化的文件并不明确，如果两个类具有多个关系。 例如：

```xml
<component name="Component3">
  <!-- only one relationship could get here: -->
  <outPort name="OutPort1">
     <targets> ...
```

### <a name="serialization-of-a-domain-specific-language-definition"></a>域特定语言定义的序列化

DslDefinition.dsl 文件本身就是一个序列化文件并且符合域特定语言定义。 以下是 XML 序列化定义的一些示例：

- **Dsl** RootClass 节点和关系图的类。 在 `Dsl` 下方嵌入了 DomainClass、DomainRelationship 和其他元素。

- **类**是**RoleElementName**的特定于域的语言和 DomainClass 之间的关系。

```xml
<Dsl Name="CmptDsl5" ...>
  <Classes>
    <DomainClass Name="NamedElement" InheritanceModifier="Abstract" ...
```

- **XmlSerializationBehavior**特性嵌入在`Dsl`属性，但**OmitElement**特性已设置在嵌入关系上。 因此，不会干扰任何 `RoleElementName` 特性。 与此相反， **ClassData**属性是`RoleElementName`属性之间的嵌入关系**XmlSerializationBehavior**属性和一个**XmlClassData**属性。

```xml
<Dsl Name="CmptDsl5" ...> ...
  <XmlSerializationBehavior Name="ComponentsSerializationBehavior" >
    <ClassData>
      <XmlClassData ...>...</XmlClassData>
      <XmlClassData ...>...</XmlClassData>
```

- ConnectorHasDecorators 是 `Connector` 和 `Decorator` 之间的嵌入关系。 已对 `UseFullForm` 进行设置，以便关系名称与连接符对象中的每个链接的关系属性列表一同显示。 但是，还对 `OmitElement` 进行了设置，以便 `RoleElementName` 没有包含嵌入在 `Connector` 内的多个链接：

```xml
<Connector Name="AssociationLink" ...>
  <ConnectorHasDecorators Position="TargetTop" ...>
    <TextDecorator Name="TargetRoleName"   />
  </ConnectorHasDecorators>
  <ConnectorHasDecorators Position="SourceTop" ...>
    <TextDecorator Name="SourceRoleName"   />
  </ConnectorHasDecorators>
</Connector>
```

## <a name="shapes-and-connectors"></a>形状和连接符

形状和连接符定义除了继承域类中的特性和子节点外，还继承以下内容：

- `Color` 和 `Line``Style` 特性。

- **ExposesFillColorAsProperty**和几个类似的属性。 这些布尔值特性通过用户使相应的属性处于可变状态。 通常情况下，当语言用户单击关系图上的形状时，属性，将出现在**属性**窗口是指该形状映射的域类实例。 如果将 `ExposesFillColorAsProperty` 设置为 true，则还将显示形状本身的属性。

- **ShapeHasDecorators**。 此特性的实例可针对每个文本、图标或展开/折叠修饰器出现。 （在 DslDefinition.dsl 文件中，如果将 `ShapeHasDecorators` 设置为 true，则 `UseFullForm` 与其之间存在关系。）

## <a name="shape-maps"></a>形状映射

形状映射将确定某个给定域类的实例（由形状表示）如何显示在屏幕上。 形状和连接符映射同时显示在 DslDefinition.dsl 文件的 `Diagram` 部分下。

如以下示例所示，`ShapeMap` 元素至少具有域类的名字对象、形状的名字对象以及 `ParentElementPath` 元素：

```xml
<ShapeMap>
  <DomainClassMoniker Name="InPort" />
  <ParentElementPath>
    <DomainPath>ComponentHasPorts.Component/!Component</DomainPath>
  </ParentElementPath>
  <PortMoniker Name="InPortShape" />
</ShapeMap>
```

将 `ParentElementPath` 元素的主要功能嵌入注释中，以便对象的相同类可以按不同形状显示在不同的上下文中。 例如，如果 `InPort` 也可以嵌入注释中，则 `InPort` 可能出于此目的而显示为不同形状。

其次，路径将确定形状如何与其父级相关。 未在 DslDefinition.dsl 文件中的形状之间定义嵌入结构。 必须根据形状映射推断该结构。 父形状是映射到父元素路径标识的域元素的形状。 在这种情况下，路径将标识 `InPort` 所属的组件。 在其他形状映射中，Component 类将映射到 ComponentShape。 因此，新的 `InPort` 形状将从其组件的 `ComponentShape` 的子形状形成。

如果改为将 InPort 形状附加到关系图，则父元素路径将需要针对映射到该关系图的组件模型采取其他步骤：

```
ComponentHasPorts . Component / ! Component /    ComponentModelHasComponents . ComponentModel / ! ComponentModel
```

模型的根不具有形状映射。 而该根可以直接从具有 `Class` 元素的关系图中引用：

```xml
<Diagram Name="ComponentDiagram" >
    <Class>
      <DomainClassMoniker Name="ComponentModel" />
    </Class>...
```

### <a name="decorator-maps"></a>修饰器映射

修饰器映射使映射类中的属性与形状上的修饰器相关联。 如果属性为枚举类型或布尔值类型，则该属性的值可以确定修饰器是否可见。 如果修饰器为文本修饰器，则可以显示该属性的值，并且用户可对其进行编辑。

### <a name="compartment-shape-maps"></a>隔离舱形状映射

隔离舱形状映射为形状映射的子类型。

## <a name="connector-maps"></a>连接符映射

最小连接符映射将引用连接符和关系：

```xml
<ConnectorMap>
  <ConnectorMoniker Name="CommentLink" />
  <DomainRelationshipMoniker Name="CommentsReferenceComponents" />
</ConnectorMap>
```

连接符映射还可以包含修饰器映射。

## <a name="see-also"></a>请参阅

- [域特定语言工具术语表](https://msdn.microsoft.com/ca5e84cb-a315-465c-be24-76aa3df276aa)
- [如何定义域特定语言](../modeling/how-to-define-a-domain-specific-language.md)
- [了解模型、类和关系](../modeling/understanding-models-classes-and-relationships.md)