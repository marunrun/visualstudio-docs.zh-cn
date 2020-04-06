---
title: 父元素 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSCT XML schema elements, Parent
- Parent element (VSCT XML schema)
ms.assetid: e4624ac8-1b9a-4940-910a-528a661cefad
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 8c018505ba06762bf8426f266b24ee1835313c29
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80702217"
---
# <a name="parent-element"></a>父元素
按钮或组合框的父项可能只有组。 菜单或组的父项可以是任何其他菜单或组。 在[命令放置元素中](../extensibility/commandplacement-element.md)，需要此元素;在所有其他实例中，它是可选的。 如果省略此元素，则表示的`Group_Undefined:0`父元素。

## <a name="syntax"></a>语法

```xml
<Parent guid="guidMyCommandSet" id="MyParentGroupOrMenu" />
```

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|特性|描述|
|---------------|-----------------|
|guid|必需。 GUID/ID 命令标识符的 GUID。|
|id|必需。 GUID/ID 命令标识符的 ID。|

### <a name="child-elements"></a>子元素
 无

### <a name="parent-elements"></a>父元素

|元素|描述|
|-------------|-----------------|
|[命令表元素](../extensibility/commandtable-element.md)|定义表示 VS 包向集成开发环境 （IDE） 提供的命令的所有元素。 例如，菜单项、菜单、工具栏和组合框。|
|[按钮元素](../extensibility/buttons-element.md)|对[按钮元素](../extensibility/button-element.md)进行分组。|
|[菜单元素](../extensibility/menus-element.md)|定义 VSPackage 实现的所有菜单。|
|[组元素](../extensibility/groups-element.md)|包含定义 VSPackage 的命令组的条目。|

## <a name="see-also"></a>请参阅
- [可视化工作室命令表 （.vsct） 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
