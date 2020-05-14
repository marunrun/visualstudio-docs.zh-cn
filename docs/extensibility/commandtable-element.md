---
title: 命令表元素 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- CommandTable
helpviewer_keywords:
- CommandTable element (VSCT XML schema)
- VSCT XML schema elements, CommandTable
ms.assetid: 15c38159-660a-4ef4-9643-aa6fcfca82a9
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a362763d34335b9a18c4114a7c35b23f0efee020
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739643"
---
# <a name="commandtable-element"></a>命令表元素
命令表是 *.vsct*文件的根元素。 这是定义 VS 包向 IDE 提供的命令的实际布局和类型的文件。 命令可能包括菜单项、菜单、工具栏和组合框。 有关详细信息，请参阅[可视化工作室命令表 （.vsct） 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)。

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

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

| 特性 | 描述 |
|-----------| - |
| xmlns | 必需。 XML 命名空间：<br /><br /> `xmlns=http://schemas.microsoft.com/VisualStudio/2005-10-18/CommandTable`<br /><br /> xmlns：xs="<http://www.w3.org/2001/XMLSchema> |
| 语言 | 可选。 语言属性可用于指定命令表中所有\<字符串>元素的默认语言。  如果未指定该语言，将使用当前进程的语言：<br /><br /> 语言="en-us" |

### <a name="child-elements"></a>子元素

|元素|描述|
|-------------|-----------------|
|[外部元素](../extensibility/extern-element.md)|可选。 包含编译器的预处理器指令。|
|[包括元素](../extensibility/include-element.md)|可选。 包含要包含在编译中的任何文件的路径。|
|[定义元素](../extensibility/define-element.md)|可选。 定义给定其名称和值的符号。|
|[命令元素](../extensibility/commands-element.md)|可选。 定义包含所有其他元素的 VSPackage 的所有命令的父元素。|
|[命令放置元素](../extensibility/commandplacements-element.md)|可选。 定义命令栏上要放置命令的位置。|
|[可见性约束元素](../extensibility/visibilityconstraints-element.md)|可选。 确定命令和工具栏的静态可见性。|
|[键绑定元素](../extensibility/keybindings-element.md)|可选。 指定命令的快捷键组合（如果有）。|
|[已用命令元素](../extensibility/usedcommands-element.md)|可选。 允许 VSPackage 可以选择实现其最初由其他 VSPackage 支持的功能版本。|
|[符号元素](https://www.microsoft.com/download/details.aspx?id=55984)|可选。 包含编译器的任何符号数据（GUID、DOd 等）。|

### <a name="parent-elements"></a>父元素

|元素|说明|
|-------------|-----------------|
|无||

## <a name="see-also"></a>请参阅
- [可视化工作室命令表 （.vsct） 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
