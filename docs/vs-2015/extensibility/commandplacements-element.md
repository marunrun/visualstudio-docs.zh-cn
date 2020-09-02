---
title: CommandPlacements 元素 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- CommandPlacements
helpviewer_keywords:
- CommandPlacements element (VSCT XML schema)
- VSCT XML schema elements, CommandPlacements
ms.assetid: 78a5724a-3b9f-4c78-9c0d-8faa3924f81c
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: dbe65cc38bd14d859507d795ce32657f53ca8b44
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68184312"
---
# <a name="commandplacements-element"></a>CommandPlacements 元素
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

CommandPlacements 元素将 CommandPlacement 元素和其他 CommandPlacements 组分组。  
  
 CommandPlacements 元素是可选的。 如果辅助位置中必须不包含任何命令、组或菜单，则不需要在 .vsct 文件中包含此部分。  
  
## <a name="syntax"></a>语法  
  
```  
<CommandPlacements>  
  <CommandPlacement>... </CommandPlacement>  
  <CommandPlacement>... </CommandPlacement>  
</CommandPlacements>  
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
|CommandPlacements|将 CommandPlacement 元素和其他 CommandPlacements 分组分组。|  
|[CommandPlacement 元素](../extensibility/commandplacement-element.md)|启用要包含在多个组或菜单中的按钮、组和菜单。|  
  
### <a name="parent-elements"></a>父元素  
  
|元素|说明|  
|-------------|-----------------|  
|[CommandTable 元素](../extensibility/commandtable-element.md)|定义表示命令的所有元素。|  
  
## <a name="example"></a>示例  
  
```  
<CommandPlacements>  
  <CommandPlacement guid="guidWidgetPackage" id="cmdidInsertOptions"  
    priority="0x0300">  
    <Parent guid="cmdGuidWidgetCommands" id="menuIDEditWidget"/>  
  </CommandPlacement>  
</CommandPlacements>  
```  
  
## <a name="see-also"></a>另请参阅  
 [CommandPlacement 元素](../extensibility/commandplacement-element.md)   
 [Visual Studio 命令表格 (.Vsct) 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
