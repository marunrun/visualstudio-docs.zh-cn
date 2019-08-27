---
title: Icon 元素 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSCT XML schema elements, Icon
- Icon element (VSCT XML schema)
ms.assetid: 73c58fe3-d53c-4f4e-b025-29567c6cbb7c
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: dd56391084788729c0f8439728f9afffd59da946
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66311243"
---
# <a name="icon-element"></a>Icon 元素
图标标记的 guid 属性是定义位图的 guid。 `id`属性选择槽中的位图条。 此元素为可选元素。 如果此元素不包含的值**guidOfficeIcon:msotcidNoIcon**将隐式。

## <a name="syntax"></a>语法

```xml
<Icon guid="guidImages" id="bmpPic1" />
```

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|特性|描述|
|---------------|-----------------|
|guid|必需。 定义位图的 guid。|
|id|必需。 选择槽中的位图条。|

### <a name="child-elements"></a>子元素

|元素|描述|
|-------------|-----------------|
|无。|无。|

### <a name="parent-elements"></a>父元素

|元素|描述|
|-------------|-----------------|
|[Buttons 元素](../extensibility/buttons-element.md)||

## <a name="see-also"></a>请参阅
- [Visual Studio 命令表格 (.vsct) 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)