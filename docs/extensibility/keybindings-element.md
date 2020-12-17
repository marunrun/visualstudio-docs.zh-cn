---
title: 键绑定元素 |Microsoft Docs
description: 键绑定元素将键绑定元素和其他键绑定组分组。 本文包含一个示例。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- KeyBindings
helpviewer_keywords:
- VSCT XML schema elements, KeyBindings
- KeyBindings element (VSCT XML schema)
ms.assetid: 26a15d5c-ddea-4977-af7f-d795ff09c7ad
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 928637d8103a69eafd3bda4446a55bb7523f83a8
ms.sourcegitcommit: d485b18e46ec4cf08704b5a8d0657bc716ec8393
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/17/2020
ms.locfileid: "97616086"
---
# <a name="keybindings-element"></a>键绑定元素
键绑定元素将键绑定元素和其他键绑定组分组。

## <a name="syntax"></a>语法

```xml
<KeyBindings>
  <KeyBinding>... </KeyBinding>
  <KeyBinding>... </KeyBinding>
</KeyBindings>
```

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|特性|说明|
|---------------|-----------------|
|条件|可选。 请参阅 [条件特性](../extensibility/vsct-xml-schema-conditional-attributes.md)。|

### <a name="child-elements"></a>子元素

|元素|说明|
|-------------|-----------------|
|[键绑定元素](../extensibility/keybinding-element.md)|指定命令的键盘快捷方式。|
|[键绑定](../extensibility/keybindings-element.md)|将键绑定元素和其他键绑定分组分组。|

### <a name="parent-elements"></a>父元素

|元素|说明|
|-------------|-----------------|
|[CommandTable 元素](../extensibility/commandtable-element.md)|定义表示命令的所有元素。|

## <a name="example"></a>示例

```xml
<KeyBindings>
  <KeyBinding guid="guidWidgetPackage" id="cmdidUpdateWidget"
    editor="guidWidgetEditor" key1="VK_F5"/>
  <KeyBinding guid="guidWidgetPackage" id="cmdidRunWidget"
    editor="guidWidgetEditor" key1="VK_F5" mod1="Control"/>
</KeyBindings>
```

## <a name="see-also"></a>另请参阅
- [键绑定元素](../extensibility/keybinding-element.md)
- [Visual Studio 命令表 ( .vsct) 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
