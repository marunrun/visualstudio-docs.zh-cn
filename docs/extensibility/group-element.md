---
title: Group 元素 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSCT XML schema elements, Groups
- Groups element (VSCT XML schema)
ms.assetid: 69faee18-cbf4-470a-b952-c1919c583df8
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c3c1c4bedc5ff44f797e6b46e351dc3753362501
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66342359"
---
# <a name="group-element"></a>Group 元素
定义 VSPackage 命令组。

## <a name="syntax"></a>语法

```xml
<Group guid="guidMyCommandSet" id="MyGroup" priority="0x101">
  <Parent>... </Parent>
</Group>
```

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|特性|描述|
|---------------|-----------------|
|guid|必需。 GUID ID 的命令标识符的 GUID。|
|id|必需。 GUID ID 的命令标识符的 ID。|
|priority|可选。 一个数字值，该值指定的优先级。|
|条件|可选。 请参阅[条件属性](../extensibility/vsct-xml-schema-conditional-attributes.md)。|

### <a name="child-elements"></a>子元素

|元素|描述|
|-------------|-----------------|
|父级|可选。 按钮的父元素。|
|批注|可选注释。|

### <a name="parent-elements"></a>父元素

|元素|描述|
|-------------|-----------------|
|[Groups 元素](../extensibility/groups-element.md)|包含定义 VSPackage 的命令组的条目。|

## <a name="example"></a>示例

```xml
<Group guid="cmdSetGuidWidgetCommands" id="groupIDFileEdit">
  <Parent guid="guidSHLMainMenu" id="IDM_VS_TOOL_MAINMENU"/>
</Group>
```

## <a name="see-also"></a>请参阅
- [Visual Studio 命令表格 (.vsct) 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)