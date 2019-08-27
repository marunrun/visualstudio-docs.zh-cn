---
title: 代码片段架构参考
ms.date: 02/25/2019
ms.topic: reference
helpviewer_keywords:
- schema reference [Visual Studio]
- snippets [Visual Studio], schema reference
- code snippets [Visual Studio], schema reference
- IntelliSense Code Snippets, XML Schema
ms.assetid: 58a60621-725f-4763-93b7-62ea5424ef88
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e35641371ebac33c7a89426290927b6045bc4e3e
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68924082"
---
# <a name="code-snippets-schema-reference"></a>代码片段架构参考

IntelliSense 代码片段是预编写的代码段，可以随时使用 Visual Studio 将这些代码片段插入到应用程序中。 可以通过提供代码段来减少键入重复代码或搜索示例所用的时间，从而提高工作效率。 可以使用 IntelliSense 代码段 XML 架构创建自己的代码段，并将它们添加到 Visual Studio 已包含的代码段中。

## <a name="assembly-element"></a>Assembly 元素

指定代码段引用的程序集的名称。

**Assembly** 元素的文本值可以是程序集的友好文本名称（如 `System.dll`），也可以是程序集的强名称（如 `System,Version=1.0.0.1,Culture=neutral,PublicKeyToken=9b35aa323c18d4fb1`）。

```xml
<Assembly>
    AssemblyName
</Assembly>
```

|父元素|说明|
| - |-----------------|
|[Reference 元素](../ide/code-snippets-schema-reference.md#reference-element)|包含有关代码段所需的程序集引用的信息。|

需要一个文本值。 此文本指定代码段引用的程序集。

## <a name="author-element"></a>Author 元素

指定代码段作者的姓名。 **代码片段管理器**显示存储在代码片段的 `Author` 元素中的名称。

```xml
<Author>
   Code Snippet Author
</Author>
```

|父元素|说明|
| - |-----------------|
|[Header 元素](../ide/code-snippets-schema-reference.md#header-element)|包含有关代码段的常规信息。|

需要一个文本值。 此文本指定代码段的作者。

## <a name="code-element"></a>代码元素

为短代码块提供一个容器。

### <a name="keywords"></a>关键字

两个保留字可在 `Code` 元素的文本中使用：`$end$` 和 `$selected$`。 `$end$` 标记在插入代码段之后用于放置光标的位置。 `$selected$` 表示在文档中选择的要在调用时插入代码段的文本。 例如，指定一个代码段，使其包括：

```
$selected$ is a great color.
```

如果用户在调用模板时选择了“蓝色”一词，结果为：

```
Blue is a great color.
```

你不能在一个代码段中多次使用 `$end$` 或 `$selected$`。 如果要这么做，只能识别第二个实例。 指定代码段，使其包括：

```
$selected$ is a great color. I love $selected$.
```

如果选择了“蓝色”一词，结果为：

```
 is a great color. I love Blue.
```

由于 `$selected$` 和 `is` 之间存在空格，所以出现了初始空格。

所有其他 `$` 关键字将在 `<Literal>` 和 `<Object>` 标记中自动定义。

以下是 Code 元素的结构：

```xml
<Code Language="Language"
    Kind="method body/method decl/type decl/page/file/any"
    Delimiter="Delimiter">
    Code to insert
</Code>
```

需要一个文本值。 此文本指定在将此代码片段插入到代码文件中时可以使用的代码以及文本和对象。

### <a name="attributes"></a>特性

以下三种属性可用于 Code 元素：

- **语言**  -  该必选属性用于指定代码片段的语言  。 值可以是下列任一值：

   |值|说明|
   |-----|-----------|
   |`VB`|标识 Visual Basic 代码段。|
   |`CSharp`|标识 C# 代码段。|
   |`CPP`|标识 C++ 代码段。|
   |`XML`|标识 XML 代码段。|
   |`JavaScript`|标识 JavaScript 代码段。|
   |`TypeScript`|标识 TypeScript 代码片段。|
   |`SQL`|标识 SQL 代码段。|
   |`HTML`|标识 HTML 代码段。|

- **类型**  -  该可选属性用于指定代码片段包含的代码的类型，以及编译代码片段时代码片段必须插入的位置  。 值可以是下列任一值：

   |值|说明|
   |-----|-----------|
   |`method body`|指定代码段为方法体，因此必须插入到方法声明中。|
   |`method decl`|指定代码段为方法，因此必须插入到类或模块中。|
   |`type decl`|指定代码段为类型，因此必须插入到类、模块或命名空间中。|
   |`file`|指定代码段为完整的代码文件。 这些代码段可单独插入到代码文件或命名空间中。|
   |`any`|指定代码段可插入到任何位置。 此标记可用于上下文独立的代码段（例如注释）。|

- **分隔符**  -  该可选属性用于指定用于描述代码中的文本和对象的分隔符  。 默认情况下，分隔符为 `$`。

### <a name="parent-element"></a>父元素

|父元素|说明|
| - |-----------------|
|[Snippet 元素](../ide/code-snippets-schema-reference.md#snippet-element)|包含用于代码段的引用、导入、声明和代码。|

## <a name="codesnippet-element"></a>CodeSnippet 元素

允许你指定一个标题和多个 IntelliSense 代码段，你可以将其插入 Visual Studio 代码文件中。

```xml
<CodeSnippet Format="x.x.x">
    <Header>... </Header>
    <Snippet>... </Snippet>
</CodeSnippet>
```

|特性|说明|
|---------------|-----------------|
|`Format`|必需的特性。 指定代码段的架构版本。 Format 特性必须是语法为 x.x.x 的字符串，其中每个“x”表示版本号的数值。 Visual Studio 将忽略具有它不理解的 `Format` 特性的代码段。|

|子元素|说明|
|-------------------|-----------------|
|[Header 元素](../ide/code-snippets-schema-reference.md#header-element)|必需的元素。 包含有关代码段的常规信息。 代码段中必须有且仅有一个 `Header` 元素。|
|[Snippet 元素](../ide/code-snippets-schema-reference.md#snippet-element)|必需的元素。 包含将由 Visual Studio 插入的代码。 代码段中必须有且仅有一个 `Snippet` 元素。|

|父元素|说明|
| - |-----------------|
|[CodeSnippets 元素](../ide/code-snippets-schema-reference.md#codesnippets-element)|代码段 XML 架构的根元素。|

## <a name="codesnippets-element"></a>CodeSnippets 元素

对 [CodeSnippet](../ide/code-snippets-schema-reference.md#codesnippet-element) 元素进行分组。 `CodeSnippets` 元素是代码段 XML 架构的根元素。

```xml
<CodeSnippets>
    <CodeSnippet>... </CodeSnippet>
</CodeSnippets>
```

|子元素|说明|
|-------------------|-----------------|
|[CodeSnippet 元素](../ide/code-snippets-schema-reference.md#codesnippet-element)|可选元素。 所有代码段数据的父元素。 `CodeSnippet` 元素中可能有零个或零个以上的 `CodeSnippets` 元素。|

## <a name="declarations-element"></a>Declarations 元素

指定作为某个代码段组成部分的文本和对象，你可以对该代码段进行编辑。

```xml
<Declarations>
    <Literal>... </Literal>
    <Object>... </Object>
</Declarations>
```

|子元素|说明|
|-------------------|-----------------|
|[Literal 元素](../ide/code-snippets-schema-reference.md#literal-element)|可选元素。 定义你可以编辑的代码段的文本。 `Literal` 元素中可能有零个或零个以上的 `Declarations` 元素。|
|[Object 元素](../ide/code-snippets-schema-reference.md#object-element)|可选元素。 定义你可以编辑的代码段的对象。 `Object` 元素中可能有零个或零个以上的 `Declarations` 元素。|

|父元素|说明|
| - |-----------------|
|[Snippet 元素](../ide/code-snippets-schema-reference.md#snippet-element)|包含用于代码段的引用、导入、声明和代码。|

## <a name="default-element"></a>Default 元素

指定 IntelliSense 代码段的文本或对象的默认值。

```xml
<Default>
    Default value
</Default>
```

|父元素|说明|
| - |-----------------|
|[Literal 元素](../ide/code-snippets-schema-reference.md#literal-element)|定义代码段的可编辑文本字段。|
|[Object 元素](../ide/code-snippets-schema-reference.md#object-element)|定义代码段的可编辑对象字段。|

需要一个文本值。 此文本指定文本或对象的默认值，该默认值用于填充你可以编辑的代码段的字段。

## <a name="description-element"></a>Description 元素

指定有关 IntelliSense 代码段内容的说明信息。

```xml
<Description>
    Code Snippet Description
</Description>
```

|父元素|说明|
| - |-----------------|
|[Header 元素](../ide/code-snippets-schema-reference.md#header-element)|包含有关代码段的常规信息。|

需要一个文本值。 此文本描述代码段。

## <a name="function-element"></a>Function 元素

指定当 Visual Studio 中的文本或对象收到焦点时要执行的函数。

> [!NOTE]
> 仅 C# 代码片段中支持 `Function` 元素。

```xml
<Function>
    FunctionName
</Function>
```

|父元素|说明|
| - |-----------------|
|[Literal 元素](../ide/code-snippets-schema-reference.md#literal-element)|定义代码段的可编辑文本字段。|
|[Object 元素](../ide/code-snippets-schema-reference.md#object-element)|定义代码段的可编辑对象字段。|

需要一个文本值。 此文本指定当文本或对象字段在 Visual Studio 中获得焦点时要执行的函数。

## <a name="header-element"></a>Header 元素

指定有关 IntelliSense 代码段的常规信息。

```xml
<Header>
    <Title>... </Title>
    <Author>... </Author>
    <Description>... </Description>
    <HelpUrl>... </HelpUrl>
    <SnippetTypes>... </SnippetTypes>
    <Keywords>... </Keywords>
    <Shortcut>... </Shortcut>
</Header>
```

|子元素|说明|
|-------------------|-----------------|
|[Author 元素](../ide/code-snippets-schema-reference.md#author-element)|可选元素。 编写代码段的人员或公司的姓名或名称。 `Header` 元素中可能有零个或一个 `Author` 元素。|
|[Description 元素](../ide/code-snippets-schema-reference.md#description-element)|可选元素。 代码段说明。 `Header` 元素中可能有零个或一个 `Description` 元素。|
|[HelpUrl 元素](../ide/code-snippets-schema-reference.md#helpurl-element)|可选元素。 包含有关代码段的详细信息的 URL。 Header 元素中可能有零个或一个 `HelpURL` 元素。 **注意：** Visual Studio 不使用 `HelpUrl` 元素。 该元素是 IntelliSense 代码段 XML 架构的一部分，包含该元素的任何代码段将进行验证，但是从不使用该元素的值。|
|[Keywords 元素](../ide/code-snippets-schema-reference.md#keywords-element)|可选元素。 对 `Keyword` 元素进行分组。 `Header` 元素中可能有零个或一个 `Keywords` 元素。|
|[Shortcut 元素](../ide/code-snippets-schema-reference.md#shortcut-element)|可选元素。 指定可用于插入代码段的快捷方式文本。 `Header` 元素中可能有零个或一个 `Shortcut` 元素。|
|[SnippetTypes 元素](../ide/code-snippets-schema-reference.md#snippettypes-element)|可选元素。 对 `SnippetType` 元素进行分组。 `Header` 元素中可能有零个或一个 `SnippetTypes` 元素。 如果没有 `SnippetTypes` 元素，代码段将一直有效。|
|[Title 元素](../ide/code-snippets-schema-reference.md#title-element)|必需的元素。 代码段的友好名称。 `Title` 元素中必须有且仅有一个 `Header` 元素。|

|父元素|说明|
| - |-----------------|
|[CodeSnippet 元素](../ide/code-snippets-schema-reference.md#codesnippet-element)|所有代码段数据的父元素。|

## <a name="helpurl-element"></a>HelpUrl 元素

指定一个用于提供有关代码段的详细信息的 URL。

> [!NOTE]
> Visual Studio 不使用 `HelpUrl` 元素。 该元素是 IntelliSense 代码段 XML 架构的一部分，包含该元素的任何代码段将进行验证，但是从不使用该元素的值。

```xml
<HelpUrl>
    www.microsoft.com
</HelpUrl>
```

|父元素|说明|
| - |-----------------|
|[Header 元素](../ide/code-snippets-schema-reference.md#header-element)|包含有关代码段的常规信息。|

文本值是可选的。 此文本指定用于访问有关代码段的详细信息的 URL。

## <a name="id-element"></a>ID 元素

指定 `Literal` 或 `Object` 元素的唯一标识符。 相同代码段中的两个文本或对象不能在其 `ID` 元素中具有相同的文本值。 文本和对象不能包含具有末尾值的 `ID` 元素。 `$end$` 值是保留值，用于标记插入代码段后放置光标的位置。

```xml
<ID>
    Unique Identifier
</ID>
```

|父元素|说明|
| - |-----------------|
|[Literal 元素](../ide/code-snippets-schema-reference.md#literal-element)|定义代码段的可编辑文本字段。|
|[Object 元素](../ide/code-snippets-schema-reference.md#object-element)|定义代码段的可编辑对象字段。|

需要一个文本值。 此文本指定对象或文本的唯一标识符。

## <a name="import-element"></a>Import 元素

指定 IntelliSense 代码段使用的导入的命名空间。

```xml
<Import>
    <Namespace>... </Namespace>
</Import>
```

|子元素|说明|
|-------------------|-----------------|
|[Namespace 元素](../ide/code-snippets-schema-reference.md#namespace-element)|必需的元素。 指定代码段使用的命名空间。 `Namespace` 元素中必须有且仅有一个 `Import` 元素。|

|父元素|说明|
| - |-----------------|
|[Imports 元素](../ide/code-snippets-schema-reference.md#imports-element)|对 **Import** 元素进行分组。|

## <a name="imports-element"></a>Imports 元素

对单个 `Import` 元素进行分组。

```xml
<Imports>
    <Import>... </Import>
</Imports>
```

|子元素|说明|
|-------------------|-----------------|
|[Import 元素](../ide/code-snippets-schema-reference.md#import-element)|可选元素。 包含代码段的导入命名空间。 `Imports` 元素中可能有零个或零个以上的 **Import** 元素。|

|父元素|说明|
| - |-----------------|
|[Snippet 元素](../ide/code-snippets-schema-reference.md#snippet-element)|包含用于代码段的引用、导入、声明和代码。|

## <a name="keyword-element"></a>Keyword 元素

为代码段指定自定义关键字。 代码段关键字由 Visual Studio 使用，这些关键字表示联机内容提供程序添加用于搜索或分类的自定义关键字的标准方法。

```xml
<Keyword>
    Code Snippet Keyword
</Keyword>
```

|父元素|说明|
| - |-----------------|
|[Keywords 元素](../ide/code-snippets-schema-reference.md#keywords-element)|对单个 `Keyword` 元素进行分组。|

需要一个文本值。 代码段的关键字。

## <a name="keywords-element"></a>Keywords 元素

对单个 `Keyword` 元素进行分组。 代码段关键字由 Visual Studio 使用，这些关键字表示联机内容提供程序添加用于搜索或分类的自定义关键字的标准方法

```xml
<Keywords>
    <Keyword>... </Keyword>
    <Keyword>... </Keyword>
</Keywords>
```

|子元素|说明|
|-------------------|-----------------|
|[Keyword 元素](../ide/code-snippets-schema-reference.md#keyword-element)|可选元素。 包含代码段的各个关键字。 `Keyword` 元素中可能有零个或零个以上的 `Keywords` 元素。|

|父元素|说明|
| - |-----------------|
|[Header 元素](../ide/code-snippets-schema-reference.md#header-element)|包含有关代码段的常规信息。|

## <a name="literal-element"></a>Literal 元素

定义你可以编辑的代码段的文本。 `Literal` 元素用于标识整体包含在代码段中、但在插入到代码中后可能会进行自定义的代码部分的替换对象。 例如，文本字符串、数值和某些变量名应声明为文本。

文本和对象不能包含具有选定值或末尾值的 **ID** 元素。 值 `$selected$` 表示在文档中选择的要在调用时插入代码段的文本。 `$end$` 标记在插入代码段之后用于放置光标的位置。

```xml
<Literal Editable="true/false">
   <ID>... </ID>
   <ToolTip>... </ToolTip>
   <Default>... </Default>
   <Function>... </Function>
</Literal>
```

|特性|说明|
|---------------|-----------------|
|`Editable`|可选的 `Boolean` 特性。 指定在插入代码段之后是否可以编辑文本。 此特性的默认值为 `true`。|

|子元素|说明|
|-------------------|-----------------|
|[Default 元素](../ide/code-snippets-schema-reference.md#default-element)|必需的元素。 指定插入代码段时文本的默认值。 `Default` 元素中必须有且仅有一个 `Literal` 元素。|
|[Function 元素](../ide/code-snippets-schema-reference.md#function-element)|可选元素。 指定当文本在 Visual Studio 中获得焦点时要执行的函数。 `Literal` 元素中可能有零个或一个 `Function` 元素。|
|[ID 元素](../ide/code-snippets-schema-reference.md#id-element)|必需的元素。 指定文本的唯一标识符。 `ID` 元素中必须有且仅有一个 `Literal` 元素。|
|[ToolTip 元素](../ide/code-snippets-schema-reference.md#tooltip-element)|可选元素。 描述文本的预期值和用法。 `Literal` 元素中可能有零个或一个 **Tooltip** 元素。|

|父元素|说明|
| - |-----------------|
|[Declarations 元素](../ide/code-snippets-schema-reference.md#declarations-element)|包含代码段的可编辑文本和对象。|

## <a name="namespace-element"></a>Namespace 元素

指定使代码段能够正常编译和运行而必须导入的命名空间。 如果尚不存在命名空间，系统会将 `Namespace` 元素中指定的命名空间自动添加到代码起始位置处的 `using` 指令或 `Imports` 语句中。

```xml
<Namespace>
    Namespace
</Namespace>
```

|父元素|说明|
| - |-----------------|
|[Import 元素](../ide/code-snippets-schema-reference.md#import-element)|导入指定的命名空间。|

需要一个文本值。 此文本指定代码段采用的命名空间已导入。

## <a name="object-element"></a>Object 元素

定义你可以编辑的代码段的对象。 `Object` 元素用于标识代码段所需的、但可能是在代码段外部定义的项。 例如，Windows 窗体控件、ASP.NET 控件、对象实例以及类型实例应声明为对象。 对象声明要求指定类型，这一操作可通过 `Type` 元素完成。

```xml
<Object Editable="true/false">
    <ID>... </ID>
    <Type>... </Type>
    <ToolTip>... </ToolTip>
    <Default>... </Default>
    <Function>... </Function>
</Object>
```

|特性|说明|
|---------------|-----------------|
|`Editable`|可选的 `Boolean` 特性。 指定在插入代码段之后是否可以编辑文本。 此特性的默认值为 `true`。|

|子元素|说明|
|-------------------|-----------------|
|[Default 元素](../ide/code-snippets-schema-reference.md#default-element)|必需的元素。 指定插入代码段时文本的默认值。 `Default` 元素中必须有且仅有一个 `Literal` 元素。|
|[Function 元素](../ide/code-snippets-schema-reference.md#function-element)|可选元素。 指定当文本在 Visual Studio 中获得焦点时要执行的函数。 `Literal` 元素中可能有零个或一个 `Function` 元素。|
|[ID 元素](../ide/code-snippets-schema-reference.md#id-element)|必需的元素。 指定文本的唯一标识符。 `ID` 元素中必须有且仅有一个 `Literal` 元素。|
|[ToolTip 元素](../ide/code-snippets-schema-reference.md#tooltip-element)|可选元素。 描述文本的预期值和用法。 `Literal` 元素中可能有零个或一个 **Tooltip** 元素。|
|[Type 元素](../ide/code-snippets-schema-reference.md#type-element)|必需的元素。 指定对象的类型。 `Type` 元素中必须有且仅有一个 `Object` 元素。|

|父元素|说明|
| - |-----------------|
|[Declarations 元素](../ide/code-snippets-schema-reference.md#declarations-element)|包含代码段的可编辑文本和对象。|

## <a name="reference-element"></a>Reference 元素

指定有关代码段所需的程序集引用的信息。

```xml
<Reference>
    <Assembly>... </Assembly>
    <Url>... </Url>
</Reference>
```

|子元素|说明|
|-------------------|-----------------|
|[Assembly 元素](../ide/code-snippets-schema-reference.md#assembly-element)|必需的元素。 包含代码段引用的程序集的名称。 `Assembly` 元素中必须有且仅有一个 `Reference` 元素。|
|[Url 元素](../ide/code-snippets-schema-reference.md#url-element)|可选元素。 包含一个提供有关所引用程序集的详细信息的 URL。 `Reference` 元素中可能有零个或一个 `Url` 元素。|

|父元素|说明|
| - |-----------------|
|[References 元素](../ide/code-snippets-schema-reference.md#references-element)|对 `Reference` 元素进行分组。|

## <a name="references-element"></a>References 元素

对单个 `Reference` 元素进行分组。

```xml
<References>
    <Reference>... </Reference>
</References>
```

|子元素|说明|
|-------------------|-----------------|
|[Reference 元素](../ide/code-snippets-schema-reference.md#reference-element)|可选元素。 包含有关代码段的程序集引用的信息。 `Reference` 元素中可能有零个或零个以上的 `References` 元素。|

|父元素|说明|
| - |-----------------|
|[Snippet 元素](../ide/code-snippets-schema-reference.md#snippet-element)|包含用于代码段的引用、导入、声明和代码。|

## <a name="shortcut-element"></a>Shortcut 元素

指定用于插入代码段的快捷方式文本。 `Shortcut` 元素的文本值只能包含字母数字字符、连字符 (-) 和下划线 (_)。

> [!CAUTION]
> C++ 代码片段快捷方式不支持 _ 和 - 字符。

```xml
<Shortcut>
    Shortcut Text
</Shortcut>
```

|父元素|说明|
| - |-----------------|
|[Header 元素](../ide/code-snippets-schema-reference.md#header-element)|包含有关代码段的常规信息。|

文本值是可选的。 此文本可作为插入代码段的快捷方式使用。

## <a name="snippet-element"></a>Snippet 元素

指定代码段的引用、导入、声明和代码。

```xml
<Snippet>
    <References>... </References>
    <Imports>... </Imports>
    <Declarations>... </Declarations>
    <Code>... </Code>
</Snippet>
```

|子元素|说明|
|-------------------|-----------------|
|[Code 元素](../ide/code-snippets-schema-reference.md#code-element)|必需的元素。 指定要插入到文档文件中的代码。 `Code` 元素中必须有且仅有一个 `Snippet` 元素。|
|[Declarations 元素](../ide/code-snippets-schema-reference.md#declarations-element)|可选元素。 指定作为某个代码段组成部分的文本和对象，你可以对该代码段进行编辑。 `Snippet` 元素中可能有零个或一个 `Declarations` 元素。|
|[Imports 元素](../ide/code-snippets-schema-reference.md#imports-element)|可选元素。 对单个 `Import` 元素进行分组。 `Snippet` 元素中可能有零个或一个 `Imports` 元素。|
|[References 元素](../ide/code-snippets-schema-reference.md#references-element)|可选元素。 对单个 `Reference` 元素进行分组。 `Snippet` 元素中可能有零个或一个 `References` 元素。|

|父元素|说明|
| - |-----------------|
|[CodeSnippet 元素](../ide/code-snippets-schema-reference.md#codesnippet-element)|允许你指定一个标题和多个 IntelliSense 代码段，你可以将其插入 Visual Studio 代码文件中。|

## <a name="snippettype-element"></a>SnippetType 元素

指定 Visual Studio 如何插入代码段。

```xml
<SnippetType>
    SurroundsWith/Expansion
</SnippetType>
```

|父元素|说明|
| - |-----------------|
|[SnippetTypes 元素](../ide/code-snippets-schema-reference.md#snippettypes-element)|对 `SnippetType` 元素进行分组。|

此文本值必须为以下值之一：

- `SurroundsWith`：允许将代码段放置在一段选定的代码周围。

- `Expansion`：允许将代码段插入到光标处。

- `Refactoring`：指定在 C# 重构过程中使用代码片段。 不能在自定义代码段中使用 `Refactoring`。

## <a name="snippettypes-element"></a>SnippetTypes 元素

对单个 `SnippetType` 元素进行分组。 如果 `SnippetTypes` 元素不存在，则代码段可以插入到代码中的任何位置。

```xml
<SnippetTypes>
    <SnippetType>... </SnippetType>
    <SnippetType>... </SnippetType>
</SnippetTypes>
```

|子元素|说明|
|-------------------|-----------------|
|[SnippetType 元素](../ide/code-snippets-schema-reference.md#snippettype-element)|可选元素。 指定 Visual Studio 如何将代码段插入到代码中。 `SnippetType` 元素中可能有零个或零个以上的 `SnippetTypes` 元素。|

|父元素|说明|
| - |-----------------|
|[Header 元素](../ide/code-snippets-schema-reference.md#header-element)|指定有关代码段的常规信息。|

## <a name="title-element"></a>Title 元素

指定代码段的标题。 代码片段的 `Title` 元素中存储的标题显示在**代码片段选择器**中和**代码片段管理器**的代码片段说明中。

```xml
<Title>
    Code Snippet Title
</Title>
```

|父元素|说明|
| - |-----------------|
|[Header 元素](../ide/code-snippets-schema-reference.md#header-element)|指定有关代码段的常规信息。|

需要一个文本值。 此文本指定代码段的标题。

## <a name="tooltip-element"></a>ToolTip 元素

描述代码段中文本或对象的所需值和用法，Visual Studio 将代码段插入项目时将在工具提示中显示这些内容。 插入代码段后，当鼠标悬停在文本或对象上时，将显示工具提示文本。

```xml
<ToolTip>
    ToolTip description
</ToolTip>
```

|父元素|说明|
| - |-----------------|
|[Literal 元素](../ide/code-snippets-schema-reference.md#literal-element)|定义代码段的可编辑文本字段。|
|[Object 元素](../ide/code-snippets-schema-reference.md#object-element)|定义代码段的可编辑对象字段。|

需要一个文本值。 此文本指定要与代码段中的对象或文本关联的工具提示说明。

## <a name="type-element"></a>Type 元素

指定对象的类型。 `Object` 元素用于标识代码段所需的、但可能是在代码段外部定义的项。 例如，Windows 窗体控件、ASP.NET 控件、对象实例以及类型实例应声明为对象。 对象声明要求指定类型，这一操作可通过 `Type` 元素完成。

```xml
<Type>
    Type
</Type>
```

|父元素|说明|
| - |-----------------|
|[Object 元素](../ide/code-snippets-schema-reference.md#object-element)|定义代码段的可编辑对象字段。|

需要一个文本值。 此文本指定对象的类型。 例如:

```xml
<Type>System.Data.SqlClient.SqlConnection</Type>
```

## <a name="url-element"></a>Url 元素

指定一个 URL，它提供有关所引用程序集的详细信息。

> [!NOTE]
> 只有 Visual Basic 项目支持 `Url` 元素。

```xml
<Url>
    www.microsoft.com
</Url>
```

|父元素|说明|
| - |-----------------|
|[Reference 元素](../ide/code-snippets-schema-reference.md#reference-element)|指定代码段所需的程序集引用。|

需要一个文本值。 此文本指定包含有关所引用程序集的详细信息的 URL。 在无法向项目添加引用时将显示此 URL。

## <a name="see-also"></a>请参阅

- [代码片段](../ide/code-snippets.md)
- [演练：创建代码片段](../ide/walkthrough-creating-a-code-snippet.md)
