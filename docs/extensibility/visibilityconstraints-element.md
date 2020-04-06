---
title: 可见性约束元素 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- VisibilityConstraints
helpviewer_keywords:
- VSCT XML schema elements, VisibilityConstraints
- VisibilityConstraints element (VSCT XML schema)
ms.assetid: d6dcd314-6fe4-4693-a189-91fa026c7b34
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: b1aaa9573b883910ac6fa5d921a9bc79ce1c1cf3
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80698188"
---
# <a name="visibilityconstraints-element"></a>可见性约束元素
"可见性约束"元素确定命令组和工具栏组的静态可见性。 可见性首先由[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]集成开发环境 （IDE） 控制，无需加载 VSPackage。

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
|[可见性项目元素](../extensibility/visibilityitem-element.md)|确定命令和工具栏的静态可见性。|
|[可见性约束](../extensibility/visibilityconstraints-element.md)|确定命令组和工具栏的静态可见性。|

### <a name="parent-elements"></a>父元素

|元素|描述|
|-------------|-----------------|
|[命令表元素](../extensibility/commandtable-element.md)|定义表示 VSPackage 向 IDE 提供的命令的所有元素（例如，菜单项、菜单、工具栏和组合框）。|

## <a name="example"></a>示例

```xml
<VisibilityConstraints>
  <VisibilityItem guid="cmdSetGuidMyProductCommands"     id="cmdidAddWidget"
    context="guidNotViewSourceMode"/>
</VisibilityConstraints>
```

## <a name="see-also"></a>请参阅
- [可见性项目元素](../extensibility/visibilityitem-element.md)
- [可视化工作室命令表 （.Vsct） 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
