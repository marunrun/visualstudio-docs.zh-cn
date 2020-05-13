---
title: 按钮元素 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Buttons element (VSCT XML schema)
- VSCT XML schema elements, Buttons
ms.assetid: 96dccf51-2b00-4700-9d28-924b34c21ecd
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 05bd73764e96a27a92d741f144c222acc48fa518
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739939"
---
# <a name="button-element"></a>按钮元素
定义用户可以与之交互的元素。 按钮可以是不同类型的：按钮、菜单按钮和拆分下拉。

## <a name="syntax"></a>语法

```
<Button guid="guidMyCommandSet" id="MyCommand" priority="0x102" type="button">
  <Parent>... </Parent>
  <Icon>... </Icon>
  <CommandFlag>... </CommandFlag>
  <Strings>... </Strings>
</Button>
```

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|特性|描述|
|---------------|-----------------|
|guid|必需。 GUID/ID 命令标识符的 GUID。|
|id|必需。 GUID/ID 命令标识符的 ID。|
|priority|可选。 指定优先级的数值。|
|type|可选。 指定按钮类型的枚举值。<br /><br /> 如果未给出，则使用按钮。<br /><br /> Button<br /> 出现在工具栏（通常作为标志性按钮）、菜单和上下文菜单上的标准命令。<br /><br /> 菜单按钮<br /> 不执行命令但生成其他菜单的菜单项。<br /><br /> 拆分下拉<br /> 控件，如 Microsoft Word 中标准工具栏上的"撤消"和"重做"按钮。|
|条件|可选。 请参阅[条件属性](../extensibility/vsct-xml-schema-conditional-attributes.md)。|

### <a name="child-elements"></a>子元素

|元素|描述|
|-------------|-----------------|
|[父元素](../extensibility/parent-element.md)|可选。 按钮的父元素。|
|[图标元素](../extensibility/icon-element.md)|可选。 与按钮关联的图标。|
|[命令标志元素](../extensibility/command-flag-element.md)|必需。 按钮的有效命令 Flag 值如下所示。<br /><br /> - 允许帕姆斯<br /><br /> - 命令井只<br /><br /> - 默认禁用<br /><br /> - 默认不可见<br /><br /> - 唐特卡奇<br /><br /> - 动态项目启动<br /><br /> - 动态可见性<br /><br /> - 修复菜单控制器<br /><br /> - 图标和文本<br /><br /> - 无按钮定制<br /><br /> - 无定制<br /><br /> - 无键定制<br /><br /> - 无秀门控制器<br /><br /> - 皮克特<br /><br /> - 邮政执行<br /><br /> - 普罗维姆姆德<br /><br /> - 路由到文档<br /><br /> - 文本级联<br /><br /> - 文本菜单使用按钮<br /><br /> - 文本更改<br /><br /> - 文本更改按钮<br /><br /> - 文本上下文使用按钮<br /><br /> - 文本菜单Ctrluse菜单<br /><br /> - 文本菜单使用按钮<br /><br /> - 仅文本|
|[字符串元素](../extensibility/strings-element.md)|必需。 必须定义子[按钮文本元素](../extensibility/buttontext-element.md)。|
|Annotation|可选注释。|

### <a name="parent-elements"></a>父元素

|元素|描述|
|-------------|-----------------|
|[按钮元素](../extensibility/buttons-element.md)|对按钮元素进行分组。|

## <a name="example"></a>示例
 下面的示例定义 *.vsct*文件中的按钮。

 ```xml
<Button guid="guidMenuTextCmdSet" id="cmdidMyCommand" priority="0x0100" type="Button">
    <Parent guid="guidMenuTextCmdSet" id="MyMenuGroup" />
    <Icon guid="guidImages" id="bmpPic1" />
    <CommandFlag>TextChanges</CommandFlag>
    <Strings>
          <CommandName>cmdidMyCommand</CommandName>
          <ButtonText>My Command name</ButtonText>
    </Strings>
</Button>
 ```

## <a name="see-also"></a>请参阅
- [可视化工作室命令表 （.vsct） 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
