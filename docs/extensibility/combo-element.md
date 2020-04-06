---
title: 组合元素 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Combos element (VSCT XML schema)
- VSCT XML schema elements, Combos
ms.assetid: 392e3063-f0a0-4130-9583-23bd2aa3fa36
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 18ff9d9e20ec221a86f1cce5f9c43a4e47ed6dc2
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739817"
---
# <a name="combo-element"></a>组合元素
定义显示在组合框中的命令。 组合框有四种，如下所示：下拉康博、动态康波、指数康博和MRUCombo。

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
|guid|必需。 GUID/ID 命令标识符的 GUID。|
|id|必需。 GUID/ID 命令标识符的 ID。|
|默认宽度|必需。 指定组合框像素宽度的整数。|
|id命令列表|必需。 发送到活动命令目标的 ID，用于检索要在组合框中显示的项目列表。 ID 将与控件位于相同的 GUID 作用域中。|
|priority|可选。 指定优先级的数值。|
|type|可选。 指定按钮类型的枚举值。<br /><br /> 如果未给出，则使用按钮。<br /><br /> 下拉康博<br /> VS包装负责填写此组合框的内容。 用户无法在此下拉列表的文本框中键入任何内容。<br /><br /> 动态通信<br /> VS包装负责填写此组合框的内容。 用户可以编辑此组合，也可以选择其中的项目。<br /><br /> 索引孔博<br /> 与 DynamicCombo 相同，只不过它提高了项的索引，而不是其文本。<br /><br /> MRUCombo<br /> 由代表 VSPackage 的集成开发环境 （IDE） 填充。  用户可以在此组合框中进行编辑。 IDE 最多记住每个组合框的最后 16 个条目。<br /><br /> 当用户在组合框中选择某些内容或输入新内容时，IDE 会通知相应的 VSPackage。|
|条件|可选。 请参阅[条件属性](../extensibility/vsct-xml-schema-conditional-attributes.md)。|

### <a name="child-elements"></a>子元素

|元素|描述|
|-------------|-----------------|
|Parent|可选。 按钮的父元素。|
|命令标志|必需。 请参阅[命令标志元素](../extensibility/command-flag-element.md)。 按钮的有效命令 Flag 值如下所示。<br /><br /> - 区分大小写<br /><br /> - 命令井只<br /><br /> - 默认禁用<br /><br /> - 默认不可见<br /><br /> - 动态可见性<br /><br /> - 过滤器键<br /><br /> - 图标和文本<br /><br /> - 无自动完成<br /><br /> - 无按钮定制<br /><br /> - 无定制<br /><br /> - 无键定制<br /><br /> - 横向拉伸|
|字符串|必需。 请参阅[字符串元素](../extensibility/strings-element.md)。 必须定义子按钮文本元素。|
|Annotation|可选注释。|

### <a name="parent-elements"></a>父元素

|元素|描述|
|-------------|-----------------|
|[命令元素](../extensibility/commands-element.md)|表示 VSPackage 工具栏上的命令集合。|

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
- [可视化工作室命令表 （.vsct） 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
