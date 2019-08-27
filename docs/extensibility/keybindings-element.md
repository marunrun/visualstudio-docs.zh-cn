---
title: KeyBindings 元素 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- KeyBindings
helpviewer_keywords:
- VSCT XML schema elements, KeyBindings
- KeyBindings element (VSCT XML schema)
ms.assetid: 26a15d5c-ddea-4977-af7f-d795ff09c7ad
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: d970497dd8f80d66bdbdac8809103582104a2636
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66352582"
---
# <a name="keybindings-element"></a>KeyBindings 元素
键绑定元素进行分组键绑定元素和其他键绑定分组。

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

|特性|描述|
|---------------|-----------------|
|条件|可选。 请参阅[条件属性](../extensibility/vsct-xml-schema-conditional-attributes.md)。|

### <a name="child-elements"></a>子元素

|元素|描述|
|-------------|-----------------|
|[KeyBinding 元素](../extensibility/keybinding-element.md)|指定的命令的键盘快捷方式。|
|[KeyBindings](../extensibility/keybindings-element.md)|键绑定元素进行分组和其他键绑定分组。|

### <a name="parent-elements"></a>父元素

|元素|描述|
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

## <a name="see-also"></a>请参阅
- [KeyBinding 元素](../extensibility/keybinding-element.md)
- [Visual Studio 命令表格 (.vsct) 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)