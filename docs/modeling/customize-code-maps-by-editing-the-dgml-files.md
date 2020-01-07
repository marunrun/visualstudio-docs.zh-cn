---
title: 通过编辑 DGML 文件自定义代码图
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- dependency graphs, creating path aliases
- dependency graphs, linking items to nodes
- graph documents, creating path aliases
- dependency graphs, grouping nodes
- graph documents, editing
- graph documents, linking items to nodes
- graph documents, customizing
- graph documentings, assigning categories and properties
- dependency graphs, editing
- dependency graphs, customizing
- graph documents, grouping nodes
- dependency graphs, assigning categories and properties
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2b79fd73713de535c11062fd6396abde6b1a0131
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75590509"
---
# <a name="customize-code-maps-by-editing-the-dgml-files"></a>通过编辑 DGML 文件自定义代码图

若要自定义代码图，可以编辑其定向关系图标记语言（.dgml）文件。 例如，可以编辑元素来指定自定义样式，向代码元素和链接分配属性和类别，或将文档（或 URL）链接到代码元素（或链接）。 有关 DGML 元素的详细信息，请参阅[定向关系图标记语言（DGML）引用](../modeling/directed-graph-markup-language-dgml-reference.md)。

在文本编辑器或 XML 编辑器中编辑代码图的 .dgml 文件。 如果该地图是你的 Visual Studio 解决方案的一部分，请在**解决方案资源管理器**中将其选中，打开快捷菜单，然后选择 "**打开**方式"、" **XML （文本）编辑器**"。

> [!NOTE]
> 若要创建代码图，必须具有 Visual Studio Enterprise 版本。 在 Visual Studio 中编辑代码图时，Visual Studio 会在保存 .dgml 文件时删除所有未使用的 DGML 元素和属性以进行清理。 当手动添加新链接时，它还将自动创建代码元素。 当你保存 .dgml 文件时，你添加到元素的任何特性可能会按字母顺序重新排列。

## <a name="OrganizeNodes"></a>分组代码元素
 你可以添加新组，也可以将现有节点转换为一个组。

1. 在文本编辑器或 XML 编辑器中打开 .dgml 文件。

2. 若要将代码元素转换为一个组，请查找该代码元素的 `<Node/>` 元素。

    \- 或 -

    若要添加新组，请查找 `<Nodes>` 部分。 创建新的 `<Node/>` 元素。

3. 在 `<Node/>` 元素中，添加一个 `Group` 特性以指定组显示为展开状态还是折叠状态。 例如：

   ```xml
   <Nodes>
      <Node Id="MyFirstGroup" Group="Expanded" />
      <Node Id="MySecondGroup" Group="Collapsed" />
   </Nodes>
   ```

4. 在 `<Links>` 部分，确保对于组代码元素与其子代码元素之间的每个关系都存在具有以下特性的 `<Link/>` 元素：

   - 指定组代码元素的 `Source` 特性

   - 指定子代码元素的 `Target` 特性

   - 指定组代码元素与其子代码元素之间的 `Category` 关系的 `Contains` 特性

     例如：

   ```xml
   <Links>
      <Link Category="Contains" Source="MyFirstNewGroup" Target="FirstGroupChildOne" />
      <Link Category ="Contains" Source="MyFirstNewGroup" Target="FirstGroupChildTwo" />
      <Link Category ="Contains" Source="MySecondNewGroup" Target="SecondGroupChildOne" />
      <Link Category="Contains" Source="MySecondNewGroup" Target="SecondGroupChildTwo" />
   </Links>
   ```

    有关 `Category` 特性的详细信息，请参阅向[代码元素和链接分配类别](#AssignCategories)。

## <a name="ChangeGraphStyle"></a>更改地图的样式
 你可以通过编辑代码图的 .dgml 文件来更改代码图的背景色和边框颜色。 若要更改代码元素和链接的样式，请参阅[更改代码元素和链接的样式](#Highlight)。

1. 在文本编辑器或 XML 编辑器中打开 .dgml 文件。

2. 在 `<DirectedGraph>` 元素中，添加以下任何特性以更改其样式：

     背景色

    ```xml
    Background="ColorNameOrHexadecimalValue"
    ```

     边框颜色

    ```xml
    Stroke="StrokeValue"
    ```

     例如：

    ```xml
    <DirectedGraph Background="Green" xmlns="http://schemas.microsoft.com/vs/2009/dgml" >
       ...
       ...
    </DirectedGraph>
    ```

## <a name="Highlight"></a>更改代码元素和链接的样式

### <a name="CreateCustomStyles"></a>
 你可以将自定义样式应用于以下代码元素：

- 单个代码元素和链接

- 代码元素和链接组

- 基于特定条件的代码元素和链接组

> [!TIP]
> 如果很多代码元素或链接具有重复的样式，则可以考虑向这些代码元素或链接应用一个类别，然后向该类别应用一个样式。 有关详细信息，请参阅向[代码元素和链接分配类别](#AssignCategories)和向[代码元素和链接分配属性](#AssignProperties)。

##### <a name="to-apply-a-custom-style-to-a-single-code-element"></a>将自定义样式应用于单个代码元素

1. 在文本编辑器或 XML 编辑器中打开 .dgml 文件。

2. 查找代码元素的 `<Node/>` 元素。 添加以下任何特性，以自定义其样式：

     背景色

    ```xml
    Background="ColorNameOrHexadecimalValue"
    ```

     外边框

    ```xml
    Stroke="ColorNameOrHexadecimalValue"
    ```

     轮廓粗细

    ```xml
    StrokeThickness="StrokeValue"
    ```

     文本颜色

    ```xml
    Foreground="ColorNameOrHexadecimalValue"
    ```

     图标

    ```xml
    Icon="IconFilePathLocation"
    ```

     文本大小

    ```xml
    FontSize="FontSizeValue"
    ```

     文本类型

    ```xml
    FontFamily="FontFamilyName"
    ```

     文本粗细

    ```xml
    FontWeight="FontWeightValue"
    ```

     文本样式

    ```xml
    FontStyle="FontStyleName"
    ```

     例如，可以指定 `Italic` 作为文本样式。

     纹理

    ```xml
    Style="Glass"
    ```

     - 或 -

    ```xml
    Style="Plain"
    ```

     形状

     若要将形状替换为图标，请将 `Shape` 属性设置为 `None` 并将 `Icon` 属性设置为包含图标文件的路径。

    ```xml
    Shape="ShapeFilePathLocation"
    ```

     例如：

    ```xml
    <Nodes>
       <Node Id="MyNode" Background="#FF008000" Stroke="#FF000000"
       Foreground="#FFFFFFFF" Icon="...\Icons\Globe.png"/>
    </Nodes>
    ```

##### <a name="to-apply-a-custom-style-to-a-single-link"></a>将自定义样式应用于单个链接

1. 在文本编辑器或 XML 编辑器中打开 .dgml 文件。

2. 查找包含源代码元素名称和目标代码元素名称的 `<Link/>` 元素。

3. 在 `<Link/>` 元素中，添加以下任何特性以自定义其样式：

     边框和箭头颜色

    ```xml
    Stroke="ColorNameOrHexadecimalValue"
    ```

     轮廓粗细

    ```xml
    StrokeThickness="StrokeValue"
    ```

     轮廓样式

    ```xml
    StrokeDashArray="StrokeArrayValues"
    ```

     例如：

    ```xml
    <Links>
       <Link Source="MyFirstNode" Target="MySecondNode" Background="Green" Stroke="#FF000000" StrokeDashArray="2,2"/>
    </Links>
    ```

##### <a name="to-apply-custom-styles-to-a-group-of-code-elements-or-links"></a>将自定义样式应用于代码元素或链接组

1. 在文本编辑器或 XML 编辑器中打开 .dgml 文件。

2. 如果 `<Styles></Styles>` 元素不存在，请在 `<DirectedGraph></DirectedGraph>` 元素下的 `<Links></Links>` 元素后面添加一个该元素。

3. 在 `<Styles></Styles>` 元素中的 `<Style/>` 元素下，指定以下特性：

   - `TargetType="Node` &#124; `Link | Graph"`

   - `GroupLabel="` *NameInLegendBox* `"`

   - `ValueLabel="` *NameInStylePickerBox* `"`

     若要将自定义样式应用于所有目标类型，请不要使用条件。

##### <a name="to-apply-a-conditional-style-to-groups-of-code-elements-or-links"></a>将条件样式应用于代码元素或链接组

1. 在文本编辑器或 XML 编辑器中打开 .dgml 文件。

2. 在 `<Style/>` 元素中，添加一个包含 `<Condition/>` 特性的 `Expression` 元素，以指定返回布尔值的表达式。

    例如：

   ```xml
   <Condition Expression="MyCategory"/>
   ```

    - 或 -

   ```xml
   <Condition Expression="MyCategory > 100"/>
   ```

    - 或 -

   ```xml
   <Condition Expression="HasCategory('MyCategory')"/>
   ```

    此表达式使用以下 Backus-Naur 形式 (BNF) 语法：

    \<Expression >：： = \<BinaryExpression > &#124; \<UnaryExpression > &#124; "（"\<Expression > "）" &#124; \<b > &#124; \<> \<&#124; >

    \<BinaryExpression >：： = \<Expression > \<> \<表达式 >

    \<UnaryExpression >：： = "！" \<表达式 > &#124; "+" \<表达式 > &#124; "-" \<表达式 >

    \<运算符 >：： = "<" &#124; "\<=" &#124; "=" &#124; "> =" &#124; ">" &#124; "！ =" &#124; "、" &#124; "和" &#124; "+" &#124; "*" &#124; "/" &#124; "-"

    \<b >：： = \<b > &#124; \<MemberBinding > "." \<MemberBinding >

    \<MemberBinding >：： = \<MethodCall > &#124; \<PropertyGet >

    \<MethodCall >：： = \<标识符 > "（" \<G s > "）"

    \<PropertyGet >：： = 标识符

    \<G s >：： = \<表达式 > &#124; \<表达式 > "，" \<g s > &#124; \<空 >

    \<标识符 >：： = [^。 ]*

    \<文字 >：： = 单个或用双引号括起来的字符串

    \<号 >：： = 带可选小数点的数字字符串

    可以指定多个 `<Condition/>` 元素，这些元素必须全部为 true 才能应用样式。

3. 在 `<Condition/>` 元素后的下一行上，添加一个或多个 `<Setter/>` 元素，以指定要应用于满足条件的代码图、代码元素或链接的 `Property` 特性和固定 `Value` 特性或者计算所得的 `Expression` 特性。

    例如：

   ```xml
   <Setter Property="BackGround" Value="Green"/>
   ```

   作为一个完整的简单示例，以下条件根据代码元素的 `Passed` 类别是设置为 `True` 还是 `False` 来指定该代码元素显示为绿色或红色：

```xml
<?xml version="1.0" encoding="utf-8"?>
<DirectedGraph xmlns="http://schemas.microsoft.com/vs/2009/dgml">
   <Nodes>
      <Node Id="MyFirstNode" Passed="True" />
      <Node Id="MySecondNode" Passed="False" />
   </Nodes>
   <Links>
   </Links>
   <Styles>
      <Style TargetType="Node" GroupLabel="Passed" ValueLabel="True">
         <Condition Expression="Passed='True'"/>
         <Setter Property="Background" Value="Green"/>
      </Style>
      <Style TargetType="Node" GroupLabel="Passed" ValueLabel="False">
         <Condition Expression="Passed='False'"/>
         <Setter Property="Background" Value="Red"/>
      </Style>
   </Styles>
</DirectedGraph>
```

 下表包括一些您可以使用的示例条件：

 根据代码的行数来设置字号，这样也会更改代码元素的大小。 此示例使用单个条件表达式来设置多个属性：`FontSize` 和 `FontFamily`。

```xml
<?xml version="1.0" encoding="utf-8"?>
<DirectedGraph xmlns="http://schemas.microsoft.com/vs/2009/dgml">
<Nodes>
   <Node Id="Class1" LinesOfCode ="200" />
   <Node Id="Class2" LinesOfCode ="1000" />
   <Node Id="Class3" LinesOfCode ="20" />
</Nodes>
<Properties>
   <Property Id="LinesOfCode" Label="LinesOfCode" Description="LinesOfCode" DataType="System.Int32" />
</Properties>
<Styles>
   <Style TargetType="Node" GroupLabel="LinesOfCode" ValueLabel="Function">
      <Condition Expression="LinesOfCode > 0" />
      <Setter Property="FontSize" Expression="Math.Max(9,Math.Sqrt(LinesOfCode))" />
      <Setter Property="FontFamily" Value="Papyrus" />
   </Style>
</Styles>
</DirectedGraph>
```

 基于 `Coverage` 属性设置代码元素的背景色。 类似于 `if-else` 语句，将按样式的出现顺序来计算样式。

 在此示例中：

1. 如果 `Coverage` > 80，则将 `Background` 属性设置为绿色。

2. 否则，如果 `Coverage` > 50，则将 `Background` 属性设置为基于 `Coverage` 属性值的橙色底纹。

3. 否则基于 `Background` 属性的值将 `Coverage` 属性设置为红色阴影。

```xml
<?xml version="1.0" encoding="utf-8"?>
<DirectedGraph xmlns="http://schemas.microsoft.com/vs/2009/dgml">
<Nodes>
   <Node Id="Class1" Coverage="58" />
   <Node Id="Class2" Coverage="95" />
   <Node Id="Class3" Coverage="32" />
</Nodes>
<Properties>
   <Property Id="Coverage" Label="Coverage" Description="Code coverage as a percentage of blocks" DataType="Double" />
</Properties>
<Styles>
   <Style TargetType="Node" GroupLabel="Coverage" ValueLabel="Good">
      <Condition Expression="Coverage > 80" />
      <Setter Property="Background" Value="Green" />
   </Style>
   <Style TargetType="Node" GroupLabel="Coverage" ValueLabel="OK">
      <Condition Expression="Coverage > 50" />
      <Setter Property="Background" Expression="Color.FromRgb(180 * Math.Max(1, (80 - Coverage) / 30), 180, 0)" />
   </Style>
   <Style TargetType="Node" GroupLabel="Coverage" ValueLabel="Bad">
      <Setter Property="Background" Expression="Color.FromRgb(180, 180 * Coverage / 50, 0)" />
   </Style>
</Styles>
</DirectedGraph>
```

 将 `Shape` 属性设置为 `None` 以使图标替换形状。 使用 `Icon` 属性指定图标的位置。

```xml
<DirectedGraph xmlns="http://schemas.microsoft.com/vs/2009/dgml">
<Nodes>
   <Node Id="Automation" Category="Test" Label="Automation" />
   <Node Id="C# Provider" Category="Provider" Label="C# Provider" />
</Nodes>
<Categories>
   <Category Id="Provider" Icon="...\Icons\Module.png" Shape="None" />
   <Category Id="Test" Icon="...\Icons\Page.png" Shape="None" />
</Categories>
<Properties>
   <Property Id="Icon" DataType="System.String" />
   <Property Id="Label" Label="Label" Description="Displayable label of an Annotatable object" DataType="System.String" />
   <Property Id="Shape" DataType="System.String" />
</Properties>
<Styles>
   <Style TargetType="Node" GroupLabel="Group" ValueLabel="Has category">
      <Condition Expression="HasCategory('Group')" />
      <Setter Property="Background" Value="#80008080" />
   </Style>
   <Style TargetType="Node">
      <Setter Property="HorizontalAlignment" Value="Center" />
   </Style>
</Styles>
</DirectedGraph>
```

## <a name="AssignProperties"></a>向代码元素和链接分配属性
 你可以通过向代码元素和链接分配属性来组织代码元素和链接。 例如，可以选择具有特定属性的代码元素，以便能够对这些代码元素进行分组、更改它们的样式或隐藏它们。

#### <a name="to-assign-a-property-to-a-code-element"></a>向代码元素分配属性

1. 在文本编辑器或 XML 编辑器中打开 .dgml 文件。

2. 查找该代码元素的 `<Node/>` 元素。 指定属性的名称和属性的值。 例如：

    ```xml
    <Nodes>
       <Node Id="MyNode" MyPropertyName="PropertyValue" />
    </Nodes>
    ```

3. 将 `<Property/>` 元素添加到 `<Properties>` 部分以指定特性，例如其可见名称和数据类型：

    ```xml
    <Properties>
       <Property Id="MyPropertyName" Label="My Property" DataType="System.DataType"/>
    </Properties>
    ```

#### <a name="to-assign-a-property-to-a-link"></a>为链接分配属性

1. 在文本编辑器或 XML 编辑器中打开 .dgml 文件。

2. 查找包含源代码元素名称和目标代码元素名称的 `<Link/>` 元素。

3. 在 `<Node/>` 元素中，指定属性的名称和属性的值。 例如：

    ```xml
    <Links>
       <Link Source="MyFirstNode" Target="MySecondNode" MyPropertyName="PropertyValue" />
    </Links>
    ```

4. 将 `<Property/>` 元素添加到 `<Properties>` 部分以指定特性，例如其可见名称和数据类型：

    ```xml
    <Properties>
       <Property Id="MyPropertyName" Label="My Property Name" DataType="System.DataType"/>
    </Properties>
    ```

## <a name="AssignCategories"></a>向代码元素和链接分配类别
 以下各节演示如何通过将类别分配给代码元素来组织代码元素，以及如何创建可帮助组织代码元素并通过使用继承将特性添加到子类别的分层类别。

#### <a name="to-assign-a-category-to-a-code-element"></a>向代码元素分配类别

- 在文本编辑器或 XML 编辑器中打开 .dgml 文件。

- 查找所需代码元素的 `<Node/>` 元素。

- 在 `<Node/>` 元素中，添加一个 `Category` 特性以指定类别的名称。 例如：

    ```xml
    <Nodes>
       <Node Id="MyNode" Category="MyCategory" />
    </Nodes>
    ```

     向 `<Category/>` 部分添加一个 `<Categories>` 元素，以便能够使用 `Label` 特性来指定该类别的显示文本：

    ```xml
    <Categories>
       <Category Id="MyCategory" Label="My Category" />
    </Categories>
    ```

#### <a name="to-assign-a-category-to-a-link"></a>为链接分配类别

1. 在文本编辑器或 XML 编辑器中打开 .dgml 文件。

2. 查找包含源代码元素名称和目标代码元素名称的 `<Link/>` 元素。

3. 在 `<Link/>` 元素中，添加一个 `Category` 特性以指定类别的名称。 例如：

    ```xml
    <Links>
       <Link Source="MyFirstNode" Target="MySecondNode" Category="MyCategory"
    </Links>
    ```

4. 向 `<Category/>` 部分添加一个 `<Categories>` 元素，以便能够使用 `Label` 特性来指定该类别的显示文本：

    ```xml
    <Categories>
       <Category Id="MyCategory" Label="My Category" />
    </Categories>
    ```

#### <a name="to-create-hierarchical-categories"></a>创建分层类别

1. 在文本编辑器或 XML 编辑器中打开 .dgml 文件。

2. 为父类别添加一个 `<Category/>` 元素，然后将 `BasedOn` 特性添加到子类别的 `<Category/>` 元素。

     例如：

    ```xml
    <Nodes>
       <Node Id="MyFirstNode" Label="My First Node" Category= "MyCategory" />
       <Node Id="MySecondNode" Label="My Second Node" />
    </Nodes>
    <Links>
       <Link Source="MyFirstNode" Target="MySecondNode" />
    </Links>
    <Categories>
       <Category Id="MyCategory" Label="My Category" BasedOn="MyParentCategory"/>
       <Category Id="MyParentCategory" Label="My Parent Category" Background="Green"/>
    </Categories>
    ```

     在此示例中，`MyFirstNode` 的背景为绿色，因为它的 `Category` 特性继承 `Background` 的 `MyParentCategory` 特性。

## <a name="AddReferences"></a>将文档或 Url 链接到代码元素和链接
 可以通过以下方式将文档或 URL 链接到代码元素或链接：编辑代码图的 .dgml 文件并将 `Reference` 特性添加到代码元素的 `<Node/>` 元素或链接的 `<Link/>` 元素。 然后，你可以打开并查看代码元素或链接的内容。 `Reference` 特性指定该内容的路径。 此路径可能是相对于 .dgml 文件位置的路径，也可能是绝对路径。

> [!CAUTION]
> 如果使用相对路径，并将 .dgml 文件移至其他位置，则将不再解析这些路径。 当你尝试打开并查看链接内容时，将出现表示内容无法查看的错误。

 例如，你可能希望链接以下代码元素：

- 若要描述某个类的更改，则可以将工作代码元素、文档或另一个 .dgml 文件的 URL 链接到该类的代码元素。

- 你可以将依赖关系图链接到表示软件逻辑体系结构中的层的组代码元素。

- 若要显示有关公开某接口的组件的更多信息，可以将组件图链接到该接口的代码元素。

- 将代码元素链接到 Team Foundation Server 工作项或 bug，或与代码元素相关的一些其他信息。

#### <a name="to-link-a-document-or-url-to-a-code-element"></a>将文档或 URL 链接到代码元素

1. 在文本编辑器或 XML 编辑器中打开 .dgml 文件。

2. 查找所需代码元素的 `<Node/>` 元素。

3. 执行下表中的任务之一：

    单个代码元素

   - 在 `<Node/>` 或 `<Link/>` 元素中，添加 `Reference` 特性以指定代码元素的位置。

     > [!NOTE]
     > 每个元素只能具有一个 `Reference` 特性。

     例如：

   ```xml
   <Nodes>
      <Node Id="MyNode" Reference="MyDocument.txt" />
   </Nodes>
   <Properties>
      <Property Id="Reference" Label="My Document" DataType="System.String" IsReference="True" />
   </Properties>
   ```

    多个代码元素

   1. 在 `<Node/>` 或 `<Link/>` 元素中，添加一个新特性以指定每个引用的位置。

   2. 在 `<Properties>` 部分：

      1. 为每个新引用类型添加一个 `<Property/>` 元素。

      2. 将 `Id` 特性设置为新引用特性的名称。

      3. 添加 `IsReference` 特性并将其设置为 `True`，以使引用显示在代码元素的 "**跳到引用**" 快捷菜单上。

      4. 使用 `Label` 特性来指定代码元素的 "**跳到引用**" 快捷菜单上的显示文本。

      例如：

   ```xml
   <Nodes>
      <Node Id="MyNode" SequenceDiagram="MySequenceDiagram.sequencediagram" ActiveBugs="MyActiveBugs.wiq"/>
   </Nodes>
   <Properties>
      <Property Id="SequenceDiagram" Label="My Sequence Diagram" DataType="System.String" IsReference="True" />
      <Property Id="ActiveBugs" Label="Active Bugs" DataType="System.String" IsReference="True" />
   </Properties>
   ```

    在代码图上，代码元素的名称带下划线显示。 当您打开代码元素或链接的快捷菜单时，您将看到一个 "**跳到引用**" 快捷菜单，其中包含要选择的链接代码元素。

4. 使用 `ReferenceTemplate` 特性来指定多个引用使用的公共字符串（例如 URL），而不是在引用中重复该字符串。

    `ReferenceTemplate` 特性为引用的值指定占位符。 在下面的示例中，`{0}` 特性中的 `ReferenceTemplate` 占位符将替换为 `MyFirstReference` 元素中 `MySecondReference` 和 `<Node/>` 特性的值，以生成完整路径：

   ```xml
   <Nodes>
      <Node Id="MyNode" MyFirstReference="MyFirstDocument" MySecondReference="MySecondDocument"/>
      <Node Id="MySecondNode" MyFirstReference="AnotherFirstDocument" MySecondReference="AnotherSecondDocument"/>
   </Nodes>
   <Properties>
      <Property Id="MyFirstReference" Label="My First Document" DataType="System.String" IsReference="True" ReferenceTemplate="http://www.Fabrikam.com/FirstDocuments/{0}.asp"/>
      <Property Id="MySecondReference" Label="My Second Document" DataType="System.String" IsReference="True" ReferenceTemplate=" http://www.Fabrikam.com/SecondDocuments/{0}.asp"/>
   </Properties>
   ```

5. 若要查看引用的代码元素或代码图中的代码元素，请打开代码元素或链接的快捷菜单。 选择 "**转向引用**"，然后选择 "代码" 元素。

## <a name="see-also"></a>另请参阅

- [映射解决方案中的依赖项](../modeling/map-dependencies-across-your-solutions.md)
- [使用代码图调试应用程序](../modeling/use-code-maps-to-debug-your-applications.md)
- [使用代码图分析查找潜在问题](../modeling/find-potential-problems-using-code-map-analyzers.md)
- [浏览和重新排列代码图](../modeling/browse-and-rearrange-code-maps.md)
- [定向图形标记语言 (DGML) 引用](../modeling/directed-graph-markup-language-dgml-reference.md)
