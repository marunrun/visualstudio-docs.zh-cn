---
title: CommandTable 元素 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- CommandTable
helpviewer_keywords:
- CommandTable element (VSCT XML schema)
- VSCT XML schema elements, CommandTable
ms.assetid: 15c38159-660a-4ef4-9643-aa6fcfca82a9
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: bb2b874f7bbe94e383e9e7fba755dcc373a93150
ms.sourcegitcommit: 374f5ec9a5fa18a6d4533fa2b797aa211f186755
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/20/2020
ms.locfileid: "77477045"
---
# <a name="commandtable-element"></a>CommandTable 元素
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

CommandTable 是 .vsct 文件的根元素。 此文件用于定义 VSPackage 提供给 IDE 的命令的实际布局和类型。 命令可能包括菜单项、菜单、工具栏和组合框。 有关详细信息，请参阅 [Visual Studio Command Table (.Vsct) Files](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)。  
  
## <a name="syntax"></a>语法  
  
```xml  
<CommandTable xmlns="http://schemas.microsoft.com/VisualStudio/2005-10-18/CommandTable" xmlns:xs="http://www.w3.org/2001/XMLSchema" >  
  <Extern>... </Extern>  
  <Include>... </Include>  
  <Define>... </Define>  
  <Commands>... </Commands>  
  <CommandPlacements>... </CommandPlacements>  
  <VisibilityConstraints>... </VisibilityConstraints>  
  <KeyBindings>... </KeyBindings>  
  <UsedCommands... </UsedCommands>  
  <Symbols>... </Symbols>  
</CommandTable>  
```  
  
## <a name="attributes-and-elements"></a>属性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>Attributes  
  
| 属性 |                                                                                                                   说明                                                                                                                   |
|-----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   xmlns   |                                   必需。 XML 命名空间：<br /><br /> `xmlns="<http://schemas.microsoft.com/VisualStudio/2005-10-18/CommandTable>"`<br /><br /> `xmlns:xs="<http://www.w3.org/2001/XMLSchema>"`                                   |
| language  | 可选。 Language 特性可用于指定命令表中 > 元素的所有 \<字符串的默认语言。  如果未指定语言，则将使用当前进程的语言：<br /><br /> language="en-us" |
  
### <a name="child-elements"></a>子元素  
  
|元素|说明|  
|-------------|-----------------|  
|[Extern 元素](../extensibility/extern-element.md)|可选。 包含编译器的预处理器指令。|  
|[ Include元素](../extensibility/include-element.md)|可选。 包含要包含在编译中的任何文件的路径。|  
|[Define 元素](../extensibility/define-element.md)|可选。 定义符号的名称和值。|  
|[Commands 元素](../extensibility/commands-element.md)|可选。 父元素，用于为包含所有其他元素的 VSPackage 定义所有命令。|  
|[CommandPlacements 元素](../extensibility/commandplacements-element.md)|可选。 定义命令栏上命令的放置位置。|  
|[VisibilityConstraints 元素](../extensibility/visibilityconstraints-element.md)|可选。 确定命令和工具栏的静态可见性。|  
|[KeyBindings 元素](../extensibility/keybindings-element.md)|可选。 为命令指定快捷键组合（如果有）。|  
|[UsedCommands 元素](../extensibility/usedcommands-element.md)|可选。 允许 VSPackage 实现其自己的功能，最初由其他 Vspackage 支持。|  
|[Symbols 元素](https://msdn.microsoft.com/f2ddd0aa-c3dd-439e-834d-28f136a27ffa)|可选。 包含编译器的任何符号数据--Guid、Id 等。|  
  
### <a name="parent-elements"></a>父元素  
  
|元素|说明|  
|-------------|-----------------|  
|无||  
  
## <a name="see-also"></a>另请参阅  
 [Visual Studio 命令表格 (.Vsct) 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
