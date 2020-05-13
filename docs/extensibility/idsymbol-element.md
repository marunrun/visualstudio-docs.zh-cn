---
title: IDSymbol 元素 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- IDSymbol element (VSCT XML schema)
- VSCT XML schema elements, IDSymbol
ms.assetid: 760cfd20-3c06-422c-9103-98bfa1f387f8
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: d02a26a6874165738d917a14986d16d142c01915
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80710379"
---
# <a name="idsymbol-element"></a>IDSymbol 元素
该`IDSymbol`元素包含表示菜单、组或命令的 GUID：ID 对的 ID。 GUID 来自父`GuidSymbol`元素。 元素`IDSymbol`具有一个`name`属性，该属性为 ID 提供友好名称，该名称包含在`value`属性中。

## <a name="syntax"></a>语法

```xml
<IDSymbol name=ElementName value="0x0010" />
```

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|特性|描述|
|---------------|-----------------|
|name|必需。 ID 符号的名称。|
|值|必需。 ID 符号的数字 ID 值。|

### <a name="child-elements"></a>子元素
 无。

### <a name="parent-elements"></a>父元素

|元素|描述|
|-------------|-----------------|
|[吉德符号元素](../extensibility/guidsymbol-element.md)|包含表示菜单、组或命令的 GUID：ID 对的 GUID。 对 `IDSymbol` 元素进行分组。|

## <a name="remarks"></a>备注
 给定`IDSymbol``GuidSymbol`元素中的每个元素都必须具有唯一的`value`。 但是，`IDSymbol`具有相同值的元素可以存在于包中，只要它们具有不同的父项。

## <a name="see-also"></a>请参阅
- [可视化工作室命令表 （.vsct） 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
