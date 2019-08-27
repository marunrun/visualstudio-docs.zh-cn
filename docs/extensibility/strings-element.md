---
title: 字符串元素 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Strings element (VSCT XML schema)
- VSCT XML schema elements, Strings
ms.assetid: 23a42074-a689-481d-824f-b43aa448f266
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 277cd2b8e40dfbfd1e222975f41bd4ac95c70c62
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66331722"
---
# <a name="strings-element"></a>Strings 元素
字符串元素必须包含至少一个**ButtonText**子元素。 所有其他子元素是可选的。 无效的 XML 字符如 & 和 < 必须编码为实体 ('&amp;和&lt;，等等)。

 And 符的文本字符串中指定该命令的键盘快捷方式。

## <a name="syntax"></a>语法

```
<Strings>
  <ButtonText>... </ButtonText>
  <CommandName>... </CommandName>
</Strings>
```

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|特性|描述|
|---------------|-----------------|
|语言|可选。 语言 ="。"。|

### <a name="child-elements"></a>子元素

|元素|描述|
|-------------|-----------------|
|ButtonText|此字段和五个命令定义中的以下文本字段可以指定各种菜单中显示的文本。 默认情况下，`ButtonText`字段显示在菜单控制器中。 `ButtonText`字段也将成为默认如果其他文本字段为空白。 `ButtonText`字段不能为空，即使指定的其他文本字段。|
|ToolTipText|`ToolTipText`字段指定菜单项的工具提示中显示的文本。<br /><br /> 如果`ToolTipText`字段为空，`ButtonText`使用字段。|
|MenuText|`MenuText`字段指定是否在主菜单中，工具栏上，在快捷菜单中，或在子菜单命令显示的文本。 如果`MenuText`字段为空白，集成的开发环境 (IDE) 使用`ButtonText`字段。 `MenuText`字段还用于本地化。<br /><br /> 对于快捷菜单，`MenuText`字段是在快捷菜单工具栏中，允许自定义的快捷菜单在 IDE 中显示的名称。 因此，为特定命名快捷方式菜单; 中例如，使用而不是"快捷方式"的"小组件的包快捷方式菜单"。<br /><br /> 如果`MenuText`未指定字段，`ButtonText`使用字段。|
|CommandName|`CommandName`字段指定的键盘类别中显示的文本**命令**选项卡中**自定义**对话框 (可通过单击**自定义**上**工具**菜单)。|
|CanonicalName|英语`CanonicalName`字段可以在中输入的英语文本中指定的命令名称**命令**窗口来执行的菜单项。 在 IDE 中剥离出字母、 数字、 下划线或嵌入的句点不是任何字符。 然后将此文本串联成`ButtonText`字段来定义该命令。 例如，**新的项目**上**文件**菜单变得 File.NewProject 命令。<br /><br /> 如果英语`CanonicalName`未指定字段、 IDE 使用`ButtonText`字段中，并带出所有除字母、 数字、 下划线和嵌入的句点。 例如，按钮文本"和定义命令..."将成为的 DefineCommands，其中删除与号、 空间和省略号。<br /><br /> 如果`TextChanges`指定标志且该命令的文本已更改，可识别的相应命令**命令**窗口不会更改; 它将保持原始的规范格式`ButtonText`或英语`CanonicalName`字段。|
|LocCanonicalName|`LocCanonicalName`字段为英语的行为相同`CanonicalName`字段，但可以指定的已本地化的命令文本。 可以指定这两个规范的字段。 因为 IDE 只分析中输入文本**命令**窗口并将关联使用英语和非英语文本命令时，它可以与相同的命令相关联。|

### <a name="parent-elements"></a>父元素

|元素|描述|
|-------------|-----------------|
|[Button 元素](../extensibility/button-element.md)|定义一个元素，用户可与之交互。|
|[Menu 元素](../extensibility/menu-element.md)|定义一个菜单项。|
|[Combo 元素](../extensibility/combo-element.md)|定义组合框中显示的命令。|

## <a name="see-also"></a>请参阅
- [Visual Studio 命令表格 (.Vsct) 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)