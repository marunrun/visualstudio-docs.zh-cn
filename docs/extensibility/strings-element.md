---
title: 字符串元素 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Strings element (VSCT XML schema)
- VSCT XML schema elements, Strings
ms.assetid: 23a42074-a689-481d-824f-b43aa448f266
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: db44db8926b523665a21c00b710dcee55749ab89
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80699723"
---
# <a name="strings-element"></a>Strings 元素
字符串元素必须至少包含一个**ButtonText**子元素。 所有其他子元素都是可选的。 无效的 XML 字符（如"&"和"<"）必须编码为&amp;实体（''和''&lt;等）。

 文本字符串中的 ampersand 指定命令的键盘快捷方式。

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
|语言|可选。 语言="|

### <a name="child-elements"></a>子元素

|元素|描述|
|-------------|-----------------|
|按钮文本|此字段和命令定义中的以下五个文本字段允许您指定出现在各种菜单中的文本。 默认情况下，该`ButtonText`字段将显示在菜单控制器中。 如果`ButtonText`其他文本字段为空，则该字段也将成为默认值。 即使`ButtonText`指定了其他文本字段，该字段也不能为空。|
|工具提示文本|该`ToolTipText`字段指定菜单项的工具提示中显示的文本。<br /><br /> 如果`ToolTipText`该字段为空，则`ButtonText`使用该字段。|
|菜单文本|如果`MenuText`命令位于主菜单、工具栏、快捷菜单或子菜单中，则该字段指定为命令显示的文本。 如果`MenuText`字段为空，则集成开发环境 （IDE） 使用`ButtonText`该字段。 该`MenuText`字段还可用于本地化。<br /><br /> 对于快捷菜单，该`MenuText`字段是"快捷菜单"工具栏中显示的名称，该工具栏允许自定义 IDE 中的快捷菜单。 因此，在快捷菜单的名称中具体说明;例如，使用"小工具包快捷菜单"而不是"快捷方式"。<br /><br /> 如果未指定`MenuText`该字段，则使用该`ButtonText`字段。|
|命令名称|该`CommandName`字段指定"**自定义"** 对话框中 **"命令"** 选项卡中键盘类别中显示的文本（可通过单击"**工具**"菜单上的 **"自定义**"来提供）。|
|CanonicalName|英语`CanonicalName`字段在英语文本中指定命令的名称，该命令可以在 **"命令"** 窗口中输入以执行菜单项。 IDE 会剥离不是字母、数字、下划线或嵌入句点的任何字符。 然后，将此文本串联到字段以`ButtonText`定义命令。 例如，"**文件**"菜单上**的"新项目**"将成为命令 File.NewProject。<br /><br /> 如果未指定英语`CanonicalName`字段，IDE 将使用该`ButtonText`字段，并剥离除字母、数字、下划线和嵌入句点之外的所有句点。 例如，按钮文本"&定义命令..."变为 DefineCommands，其中删除安培、空格和椭圆。<br /><br /> 如果指定`TextChanges`了标志并更改了命令的文本，**则命令**窗口识别的相应命令不会更改;如果指定了该标志，并且更改了命令窗口的文本。"它仍然是原始`ButtonText`或英语`CanonicalName`字段的规范形式。|
|Loccanonon 名称|字段`LocCanonicalName`与英语`CanonicalName`字段行为相同，但允许指定本地化的命令文本。 可以指定两个规范字段。 由于 IDE 只是分析在**命令**窗口中输入的文本并将其与命令相关联，因此英语和非英语文本都可以与同一命令相关联。|

### <a name="parent-elements"></a>父元素

|元素|描述|
|-------------|-----------------|
|[Button 元素](../extensibility/button-element.md)|定义用户可以与之交互的元素。|
|[Menu 元素](../extensibility/menu-element.md)|定义单个菜单项。|
|[Combo 元素](../extensibility/combo-element.md)|定义显示在组合框中的命令。|

## <a name="see-also"></a>请参阅
- [Visual Studio 命令表格 (.Vsct) 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
