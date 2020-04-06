---
title: 外部元素 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- Extern
helpviewer_keywords:
- VSCT XML schema elements, Extern
- Extern element (VSCT XML schema)
ms.assetid: db6c3ddd-a1ba-450a-897a-bb568a5377fc
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 2cf6f9db77abaa7034af8d074b9833a4c1560f07
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80711490"
---
# <a name="extern-element"></a>外部元素
Extern 元素引用任何外部标头 *（.h*） 文件，以便在编译时与 *.vsct*文件合并。 要合并的文件必须位于提供给 VSCT 编译器的"包含"路径上，或者由[Include 元素](../extensibility/include-element.md)引用。 这些文件可能是其他 *.vsct*文件或C++头文件。

 标题文件中的定义必须为"#define [符号] [值]"的形式。 定义可用于命令项的条件语句。 任何未实际使用的符号都将被丢弃。

 命令表元素外部元素

## <a name="syntax"></a>语法

```xml
<Extern href="stdidcmd.h" />
```

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|特性|描述|
|---------------|-----------------|
|href|必需。 标头文件的路径：<br /><br /> href="stdidcmd.h"|
|条件|可选。 请参阅[条件属性](../extensibility/vsct-xml-schema-conditional-attributes.md)。|
|语言|可选。 命令表中所有[\<字符串的](../extensibility/strings-element.md)默认语言>元素：<br /><br /> 语言="en-us"|

### <a name="child-elements"></a>子元素

|元素|描述|
|-------------|-----------------|
|无。|无。|

### <a name="parent-elements"></a>父元素

|元素|描述|
|-------------|-----------------|
|[命令表元素](../extensibility/commandtable-element.md)|定义表示 VSPackage 向 IDE 提供的命令的所有元素（即菜单项、菜单、工具栏和组合框）。|

## <a name="example"></a>示例

```xml
<?xml version="1.0" encoding="utf-8"?>
<CommandTable xmlns="http://schemas.microsoft.com/VisualStudio/2005-10-
  18/CommandTable" xmlns:xs="http://www.w3.org/2001/XMLSchema">
    <Extern href="C:\VSCore\vscommon\inc\vsshlids.h"/>
    ...
  <Commands package="guidMyPackage">
</CommandTable>
```

## <a name="see-also"></a>请参阅
- [可视化工作室命令表 （.vsct） 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
- [VS包如何添加用户界面元素](../extensibility/internals/how-vspackages-add-user-interface-elements.md)
- [命令、菜单和工具栏](../extensibility/internals/commands-menus-and-toolbars.md)
