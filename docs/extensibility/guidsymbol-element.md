---
title: GuidSymbol 元素 |Microsoft Docs
description: GuidSymbol 元素包含表示菜单、组或命令的 GUID： ID 对的 GUID。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: 98fd802021f29365b6f338610754214352a996d7
ms.sourcegitcommit: d10f37dfdba5d826e7451260c8370fd1efa2c4e4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2020
ms.locfileid: "96994233"
---
# <a name="guidsymbol-element"></a>GuidSymbol 元素
`GuidSymbol`元素包含表示菜单、组或命令的 guid： ID 对的 guid。 ID 来自 `IDSymbol` 元素中的元素 `GuidSymbol` 。 `GuidSymbol`元素具有 `name` 特性，该特性提供了 GUID 的友好名称，该名称包含在特性中 `value` 。

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

|特性|说明|
|---------------|-----------------|
|name|必需。 GUID 符号的名称。|
|值|必需。 GUID 符号的 GUID。|

### <a name="child-elements"></a>子元素

|元素|说明|
|-------------|-----------------|
|[IDSymbol 元素](../extensibility/idsymbol-element.md)|包含表示菜单、组或命令的 GUID： ID 对的 ID。|

### <a name="parent-elements"></a>父元素

|元素|说明|
|-------------|-----------------|
|[符号元素](../extensibility/symbols-element.md)|`GuidSymbol`对 *.vsct* 文件中的元素进行分组。|

## <a name="remarks"></a>备注
 通常， *.vsct* 文件包含三个 `GuidSymbol` 元素 `Symbols` ，一个用于包本身，一个用于命令集 (包提供) 的菜单、组和命令集，另一个用于为按钮和其他可视组件提供图标的位图。 `IDSymbol`给定元素中的每个元素 `GuidSymbol` 必须具有唯一的 `value` 。但是， `IDSymbol` 具有相同值的元素可以存在于包中，只要它们具有不同的父元素。

## <a name="see-also"></a>另请参阅
- [Visual Studio 命令表 ( .vsct) 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
