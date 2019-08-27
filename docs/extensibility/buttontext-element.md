---
title: ButtonText 元素 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- ButtonText element (VSCT XML schema)
- VSCT XML schema elements, ButtonText
ms.assetid: 56aba884-0356-4894-ae4e-32d3938f6865
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: fe2440258e95ad0d61998b24dae54b731a998c47
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66321218"
---
# <a name="buttontext-element"></a>ButtonText 元素
此字段允许您指定各种菜单中显示的文本。 默认情况下，`ButtonText`元素出现在菜单控制器。 `ButtonText`元素也将成为默认如果其他文本字段为空白。 `ButtonText`元素不能为空，即使指定的其他文本字段。

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

|元素|描述|
|-------------|-----------------|
|[Strings 元素](../extensibility/strings-element.md)|文本元素，如分组`ButtonText`和`CommandName`。|

## <a name="text-value"></a>文本值
 文本值`ButtonText`元素提供的菜单项、 combos 和其他用户界面 (UI) 元素包含可见文本显示的文本。

## <a name="see-also"></a>请参阅
- [Visual Studio 命令表格 (.vsct) 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)