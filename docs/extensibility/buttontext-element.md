---
title: ButtonText 元素 |Microsoft Docs
description: ButtonText 元素可用于指定在各种菜单中显示的文本。 即使指定了其他文本字段，ButtonText 元素也不能为空。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- ButtonText element (VSCT XML schema)
- VSCT XML schema elements, ButtonText
ms.assetid: 56aba884-0356-4894-ae4e-32d3938f6865
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 2db20bb3298a7b849e8bc4a261987c5314a29841
ms.sourcegitcommit: 5027eb5c95e1d2da6d08d208fd6883819ef52d05
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2020
ms.locfileid: "94974463"
---
# <a name="buttontext-element"></a>ButtonText 元素
此字段允许指定在各种菜单中显示的文本。 默认情况下，该 `ButtonText` 元素显示在菜单控制器中。 `ButtonText`如果其他文本字段为空，则元素也会成为默认值。 `ButtonText`即使指定了其他文本字段，元素也不能为空。

## <a name="syntax"></a>语法

```xml
<ButtonText>My Command</ButtonText>
```

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性
 无。

### <a name="child-elements"></a>子元素
 无。

### <a name="parent-elements"></a>父元素

|元素|说明|
|-------------|-----------------|
|[Strings 元素](../extensibility/strings-element.md)|组合文本元素，例如 `ButtonText` 和 `CommandName` 。|

## <a name="text-value"></a>文本值
 元素的文本值提供了为 `ButtonText` 菜单项、combos 和其他用户界面显示的文本， (UI) 具有可见文本的元素。

## <a name="see-also"></a>请参阅
- [Visual Studio 命令表 ( .vsct) 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
