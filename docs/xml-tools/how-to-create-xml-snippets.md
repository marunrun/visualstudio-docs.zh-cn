---
title: 如何：创建 XML 代码段
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: d8556dd7-1382-4af7-ba80-3e873c9416be
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: df3c2592036f085fcf89d80bcefb1a469b3c1e15
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75592745"
---
# <a name="how-to-create-xml-snippets"></a>如何：创建 XML 片段

XML 编辑器可以用于新建 XML 代码段。 编辑器包括名为“Snippet”的 XML 代码段，是用于新建 XML 代码段的代码段样本。

## <a name="to-create-a-new-xml-snippet"></a>新建 XML 代码段

要新建 XML 代码片段，请创建一个新的 XML 文件并使用“插入代码段”功能。

1. 在“文件”菜单上单击“新建”，再单击“文件”  。

2. 单击“XML 文件”，再单击“打开” 。

3. 在编辑器窗格中右键单击并选择“插入代码段”。

4. 从列表中选择“代码段”，然后按 Enter 。

5. 对新的代码段进行所需的更改。

6. 在“文件”菜单中选择“保存 XMLFile.xml” 。

     此时出现“文件另存为”对话框。

7. 输入新的代码段的名称，然后从“保存类型”下拉窗口中选择“代码段文件” 。

8. 使用“保存位置”下拉列表将文件位置更改为 My Documents\Visual Studio 2005\Code Snippets\XML\My XML Snippets 文件夹，然后按“保存”。

## <a name="snippet-description"></a>代码段说明

本节介绍代码段样本中的一些重要元素。 有关 XML 代码片段所使用的架构元素的详细信息，请参阅[代码段架构参考](../ide/code-snippets-schema-reference.md)。

### <a name="snippettype-element"></a>SnippetType 元素

编辑器支持两种代码段类型：

```xml
<SnippetTypes>
  <SnippetType>SurroundsWith</SnippetType>
  <SnippetType>Expansion</SnippetType>
</SnippetTypes>
```

`Expansion` 类型确定在调用“插入代码段”命令时是否显示代码段。 `SurroundsWith` 类型确定在调用“环绕”命令时是否显示代码段。

### <a name="code-element"></a>代码元素

`Code` 元素定义要在调用代码段时插入的 XML 文本。

> [!NOTE]
> XML 代码段文本必须包含在 `<![CDATA[...]]>` 节中。

以下是代码段样本创建的 `Code` 元素。

```xml
<Code Language="XML">
  <![CDATA[<test>
  <name>$name$</name>
  $selected$ $end$</test>]]>
</Code>
```

`Code` 元素包括三个变量。

- $name$ 是用户定义变量。 该变量创建 `name` 元素，该元素的值可编辑，且默认值为“name”。 用户定义变量使用 `Literal` 元素定义。

- $selected$ 是预定义变量。 该变量表示在调用代码段之前在 XML 编辑器中选择的文本。 设置此变量可以确定所选文本在包围它的代码段中出现的位置。

- $end$ 是预定义变量。 用户按 Enter 完成代码片段字段的编辑后，此变量将确定移动插入符号 (^) 的目标位置。

  上面的 `Code` 元素插入以下 XML 文本：

```xml
<test>
  <name>name</name>
</test>
```

name 元素的值标记为可编辑区域。

### <a name="literal-element"></a>Literal 元素

`Literal` 元素用于标识可以在插入文件之后自定义的替换文本。 例如，文本字符串、数值和某些变量名都可以声明为 Literal 元素。 可以在 XML 代码段中定义任意数目的 Literal 元素，并且可以在代码段中多次引用。 以下是定义默认值为“name”的 $name$ 变量的 `Literal` 元素示例。

```xml
<Literal>
  <ID>name</ID>
  <Default>name</Default>
</Literal
```

Literal 元素还可以指函数。 XML 编辑器包括名为 LookupPrefix 的函数。 LookupPrefix 函数从 XML 文档中调用此代码段的位置查找给定的命名空间 URI，并返回为该命名空间定义的命名空间前缀（如果有），包括该名称中的冒号 (:)。 以下是使用 LookupPrefix 函数的 `Literal` 元素示例。

```xml
<Literal Editable="false">
   <ID>prefix</ID>
   <Function>LookupPrefix("namespaceURI")</Function>
</Literal>
```

然后，可以在 XML 代码段中的任何其他位置使用该 $prefix$ 变量。

## <a name="see-also"></a>请参阅

- [XML 代码段](../xml-tools/xml-snippets.md)
- [如何：使用 XML 代码段](../xml-tools/how-to-use-xml-snippets.md)
- [如何：从 XML 架构生成 XML 代码段](../xml-tools/how-to-generate-an-xml-snippet-from-an-xml-schema.md)
