---
title: 父元素 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- VSCT XML schema elements, Parent
- Parent element (VSCT XML schema)
ms.assetid: e4624ac8-1b9a-4940-910a-528a661cefad
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 2086473bc484fed4e8e351f0c3838074557586c9
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68194073"
---
# <a name="parent-element"></a>父元素
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

按钮或组合框的父节点可能只是一个组。 菜单或组的父节点可能是任何其他菜单或组。 在中[CommandPlacement 元素](../extensibility/commandplacement-element.md)，此元素是必需的; 所有其他实例中为可选属性。 如果省略此元素，则父级的`Group_Undefined:0`将隐式。  
  
## <a name="syntax"></a>语法  
  
```  
<Parent guid="guidMyCommandSet" id="MyParentGroupOrMenu" />  
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|特性|描述|  
|---------------|-----------------|  
|guid|必需。 GUID 的 GUID/ID 命令标识符。|  
|id|必需。 ID 的 GUID/ID 命令标识符。|  
  
### <a name="child-elements"></a>子元素  
 无  
  
### <a name="parent-elements"></a>父元素  
  
|元素|描述|  
|-------------|-----------------|  
|[CommandTable 元素](../extensibility/commandtable-element.md)|定义表示命令的 VSPackage 提供对集成的开发环境 (IDE) 的所有元素。 例如，菜单项、 菜单、 工具栏和组合框。|  
|[Buttons 元素](../extensibility/buttons-element.md)|组[Button 元素](../extensibility/button-element.md)元素。|  
|[Menus 元素](../extensibility/menus-element.md)|定义 VSPackage 实现的所有菜单。|  
|[Groups 元素](../extensibility/groups-element.md)|包含定义 VSPackage 的命令组的条目。|  
  
## <a name="see-also"></a>请参阅  
 [Visual Studio 命令表格 (.Vsct) 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
