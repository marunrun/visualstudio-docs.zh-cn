---
title: 父元素 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSCT XML schema elements, Parent
- Parent element (VSCT XML schema)
ms.assetid: e4624ac8-1b9a-4940-910a-528a661cefad
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 5f64c99f030fa436eb250531ddd5c2f11bcd2bac
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66316935"
---
# <a name="parent-element"></a>父元素
按钮或组合框的父节点可能只是一个组。 菜单或组的父节点可能是任何其他菜单或组。 在中[CommandPlacement 元素](../extensibility/commandplacement-element.md)，此元素是必需的; 所有其他实例中为可选属性。 如果省略此元素，则父级的`Group_Undefined:0`将隐式。

## <a name="syntax"></a>语法

```xml
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
 None

### <a name="parent-elements"></a>父元素

|元素|描述|
|-------------|-----------------|
|[CommandTable 元素](../extensibility/commandtable-element.md)|定义表示命令的 VSPackage 提供对集成的开发环境 (IDE) 的所有元素。 例如，菜单项、 菜单、 工具栏和组合框。|
|[Buttons 元素](../extensibility/buttons-element.md)|组[Button 元素](../extensibility/button-element.md)元素。|
|[Menus 元素](../extensibility/menus-element.md)|定义 VSPackage 实现的所有菜单。|
|[Groups 元素](../extensibility/groups-element.md)|包含定义 VSPackage 的命令组的条目。|

## <a name="see-also"></a>请参阅
- [Visual Studio 命令表格 (.vsct) 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)