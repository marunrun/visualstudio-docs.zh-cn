---
title: 组合元素 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Combos element (VSCT XML schema)
- VSCT XML schema elements, Combos
ms.assetid: 392e3063-f0a0-4130-9583-23bd2aa3fa36
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 9a97163f1f7dc2a1152bc22f4bc3a68ed32b3cfe
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66334911"
---
# <a name="combo-element"></a>组合元素
定义组合框中显示的命令。 有四种类型的组合框，如下所示：下拉组合、 DynamicCombo、 IndexCombo 和 MRUCombo。

## <a name="syntax"></a>语法

```xml
<combo guid="guidMyCommandSet" id="MyCommand" defaultWidth="20" idCommandList="MyCommandListID" priority="0x102" type="DropDownCombo">
  <Parent>... </Parent
  <CommandFlag>... </CommandFlag>
  <Strings>... </Strings>
</combo>
```

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|特性|描述|
|---------------|-----------------|
|guid|必需。 GUID ID 的命令标识符的 GUID。|
|id|必需。 GUID ID 的命令标识符的 ID。|
|defaultWidth|必需。 一个整数，指定组合框的像素宽度。|
|idCommandList|必需。 发送到活动命令目标来检索要在组合框中显示的项的列表 ID。 该 ID 将是与控件相同的 GUID 作用域中。|
|priority|可选。 一个数字值，该值指定的优先级。|
|类型|可选。 一个枚举的值，指定的按钮类型。<br /><br /> 如果未指定，将使用按钮。<br /><br /> DropDownCombo<br /> VSPackage 负责填写此组合框的内容。 用户不能在这个下拉列表的文本框中键入任何内容。<br /><br /> DynamicCombo<br /> VSPackage 负责填写此组合框的内容。 用户可以编辑此组合，并还在其选择项。<br /><br /> IndexCombo<br /> 相同，不同之处 DynamicCombo 引发项而不是其文本的索引。<br /><br /> MRUCombo<br /> 通过集成的开发环境 (IDE) 代表 VSPackage 来填充。  用户可以编辑此组合框中。 IDE 会记住最多每个组合框上一次 16 个条目。<br /><br /> 当用户在组合框中，选择某个控件，或输入新内容时，IDE 会通知适当的 VSPackage。|
|条件|可选。 请参阅[条件属性](../extensibility/vsct-xml-schema-conditional-attributes.md)。|

### <a name="child-elements"></a>子元素

|元素|描述|
|-------------|-----------------|
|父级|可选。 按钮的父元素。|
|CommandFlag|必需。 请参阅[Command flag 元素](../extensibility/command-flag-element.md)。 一个按钮 CommandFlag 有效值如下所示。<br /><br /> -CaseSensitive<br /><br /> -CommandWellOnly<br /><br /> -DefaultDisabled<br /><br /> -DefaultInvisible<br /><br /> -DynamicVisibility<br /><br /> -筛选键<br /><br /> - IconAndText<br /><br /> -NoAutoComplete<br /><br /> -NoButtonCustomize<br /><br /> -NoCustomize<br /><br /> -NoKeyCustomize<br /><br /> -StretchHorizontally|
|字符串|必需。 请参阅[字符串元素](../extensibility/strings-element.md)。 必须定义子 ButtonText 元素。|
|批注|可选注释。|

### <a name="parent-elements"></a>父元素

|元素|描述|
|-------------|-----------------|
|[Commands 元素](../extensibility/commands-element.md)|表示 VSPackage 工具栏上的命令的集合。|

## <a name="example"></a>示例

```xml
<Combo guid="guidWidgetPackage" id="cmdidInsertOptions"
  defaultWidth="100" idCommandList="cmdidGetInsertOptionsList">
  <CommandFlag>DynamicVisibility</CommandFlag>
  <Strings>
    <ButtonText>Select Insert Options</ButtonText>
  </Strings>
</Combo>

<Combo guid="guidWidgetPackage" id="cmdidInsertOptions"
  priority="0x0500" type="DropDownCombo" defaultWidth="100"
  idCommandList="cmdidGetInsertOptionsList">
  <Parent guid="cmdSetGuidWidgetCommands" id="groupIDFileEdit">
  <CommandFlag>DynamicVisibility</CommandFlag>
  <Strings>
    <ButtonText>Select Insert Options</ButtonText>
  </Strings>
</Combo>
```

## <a name="see-also"></a>请参阅
- [Visual Studio 命令表格 (.vsct) 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
