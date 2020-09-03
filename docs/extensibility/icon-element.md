---
title: Icon 元素 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSCT XML schema elements, Icon
- Icon element (VSCT XML schema)
ms.assetid: 73c58fe3-d53c-4f4e-b025-29567c6cbb7c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: cf4f8a69e565620007fba4b9970ce96bb1513995
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80710511"
---
# <a name="icon-element"></a>Icon 元素
图标标记的 guid 属性是定义的位图的 guid。 该 `id` 属性在位图条带中选择槽。 此元素为可选元素。 如果此元素不包含在 **guidOfficeIcon： msotcidNoIcon** ，则将隐式赋值。

## <a name="syntax"></a>语法

```xml
<Icon guid="guidImages" id="bmpPic1" />
```

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|特性|说明|
|---------------|-----------------|
|guid|必需。 定义的位图的 guid。|
|id|必需。 选择位图条中的槽。|

### <a name="child-elements"></a>子元素

|元素|说明|
|-------------|-----------------|
|无。|无。|

### <a name="parent-elements"></a>父元素

|元素|说明|
|-------------|-----------------|
|[按钮元素](../extensibility/buttons-element.md)||

## <a name="see-also"></a>另请参阅
- [Visual Studio 命令表 ( .vsct) 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
