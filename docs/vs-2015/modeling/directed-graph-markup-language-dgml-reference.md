---
title: 定向关系图标记语言（DGML）引用 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: reference
ms.assetid: cc3e4ae7-60fa-4e22-9227-98020b480b73
caps.latest.revision: 10
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: c676c57d6e6e6008611133235df8d525752f16b5
ms.sourcegitcommit: c150d0be93b6f7ccbe9625b41a437541502560f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/10/2020
ms.locfileid: "75849505"
---
# <a name="directed-graph-markup-language-dgml-reference"></a>定向图形标记语言 (DGML) 引用
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

定向图形标记语言 (DGML) 描述用于可视化和执行复杂分析的信息，并且是用于存留 Visual Studio 中的代码图的格式。 DGML 使用简单 XML 来描述循环和非循环的定向关系图。 定向关系图是一组由链接或边缘连接的节点。 可以使用节点和链接来表示网络结构，如软件项目中的元素。

 请注意，某些版本的 Visual Studio 仅支持 DGML 功能的一个子集，请参阅[体系结构和建模工具的版本支持](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)。

> [!NOTE]
> 在编辑 .dgml 文件时，IntelliSense 可帮助您标识对每个元素及其值可用的特性。 若要指定特性中的颜色，请使用常用颜色的名称，如“Blue”或 ARGB 十六进制值（如“#ffa0b1c3”）。 DGML 使用一小部分 Windows Presentation Foundation (WPF) 颜色定义格式。 有关详细信息，请参阅[Colors 类](https://msdn.microsoft.com/library/system.windows.media.colors.aspx)。

## <a name="DGML"></a>DGML 语法
 下表描述在 DGML 中使用的各种元素：

- `<DirectedGraph></DirectedGraph>`

   此元素是代码图 (.dgml) 文档的根元素。 所有其他 DGML 元素将在此元素的范围内出现。

   下面的列表描述可包含的可选特性：

   `Background`-地图背景的颜色

   `BackgroundImage`-要用作地图背景的图像文件的位置。

   `GraphDirection`-当映射设置为树布局（`Sugiyama`）时，排列节点以便大多数链接按指定方向流动： `TopToBottom`、`BottomToTop`、`LeftToRight`或 `RightToLeft`。 请参阅[更改地图布局](../modeling/browse-and-rearrange-code-maps.md#Selecting)。

   `Layout`-将 "映射" 设置为以下布局： "`None`"、"`Sugiyama`" （树布局）、"`ForceDirected`" （快速群集）或 "`DependencyMatrix`"。 请参阅[更改地图布局](../modeling/browse-and-rearrange-code-maps.md#Selecting)。

   `NeighborhoodDistance`-当映射设置为树布局或快速群集布局时，仅显示与所选节点相距指定数目（1-7）的链接。 请参阅[更改地图布局](../modeling/browse-and-rearrange-code-maps.md#Selecting)。

   示例：

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <DirectedGraph Title="DrivingTest" Background="Blue" xmlns="http://schemas.microsoft.com/vs/2009/dgml">
     <Nodes>
        ...
     </Nodes>
     <Links>
        ...
     </Links>
     <Categories>
        ...
     </Categories>
     <Properties>
        ...
     </Properties>
  </DirectedGraph>
  ```

- `<Nodes></Nodes>`

   此可选元素包含 `<Node/>` 元素的列表，这些元素可定义代码图上的节点。 有关更多信息，请参见 `<Node/>` 元素。

  > [!NOTE]
  > 在 `<Link/>` 元素中引用未定义的节点时，代码图会自动创建 `<Node/>` 元素。

   示例：

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <DirectedGraph Title="DrivingTest" xmlns="http://schemas.microsoft.com/vs/2009/dgml">
     <Nodes>
        <Node ... />
     </Nodes>
     <Links>
        <Link ... />
     </Links>
  </DirectedGraph>
  ```

- `<Node/>`

   此元素定义单个节点。 该节点将出现在 `<Nodes><Nodes/>` 元素列表内。

   此元素必须包括以下特性：

   `Id`-节点的唯一名称和 `Label` 特性的默认值（如果未指定单独的 `Label` 特性）。 此名称必须与引用它的链接的 `Source` 或 `Target` 特性匹配。

   下面的列表描述可包含的部分可选特性：

   `Label`-节点的显示名称。

   样式特性。 请参阅 [Customize code maps by editing the DGML files](../modeling/customize-code-maps-by-editing-the-dgml-files.md)。

   `Category`-标识共享此特性的元素的类别的名称。 有关更多信息，请参见 `<Category/>` 元素。

   `Property`-属性的名称，该属性标识具有相同属性值的元素。 有关更多信息，请参见 `<Property/>` 元素。

   `Group` - 如果节点包含其他节点，请将此特性设置为 `Expanded` 或 `Collapsed` 以显示或隐藏其内容。 必须有一个 `<Link/>` 元素，此元素包含 `Category="Contains"` 特性并将父节点指定为源节点，而将子节点指定为目标节点。 请参阅对[代码元素分组](../modeling/customize-code-maps-by-editing-the-dgml-files.md#OrganizeNodes)。

   `Visibility`-将此特性设置为 `Visible`、`Hidden`或 `Collapsed`。 使用 `System.Windows.Visibility`。 请参阅[隐藏或显示节点和链接](../modeling/browse-and-rearrange-code-maps.md#HidingShowing)。

   `Reference` - 将此特性设置为链接到文档或 URL。 请参阅[将文档或 Url 链接到代码元素和链接](../modeling/customize-code-maps-by-editing-the-dgml-files.md#AddReferences)。

   示例：

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <DirectedGraph Title="DrivingTest" xmlns="http://schemas.microsoft.com/vs/2009/dgml">
     <Nodes>
        <Node Id="Driver" Label="Student" Category="Person" />
        <Node Id="Passenger" Label="Instructor" Category="Person" />
        <Node Id="Car" Label="Car" Category="Automobile" />
        <Node Id="Truck" Label="Truck" Category="Automobile" />
     </Nodes>
     <Links>
        <Link ... />
     </Links>
     <Categories>
        <Category Id="Person" Background="Orange" />
        <Category Id="Automobile" Background="Yellow"/>
     </Categories>
  </DirectedGraph>
  ```

- `<Links></Links>`

   此元素包含 `<Link>` 元素的列表，这些元素可定义两个节点之间的链接。 有关更多信息，请参见 `<Link/>` 元素。

   示例：

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <DirectedGraph Title="DrivingTest" xmlns="http://schemas.microsoft.com/vs/2009/dgml">
     <Links>
        <Link ... />
     </Links>
  </DirectedGraph>
  ```

- `<Link/>`

   此元素定义一个用于将源节点连接到目标节点的链接。 该节点将出现在 `<Links></Links>` 元素列表内。

  > [!NOTE]
  > 如果此元素引用未定义的节点，则代码图文档将自动创建具有指定特性（如果有）的节点。

   此元素必须包括以下特性：

   `Source`-链接的源节点

   `Target` - 链接的目标节点

   下面的列表描述可包含的部分可选特性：

   `Label`-链接的显示名称

   样式特性。 请参阅 [Customize code maps by editing the DGML files](../modeling/customize-code-maps-by-editing-the-dgml-files.md)。

   `Category`-标识共享此特性的元素的类别的名称。 有关更多信息，请参见 `<Category/>` 元素。

   `Property`-属性的名称，该属性标识具有相同属性值的元素。 有关更多信息，请参见 `<Property/>` 元素。

   示例：

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <DirectedGraph Title="DrivingTest" xmlns="http://schemas.microsoft.com/vs/2009/dgml">
     <Nodes>
        <Node Id="Driver" Label="Student" Category="Person" />
        <Node Id="Passenger" Label="Instructor" Category="Person" />
        <Node Id="Car" Label="Car" Category="Automobile" />
        <Node Id="Truck" Label="Truck" Category="Automobile" />
     </Nodes>
     <Links>
        <Category Id="Person" Background="Orange" />
        <Category Id="Automobile" Background="Yellow"/>
        <Link Source="Driver" Target="Car" Label="Passed" Stroke="Black" Background="Green" Category="PassedTest" />
        <Link Source="Driver" Target="Truck" Label="Failed" Stroke="Black" Background="Red" Category="PassedTest" />
     </Links>
  </DirectedGraph>
  ```

- `<Categories></Categories>`

   此元素包含 `<Category/>` 元素的列表。 有关更多信息，请参见 `<Category/>` 元素。

   示例：

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <DirectedGraph Title="DrivingTest" xmlns="http://schemas.microsoft.com/vs/2009/dgml">
     <Categories>
         <Category ... />
     </Categories>
  </DirectedGraph>
  ```

- `<Category/>`

   此元素定义 `Category` 特性，此特性用于标识共享此特性的元素。 `Category` 特性可用于组织代码图元素，通过继承提供共享特性或定义其他元数据。

   此元素必须包括以下特性：

   `Id` - 类别的唯一名称和 `Label` 特性的默认值（如果未指定单独的 `Label` 特性）。

   下面的列表描述可包含的部分可选特性：

   `Label` - 类别的读者友好名称。

   `BasedOn`-当前元素的 `<Category/>` 从中继承的父类别。

   在此元素的示例中，`FailedTest` 类别从 `Stroke` 类别继承其 `PassedTest` 特性。 请参阅[通过编辑 DGML 文件自定义代码图](../modeling/customize-code-maps-by-editing-the-dgml-files.md)中的 "创建分层类别"。

   类别还提供一些基本模板行为，这些行为用于控制节点和链接在代码图上显示的外观。 请参阅 [Customize code maps by editing the DGML files](../modeling/customize-code-maps-by-editing-the-dgml-files.md)。

   示例：

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <DirectedGraph Title="DrivingTest" xmlns="http://schemas.microsoft.com/vs/2009/dgml">
     <Nodes>
        <Node Id="Driver" Label="Driver" Category="Person" />
        <Node Id="Car" Label="Car" Category="Automobile" />
        <Node Id="Truck" Label="Truck" Category="Automobile" />
        <Node Id="Passenger" Category="Person" />
     </Nodes>
     <Links>
        <Link Source="Driver" Target="Car" Label="Passed" Category="PassedTest" />
        <Link Source="Driver" Target="Truck" Label="Failed" Category="FailedTest" />
     </Links>
     <Categories>
        <Category Id="Person" Background="Orange" />
        <Category Id="Automobile" Background="Yellow"/>
        <Category Id="PassedTest" Label="Passed" Stroke="Black" Background="Green" />
        <Category Id="FailedTest" Label="Failed" BasedOn="PassedTest" Background="Red" />
     </Categories>
  </DirectedGraph>
  ```

- `<Properties></Properties>`

   此元素包含 `<Property/>` 元素的列表。 有关更多信息，请参见 `<Property/>` 元素。

   示例：

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <DirectedGraph Title="DrivingTest" xmlns="http://schemas.microsoft.com/vs/2009/dgml">
     <Properties>
         <Property ... />
     </Properties>
  </DirectedGraph>
  ```

- `<Property/>`

   此元素定义 `Property` 特性，此特性可用于将值分配给任何 DGML 元素或特性（包括类别和其他属性）。

   此元素必须包括以下特性：

  - `Id`-属性的唯一名称和 `Label` 特性的默认值（如果未指定单独的 `Label` 特性）。

  - `DataType`-属性存储的数据的类型

    如果要在 "**属性**" 窗口中显示该属性，请使用 `Label` 属性指定该属性的显示名称。

    请参阅向[代码元素和链接分配类别](../modeling/customize-code-maps-by-editing-the-dgml-files.md#AssignCategories)。

    示例：

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <DirectedGraph Title="DrivingTest" xmlns="http://schemas.microsoft.com/vs/2009/dgml">
     <Nodes>
        <Node Id="Driver" Label="Driver" Category="Person" DrivingAge="18"/>
        <Node Id="Car" Label="Car" Category="Automobile" />
        <Node Id="Truck" Label="Truck" Category="Automobile" />
        <Node Id="Passenger" Category="Person" />
     </Nodes>
     <Links>
        <Link Source="Driver" Target="Car" Label="Passed" Category="PassedTest" />
        <Link Source="Driver" Target="Truck" Label="Failed" Category="FailedTest" />
     </Links>
     <Categories>
        <Category Id="Person" Background="Orange" />
        <Category Id="Automobile" Background="Yellow"/>
        <Category Id="PassedTest" Label="Passed" Stroke="Black" Background="Green" />
        <Category Id="FailedTest" Label="Failed" BasedOn="PassedTest" Background="Red" />
     </Categories>
     <Properties>
         <Property Id="DrivingAge" Label="Driving Age" DataType="System.Int32" />
     </Properties>
  </DirectedGraph>
  ```

### <a name="AddAlias"></a>常用路径的别名
 将常用路径替换为别名有助于减小 .dgml 文件的大小和加载或保存该文件所需的时间。 若要创建别名，请在 .dgml 文件的结尾处添加 `<Paths></Paths>` 部分。 在此部分添加 `<Path/>` 元素以定义路径的别名：

```xml
<Paths>
   <Path Id="MyPathAlias" Value="C:\...\..." />
</Paths>
```

 若要从 .dgml 文件中的某个元素引用别名，请用美元符号（$）和括号（（））将 \<Path/> 元素的 `Id` 括起来：

```xml
<Nodes>
   <Node Id="MyNode" Reference="$(MyPathAlias)MyDocument.txt" />
</Nodes>
<Properties>
   <Property Id="Reference" Label="My Document" DataType="System.String" IsReference="True" />
</Properties>
```

## <a name="see-also"></a>请参阅
 [映射解决方案中的依赖项](../modeling/map-dependencies-across-your-solutions.md)[使用代码图调试应用程序](../modeling/use-code-maps-to-debug-your-applications.md)[使用代码图分析器查找潜在问题](../modeling/find-potential-problems-using-code-map-analyzers.md)
