---
title: 命令元素 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- Commands
helpviewer_keywords:
- Commands element (VSCT XML schema)
- VSCT XML schema elements, Commands
ms.assetid: 47cf16a5-d78b-452e-86f6-b5893856dddf
caps.latest.revision: 18
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 194768a3b540511996e1d99e6450a7a9b24ebc74
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68184291"
---
# <a name="commands-element"></a>Commands 元素
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

表示 VSPackage 工具栏上的命令的集合。 该集合中可以具有最多五个小节中，如下所示： 菜单、 组、 按钮、 combos 和位图。  
  
 每个小节子元素，例如，\<菜单 >，唯一的命令 ID 的 GUID 和数值标识符对标识。 GUID 标识的"命令集"，用于从逻辑上相关的命令进行分组。 VSPackage 应定义其自己的命令集以避免与由其他 Vspackage 定义的命令 Id 冲突。  
  
## <a name="syntax"></a>语法  
  
```  
<Commands package="GuidMyPackage" >  
  <Menus>... </Menus>  
  <Groups>... </Groups>  
  <Buttons>... </Buttons>  
  <Combos>... </Combos>  
  <Bitmaps>... </Bitmaps>  
</Commands>  
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|特性|描述|  
|---------------|-----------------|  
|包|标识将提供的命令的 VSPackage 的 GUID。<br /><br /> 例如，包 ="guidVsPackage1Pkg"。|  
  
### <a name="child-elements"></a>子元素  
  
|元素|描述|  
|-------------|-----------------|  
|[Menus 元素](../extensibility/menus-element.md)|定义 VSPackage 实现的所有菜单。|  
|[Groups 元素](../extensibility/groups-element.md)|包含在 VSPackage 中定义的命令组的条目。|  
|[Buttons 元素](../extensibility/buttons-element.md)|按钮元素进行分组。|  
|[Bitmaps 元素](../extensibility/bitmaps-element.md)|位图元素进行分组。|  
|[Combos 元素](../extensibility/combos-element.md)|组合元素进行分组。|  
  
### <a name="parent-elements"></a>父元素  
  
|元素|描述|  
|-------------|-----------------|  
|[CommandTable 元素](../extensibility/commandtable-element.md)|定义表示的命令的 VSPackage 提供对 IDE 的所有元素。 使用的元素是菜单项、 菜单、 工具栏和组合框。|  
  
## <a name="example"></a>示例  
 下面的示例演示如何使用[Commands 元素](../extensibility/commands-element.md)。  
  
```  
<Commands package="guidMyPackage">  
    <Menus>  
      <Menu Condition="'%(DEBUG)' != 'true'"   
        guid="cmdSetGuidMyProductCommands" id="menuIDMainMenu"   
        priority="0x0000" type="Menu">  
        <Annotation>  
          <Documentation>this is an annotation</Documentation>  
          <AppInfo>  
            <CustomData>  
              <CustomSubElement>Some data</CustomSubElement>  
            </CustomData>  
          </AppInfo>  
        </Annotation>  
        <CommandFlag>AlwaysCreate</CommandFlag>  
        <Strings>  
          <ButtonText>MainMenu</ButtonText>  
        </Strings>  
      </Menu>  
  </Menus>  
<Commands>  
```  
  
## <a name="see-also"></a>请参阅  
 [Vspackage 如何添加用户界面元素](../extensibility/internals/how-vspackages-add-user-interface-elements.md)   
 [命令、菜单和工具栏](../extensibility/internals/commands-menus-and-toolbars.md)
