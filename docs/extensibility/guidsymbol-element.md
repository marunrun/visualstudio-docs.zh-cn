---
title: 吉德符号元素 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSCT XML schema elements, GuidSymbol
- GuidSymbol element (VSCT XML schema)
ms.assetid: 11fb3545-8974-4776-9a54-6b6e7739ae31
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 59068a9ac9f952b5370681b3684ce4234354afc9
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80711130"
---
# <a name="guidsymbol-element"></a>吉德符号元素
该`GuidSymbol`元素包含表示菜单、组或命令的 GUID：ID 对的 GUID。 ID 来自元素中`IDSymbol``GuidSymbol`的元素。 元素`GuidSymbol`具有一个`name`属性，该属性为 GUID 提供友好名称，该名称包含在`value`属性中。

## <a name="syntax"></a>语法

```xml
<GuidSymbol name="guidMyCommandSet" value="{xxxxxxxxxxxxx-xxxx-xxxx-xxxxxxxxxxxx}">
  <IDSymbol>... </IDSymbol>
  <IDSymbol>... </IDSymbol>
</GuidSymbol>
```

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|特性|描述|
|---------------|-----------------|
|name|必需。 GUID 符号的名称。|
|值|必需。 GUID 符号的 GUID。|

### <a name="child-elements"></a>子元素

|元素|描述|
|-------------|-----------------|
|[IDSymbol 元素](../extensibility/idsymbol-element.md)|包含表示菜单、组或命令的 GUID：ID 对的 ID。|

### <a name="parent-elements"></a>父元素

|元素|描述|
|-------------|-----------------|
|[符号元素](../extensibility/symbols-element.md)|对`GuidSymbol` *.vsct*文件中的元素进行分组。|

## <a name="remarks"></a>备注
 通常 *，.vsct*文件`Symbols`部分包含三`GuidSymbol`个元素，一个用于包本身，一个用于命令集（包提供的菜单、组和命令的集合），另一个用于为按钮和其他可视组件提供图标的位图。 给定`IDSymbol``GuidSymbol`元素中的每个元素都必须具有唯一的`value`。但是，`IDSymbol`具有相同值的元素可以存在于包中，只要它们具有不同的父项。

## <a name="see-also"></a>请参阅
- [可视化工作室命令表 （.vsct） 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
