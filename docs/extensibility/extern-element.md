---
title: Extern 元素 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- Extern
helpviewer_keywords:
- VSCT XML schema elements, Extern
- Extern element (VSCT XML schema)
ms.assetid: db6c3ddd-a1ba-450a-897a-bb568a5377fc
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 34e38618a153aa74bdc2449895272fc9e399c82d
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66342798"
---
# <a name="extern-element"></a>Extern 元素
Extern 元素引用外部的所有标头 ( *.h*) 要使用合并的文件 *.vsct*在编译时的文件。 要合并的文件必须位于包含路径提供给 VSCT 编译器或引用的[Include 元素](../extensibility/include-element.md)。 这些文件可能是其他 *.vsct*文件或C++标头文件。

 标头文件中的定义必须是窗体的"#define [符号] [值]"的值可能是另一个符号，如果以前已定义。 定义可用于条件语句的命令项。 实际上未使用任何符号将被放弃。

 CommandTable 元素 Extern 元素

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
|语言|可选。 默认语言的所有[\<字符串 >](../extensibility/strings-element.md)命令表中的元素：<br /><br /> language="en-us"|

### <a name="child-elements"></a>子元素

|元素|描述|
|-------------|-----------------|
|无。|无。|

### <a name="parent-elements"></a>父元素

|元素|描述|
|-------------|-----------------|
|[CommandTable 元素](../extensibility/commandtable-element.md)|定义表示命令的元素的所有 — 也就是说，菜单项、 菜单、 工具栏和组合框 — VSPackage 提供到 IDE。|

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
- [Visual Studio 命令表格 (.vsct) 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
- [Vspackage 如何添加用户界面元素](../extensibility/internals/how-vspackages-add-user-interface-elements.md)
- [命令、 菜单和工具栏](../extensibility/internals/commands-menus-and-toolbars.md)