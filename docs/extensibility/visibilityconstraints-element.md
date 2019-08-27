---
title: VisibilityConstraints 元素 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- VisibilityConstraints
helpviewer_keywords:
- VSCT XML schema elements, VisibilityConstraints
- VisibilityConstraints element (VSCT XML schema)
ms.assetid: d6dcd314-6fe4-4693-a189-91fa026c7b34
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ee64b4b8ccebe6e63b5c558df68e0a5625b37884
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66310667"
---
# <a name="visibilityconstraints-element"></a>VisibilityConstraints 元素
VisibilityConstraints 元素确定组的命令和工具栏的静态可见性。 第一次控制可见性[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]而不加载 VSPackage 的集成的开发环境 (IDE)。

## <a name="syntax"></a>语法

```xml
<VisibilityConstraints>
  <VisibilityItem />
  <VisibilityItem />
</VisibilityConstraints>
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

```xml
<VisibilityConstraints>
  <VisibilityItem guid="cmdSetGuidMyProductCommands"     id="cmdidAddWidget"
    context="guidNotViewSourceMode"/>
</VisibilityConstraints>
```

## <a name="see-also"></a>请参阅
- [VisibilityItem 元素](../extensibility/visibilityitem-element.md)
- [Visual Studio 命令表 (。Vsct) 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
