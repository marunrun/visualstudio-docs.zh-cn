---
title: 按钮元素 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- Buttons element (VSCT XML schema)
- VSCT XML schema elements, Buttons
ms.assetid: 96dccf51-2b00-4700-9d28-924b34c21ecd
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 58f63968ed02f49b0ccfa4dda24f684fed339bc4
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68184537"
---
# <a name="button-element"></a>Button 元素
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

定义一个元素，用户可与之交互。 按钮可为不同类型：按钮、 MenuButton 和 SplitDropDown。  
  
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
|guid|必需。 GUID ID 的命令标识符的 GUID。|  
|id|必需。 GUID ID 的命令标识符的 ID。|  
|priority|可选。 一个数字值，该值指定的优先级。|  
|类型|可选。 一个枚举的值，指定的按钮类型。<br /><br /> 如果未指定，将使用按钮。<br /><br /> Button<br /> 标准命令显示在工具栏上 （通常为图标按钮），菜单和上下文菜单。<br /><br /> MenuButton<br /> 不执行命令，但会生成另一个菜单的菜单项。<br /><br /> SplitDropDown<br /> 控件，例如 Microsoft Word 中的标准工具栏上的撤消和重做按钮。|  
|条件|可选。 请参阅[条件属性](../extensibility/vsct-xml-schema-conditional-attributes.md)。|  
  
### <a name="child-elements"></a>子元素  
  
|元素|描述|  
|-------------|-----------------|  
|[Parent 元素](../extensibility/parent-element.md)|可选。 按钮的父元素。|  
|[Icon 元素](../extensibility/icon-element.md)|可选。 与按钮关联的图标。|  
|[ Command Flag元素](../extensibility/command-flag-element.md)|必需。 一个按钮 CommandFlag 有效值如下所示。<br /><br /> -AllowParams<br /><br /> -CommandWellOnly<br /><br /> -DefaultDisabled<br /><br /> -DefaultInvisible<br /><br /> -DontCache<br /><br /> -DynamicItemStart<br /><br /> -DynamicVisibility<br /><br /> -FixMenuController<br /><br /> -IconAndText<br /><br /> -NoButtonCustomize<br /><br /> -NoCustomize<br /><br /> -NoKeyCustomize<br /><br /> -NoShowOnMenuController<br /><br /> -Pict<br /><br /> -PostExec<br /><br /> -ProfferedCmd<br /><br /> - RouteToDocs<br /><br /> -TextCascadeUseBtn<br /><br /> -TextMenuUseButton<br /><br /> -TextChanges<br /><br /> -TextChangesButton<br /><br /> -TextContextUseButton<br /><br /> -TextMenuCtrlUseMenu<br /><br /> -TextMenuUseButton<br /><br /> -TextOnly|  
|[Strings 元素](../extensibility/strings-element.md)|必需。 子[ButtonText 元素](../extensibility/buttontext-element.md)必须定义。|  
|批注|可选注释。|  
  
### <a name="parent-elements"></a>父元素  
  
|元素|描述|  
|-------------|-----------------|  
|[Buttons 元素](../extensibility/buttons-element.md)|按钮元素进行分组。|  
  
## <a name="example"></a>示例  
 下面的示例在.vsct 文件中定义一个按钮。  
   
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
 [Visual Studio 命令表格 (.Vsct) 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
