---
title: Extern 元素 |Microsoft Docs
description: Extern 元素在编译时引用 () 文件与 .vsct 文件合并的任何外部标头。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: 7e975c3f721d65b64fc7994824406b0c9af13022
ms.sourcegitcommit: d10f37dfdba5d826e7451260c8370fd1efa2c4e4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2020
ms.locfileid: "96994519"
---
# <a name="extern-element"></a>Extern 元素
Extern 元素在编译时 *引用 ()* 文件与 *.vsct* 文件合并的任何外部标头。 要合并的文件必须位于 .VSCT 编译器提供的包含路径上，或由 [include 元素](../extensibility/include-element.md)引用。 这些文件可以是其他 *.vsct* 文件或 c + + 头文件。

 标头文件中的定义的格式必须为 "#define [符号] [值]"。值可以是其他符号（如果以前已定义）。 定义可以在命令项的条件语句中使用。 不实际使用的任何符号将被丢弃。

 CommandTable 元素 Extern 元素

## <a name="syntax"></a>语法

```xml
<Extern href="stdidcmd.h" />
```

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|特性|说明|
|---------------|-----------------|
|href|必需。 标头文件的路径：<br /><br /> href = "stdidcmd"|
|条件|可选。 请参阅 [条件特性](../extensibility/vsct-xml-schema-conditional-attributes.md)。|
|语言|可选。 [\<Strings>](../extensibility/strings-element.md)命令表中所有元素的默认语言：<br /><br /> language = "en-us"|

### <a name="child-elements"></a>子元素

|元素|说明|
|-------------|-----------------|
|无。|无。|

### <a name="parent-elements"></a>父元素

|元素|说明|
|-------------|-----------------|
|[CommandTable 元素](../extensibility/commandtable-element.md)|定义所有元素，这些元素表示 VSPackage 提供给 IDE 的命令（即菜单项、菜单、工具栏和组合框）。|

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

## <a name="see-also"></a>另请参阅
- [Visual Studio 命令表 ( .vsct) 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
- [Vspackage 如何添加用户界面元素](../extensibility/internals/how-vspackages-add-user-interface-elements.md)
- [命令、菜单和工具栏](../extensibility/internals/commands-menus-and-toolbars.md)
