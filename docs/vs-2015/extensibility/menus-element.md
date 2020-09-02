---
title: 菜单元素 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- VSCT XML schema elements, Menus
- Menus element (VSCT XML schema)
ms.assetid: d825a99b-e05c-4dd9-8933-a180216d667a
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 10e4a865774798792a386a4736058b0a5068db85
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68194242"
---
# <a name="menus-element"></a>Menus 元素
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

定义 VSPackage 实现的所有菜单和工具栏。  
  
## <a name="syntax"></a>语法  
  
```  
<Menus>  
  <Menu>... </Menu>  
  <Menu>... </Menu>  
</Menus>  
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|特性|说明|  
|---------------|-----------------|  
|条件|可选。 请参阅 [条件特性](../extensibility/vsct-xml-schema-conditional-attributes.md)。|  
  
### <a name="child-elements"></a>子元素  
  
|元素|说明|  
|-------------|-----------------|  
|[Menus 元素](../extensibility/menus-element.md)|定义 VSPackage 实现的所有菜单和工具栏。|  
|[Menu 元素](../extensibility/menu-element.md)|表示单个菜单或工具栏。|  
  
### <a name="parent-elements"></a>父元素  
  
|元素|说明|  
|-------------|-----------------|  
|[Commands 元素](../extensibility/commands-element.md)|表示 VSPackage 中命令的集合。|  
  
## <a name="example"></a>示例  
  
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
