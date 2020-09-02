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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68184291"
---
# <a name="commands-element"></a>Commands 元素
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

表示 VSPackage 工具栏上命令的集合。 集合最多可以包含五个子节，如下所示：菜单、组、按钮、combos 和位图。  
  
 每个子元素（例如）由 \<Menu> 唯一的命令 ID 标识，该 ID 是一个 GUID 和数字标识符对。 GUID 标识 "命令集"，用于对逻辑上相关的命令进行分组。 VSPackage 应定义自己的命令集，以避免与其他 Vspackage 定义的命令 Id 发生冲突。  
  
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
  
|特性|说明|  
|---------------|-----------------|  
|包|标识提供命令的 VSPackage 的 GUID。<br /><br /> 例如，package = "guidVsPackage1Pkg"。|  
  
### <a name="child-elements"></a>子元素  
  
|元素|说明|  
|-------------|-----------------|  
|[Menus 元素](../extensibility/menus-element.md)|定义 VSPackage 实现的所有菜单。|  
|[Groups 元素](../extensibility/groups-element.md)|包含在 VSPackage 中定义命令组的项。|  
|[Buttons 元素](../extensibility/buttons-element.md)|组按钮元素。|  
|[Bitmaps 元素](../extensibility/bitmaps-element.md)|组位图元素。|  
|[Combos 元素](../extensibility/combos-element.md)|组组合元素。|  
  
### <a name="parent-elements"></a>父元素  
  
|元素|说明|  
|-------------|-----------------|  
|[CommandTable 元素](../extensibility/commandtable-element.md)|定义所有元素，这些元素表示 VSPackage 为 IDE 提供的命令。 可能的元素包括菜单项、菜单、工具栏和组合框。|  
  
## <a name="example"></a>示例  
 下面的示例演示如何使用 [命令元素](../extensibility/commands-element.md)。  
  
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
  
## <a name="see-also"></a>另请参阅  
 [Vspackage 如何添加用户界面元素](../extensibility/internals/how-vspackages-add-user-interface-elements.md)   
 [命令、菜单和工具栏](../extensibility/internals/commands-menus-and-toolbars.md)
