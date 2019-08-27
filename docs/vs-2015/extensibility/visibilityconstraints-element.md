---
title: VisibilityConstraints 元素 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- VisibilityConstraints
helpviewer_keywords:
- VSCT XML schema elements, VisibilityConstraints
- VisibilityConstraints element (VSCT XML schema)
ms.assetid: d6dcd314-6fe4-4693-a189-91fa026c7b34
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 06f6a74fabfc1bd86f54656c6b30b55690940a0d
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62585121"
---
# <a name="visibilityconstraints-element"></a>VisibilityConstraints 元素
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

VisibilityConstraints 元素确定组的命令和工具栏的静态可见性。 第一次控制可见性[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]而不加载 VSPackage 的集成的开发环境 (IDE)。  
  
## <a name="syntax"></a>语法  
  
```  
<VisibilityConstraints>  
  <VisibilityConstraint>... </VisibilityConstraint>  
  <VisibilityConstraint>... </VisibilityConstraint>  
</VisibilityConstraint>  
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|特性|描述|  
|---------------|-----------------|  
|条件|可选。 请参阅[条件属性](../extensibility/vsct-xml-schema-conditional-attributes.md)。|  
  
### <a name="child-elements"></a>子元素  
  
|元素|描述|  
|-------------|-----------------|  
|[VisibilityItem 元素](../extensibility/visibilityitem-element.md)|确定命令和工具栏的静态可见性。|  
|[VisibilityConstraints](../extensibility/visibilityconstraints-element.md)|确定组的命令和工具栏的静态可见性。|  
  
### <a name="parent-elements"></a>父元素  
  
|元素|描述|  
|-------------|-----------------|  
|[CommandTable 元素](../extensibility/commandtable-element.md)|定义表示 VSPackage 提供对 IDE 的命令 （例如，菜单项、 菜单、 工具栏和组合框） 的所有元素。|  
  
## <a name="example"></a>示例  
  
```  
<VisibilityConstraints>  
  <VisibilityItem guid="cmdSetGuidMyProductCommands"     id="cmdidAddWidget"  
    context="guidNotViewSourceMode"/>  
</VisibilityConstraints>  
```  
  
## <a name="see-also"></a>请参阅  
 [VisibilityItem 元素](../extensibility/visibilityitem-element.md)   
 [Visual Studio 命令表格 (.Vsct) 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
