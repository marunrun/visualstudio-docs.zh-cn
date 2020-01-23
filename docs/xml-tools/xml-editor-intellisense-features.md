---
title: XML 编辑器的 IntelliSense 功能
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 2b26f214-cc3a-46bf-b260-14eb8e599182
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 609684452190bf7471f90fee75f66dbb2fcbec8e
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75592381"
---
# <a name="xml-editor-intellisense-features"></a>XML 编辑器 IntelliSense 功能

“XML 编辑器”提供了完整的智能感知功能，可与 Visual Studio 中提供的其他语言编辑器相比。 本节介绍如何使用 XML 架构定义语言 (XSD) 和 XSLT 文档中的 IntelliSense。

## <a name="intellisense-in-an-xsd-document"></a>XSD 文档中的 IntelliSense

架构与文档关联后，无论何时键入 `"<"` 或单击 "XML 编辑器" 工具栏上的 "**显示对象成员列表**" 按钮，都可以获得预期元素的下拉列表。

!["显示对象成员列表" 按钮](media/display-object-member-list-xml.png)

有关如何将架构与 XML 文档关联的信息，请参阅[xml 文档验证](../xml-tools/xml-document-validation.md)。

在开始标记中键入 SPACE 时，也可以获得一个下拉列表，显示可以添加到当前元素中的所有属性。

在键入 `"="` 代表属性值时，或键入左引号代表值时，也可以获得该属性的可能值列表。 仅当架构通过 `xsd:enumeration` 方面提供枚举值时或特性属于 `Boolean` 类型时，才会提供值。 对于 `xml:lang` 或任何从 `simpleType` 派生的 `xsd:language`，还提供已知语言代码的智能感知列表。 对于命名空间声明，会提供已知 `targetNamespace` 值的智能感知列表。

如果元素为 `">"`，在键入 `simpleType` 封闭开始标记时，也会提供可能的值的 IntelliSense 列表。 元素的行为类似于上一段中所述的特性的行为。

根据关联的架构中发现的 `xsd:annotation` 和 `xsd:documentation` 信息，还会在这些智能感知列表上显示工具提示。

## <a name="intellisense-in-an-xslt-document"></a>XSLT 文档中的 IntelliSense

将命名模板或特性添加到 XSLT 文档中之后，便可以使用 IntelliSense 插入以下内容：

- 特性集名称。

- 模板模式。

- 模板名称。

- 给定模式的参数名称。

- 给定命名模板的参数名称。

有关详细信息，请参阅[演练：使用 XSLT IntelliSense](../xml-tools/walkthrough-using-xslt-intellisense.md)主题。

## <a name="auto-completion"></a>自动完成

“XML 编辑器”还通过为您填写必需的 XML 语法，使编辑 XML 更加容易。 例如，如果你键入以下开始标记：

`<book>`

“XML 编辑器”将填写结束标记，并将光标置于开始标记之后。 下面是一个示例（"&#124;" 说明光标位置）：

`<book>`&#124;`</book>`

因为特性值必须总是加引号，“XML 编辑器”会为您填写引号。 例如，如果您键入以下内容：

`<book title=`

“XML 编辑器”会添加引号并将光标置于两个引号之间：

`<book title="`&#124;`"`

同样，“XML 编辑器”还为您自动插入以下 XML 语法：

- 结束处理指令：`?>`

- 结束 CDATA 块：`]]>`

- 结束注释：`-->`

- 结束 DTD 声明：`>`

如果从 IntelliSense 列表中选择一个命名空间限定的元素或属性，并且该元素或属性的命名空间尚不在范围内，则 "XML 编辑器" 还可以插入命名空间声明。

例如，如果从智能感知列表中选择了 `e:Book` 元素，该元素的前缀绑定到的 `http://books` 命名空间尚未在文档中声明，“XML 编辑器”将为您插入所需的命名空间声明。 以下是生成的 XML 文本：

`<e:Book xmlns:e="http://books"`

## <a name="brace-matching"></a>大括号匹配

“XML 编辑器”提供括号突出显示功能，针对您刚封闭的元素提供即时反馈。 你还可以使用键盘快捷方式（**Ctrl**+ **]** ）从一个大括号跳转到匹配的大括号。

“XML 编辑器”对下列项执行此操作：

- 匹配的开始标记和结束标记。

- 任何 "\<" 或 ">" 尖括号对。

- 注释的开始和结束。

- 处理指令的开始和结束。

- CDATA 块的开始和结束。

- DTD 声明的开始和结束。

- 特性的左引号和右引号。

## <a name="modify-the-intellisense-options"></a>修改 IntelliSense 选项

默认情况下启用智能感知和自动完成功能。 不过，您可以通过修改**工具** > **选项**"设置来更改此设置。

"**杂项**" 页的 "**自动插入**" 部分控制以下行为：

|Name|描述|
|-|-----------------|
|结束标记|为新元素插入结束标记。|
|属性引号|在输入新特性名时插入特性值引号。|
|其他标记|完成注释、CDATA、DOCTYPE、处理指令和其他标记声明。|

### <a name="to-change-the-auto-completion-behavior"></a>更改自动完成行为

1. 从“工具”菜单中选择“选项”。

2. 展开 "**文本编辑器**"，展开 " **XML**"，然后选择 "**其他**"。

3. 对 "**自动插入**" 部分进行任何更改，然后单击 **"确定"** 。

## <a name="see-also"></a>另请参阅

- [XML 编辑器](../xml-tools/xml-editor.md)
- [使用 IntelliSense](../ide/using-intellisense.md)
- [演练：使用 XSLT IntelliSense](../xml-tools/walkthrough-using-xslt-intellisense.md)
