---
title: IDSymbol 元素 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- IDSymbol element (VSCT XML schema)
- VSCT XML schema elements, IDSymbol
ms.assetid: 760cfd20-3c06-422c-9103-98bfa1f387f8
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 4489be4ea24382ddaf0fcbe5e824eac3945c9cec
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66319537"
---
# <a name="idsymbol-element"></a>IDSymbol 元素
`IDSymbol`元素包含表示菜单、 组或命令的 guid: id 对中的 ID。 GUID 来自父`GuidSymbol`元素。 `IDSymbol`元素具有`name`提供的 ID，它包含在一个友好名称的属性`value`属性。

## <a name="syntax"></a>语法

```xml
<IDSymbol name=ElementName value="0x0010" />
```

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|特性|描述|
|---------------|-----------------|
|name|必需。 ID 符号名称。|
|值|必需。 ID 符号的数字 ID 值。|

### <a name="child-elements"></a>子元素
 无。

### <a name="parent-elements"></a>父元素

|元素|描述|
|-------------|-----------------|
|[GuidSymbol 元素](../extensibility/guidsymbol-element.md)|包含表示菜单、 组或命令的 guid: id 对中的 GUID。 对 `IDSymbol` 元素进行分组。|

## <a name="remarks"></a>备注
 每个`IDSymbol`元素中的给定`GuidSymbol`元素必须具有一个唯一`value`。 但是， `IDSymbol` ，只要它们具有不同的父，可以在包中存在具有相同的值的元素。

## <a name="see-also"></a>请参阅
- [Visual Studio 命令表格 (.vsct) 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)