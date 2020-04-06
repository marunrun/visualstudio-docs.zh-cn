---
title: 按钮文本元素 |微软文档
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
ms.openlocfilehash: 59308feea2002a18662a7c04b95a92a920f934c4
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739905"
---
# <a name="buttontext-element"></a>按钮文本元素
此字段允许您指定出现在各种菜单中的文本。 默认情况下，该`ButtonText`元素将显示在菜单控制器中。 如果`ButtonText`其他文本字段为空，则元素也变为默认值。 即使`ButtonText`指定了其他文本字段，元素也不能为空。

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
|[Strings 元素](../extensibility/strings-element.md)|对文本元素（如`ButtonText`和`CommandName`）|

## <a name="text-value"></a>文本值
 `ButtonText`元素的文本值提供为菜单项、组合和其他具有可见文本的用户界面 （UI） 元素显示的文本。

## <a name="see-also"></a>请参阅
- [可视化工作室命令表 （.vsct） 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
