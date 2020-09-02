---
title: Button 元素 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80739939"
---
# <a name="button-element"></a>Button 元素
定义用户可与之交互的元素。 按钮可以是不同的类型： Button、MenuButton 和 SplitDropDown。

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

|特性|说明|
|---------------|-----------------|
|guid|必需。 GUID/ID 命令标识符的 GUID。|
|id|必需。 GUID/ID 命令标识符的 ID。|
|priority|可选。 一个指定优先级的数值。|
|type|可选。 一个枚举值，该值指定按钮的类型。<br /><br /> 如果未提供，则使用按钮。<br /><br /> Button<br /> 工具栏上出现的标准命令 (通常作为图标按钮) 、菜单和上下文菜单。<br /><br /> MenuButton<br /> 不执行命令但会生成另一个菜单的菜单项。<br /><br /> SplitDropDown<br /> 控件，如 Microsoft Word 中的 "标准" 工具栏上的 "撤消" 和 "重做" 按钮。|
|条件|可选。 请参阅 [条件特性](../extensibility/vsct-xml-schema-conditional-attributes.md)。|

### <a name="child-elements"></a>子元素

|元素|说明|
|-------------|-----------------|
|[父元素](../extensibility/parent-element.md)|可选。 按钮的父元素。|
|[Icon 元素](../extensibility/icon-element.md)|可选。 与按钮关联的图标。|
|[命令标志元素](../extensibility/command-flag-element.md)|必需。 按钮的有效 CommandFlag 值如下所示。<br /><br /> - AllowParams<br /><br /> - CommandWellOnly<br /><br /> - DefaultDisabled<br /><br /> - DefaultInvisible<br /><br /> - DontCache<br /><br /> - DynamicItemStart<br /><br /> - DynamicVisibility<br /><br /> - FixMenuController<br /><br /> - IconAndText<br /><br /> - NoButtonCustomize<br /><br /> - NoCustomize<br /><br /> - NoKeyCustomize<br /><br /> - NoShowOnMenuController<br /><br /> -Pict<br /><br /> - PostExec<br /><br /> - ProfferedCmd<br /><br /> - RouteToDocs<br /><br /> - TextCascadeUseBtn<br /><br /> - TextMenuUseButton<br /><br /> -TextChanges<br /><br /> - TextChangesButton<br /><br /> - TextContextUseButton<br /><br /> - TextMenuCtrlUseMenu<br /><br /> - TextMenuUseButton<br /><br /> -TextOnly|
|[Strings 元素](../extensibility/strings-element.md)|必需。 必须定义子 [ButtonText 元素](../extensibility/buttontext-element.md) 。|
|Annotation|可选注释。|

### <a name="parent-elements"></a>父元素

|元素|说明|
|-------------|-----------------|
|[按钮元素](../extensibility/buttons-element.md)|组按钮元素。|

## <a name="example"></a>示例
 下面的示例定义了 *.vsct* 文件中的按钮。

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
- [Visual Studio 命令表 ( .vsct) 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
