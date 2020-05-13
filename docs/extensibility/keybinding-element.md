---
title: 键绑定元素 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSCT XML schema elements, KeyBindings
- KeyBinding element (VSCT XML schema)
ms.assetid: e55a1098-15df-42a9-9f87-e3a99cf437dd
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: b458e70a9a85c11707c50da2e16e3aa73f51bc12
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80703147"
---
# <a name="keybinding-element"></a>键绑定元素
KeyBinding 元素指定命令的键盘快捷方式。

 命令可以同时具有与其关联的单键和双密钥绑定。 单个键绑定的示例是 **"保存**"命令的**Ctrl**+**S。** 双键绑定需要两个连续的键组合才能触发命令。 双键绑定的示例是<strong>Ctrl*+</strong>K<strong>，</strong>Ctrl<strong>+</strong>K*= 来设置书签。

## <a name="syntax"></a>语法

```
<Keybinding guid="MyGuid" id="MyId" Editor="MyEditor" key1="B" key2="x" mod1="Control" mod2="Alt" />
```

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|特性|描述|
|---------------|-----------------|
|guid|必需。|
|id|必需。|
|编辑器|必需。 编辑器 GUID 指示此键盘快捷方式将处于活动状态的编辑上下文。 全局绑定范围值为"guidVSStd97"。|
|key1|必需。 有效值包括所有可键入的字母数字，以及前面以 0x 和[VK_constants](/windows/desktop/inputdev/virtual-key-codes)开头的两位十进制值。|
|mod1|可选。 **Ctrl、Alt**和**Alt** **Shift**的任意组合由空间分隔。|
|key2|可选。 有效值包括所有可键入的字母数字，以及前面以 0x 和[VK_constants](/windows/desktop/inputdev/virtual-key-codes)开头的两位十进制值。|
|mod2|可选。 **Ctrl、Alt**和**Alt** **Shift**的任意组合由空间分隔。|
|模拟器|可选。|
|条件|可选。 请参阅[条件属性](../extensibility/vsct-xml-schema-conditional-attributes.md)。|

### <a name="child-elements"></a>子元素

|元素|描述|
|-------------|-----------------|
|Parent||
|Annotation||

### <a name="parent-elements"></a>父元素

|元素|描述|
|-------------|-----------------|
|[键绑定元素](../extensibility/keybindings-element.md)|对键绑定元素和其他键绑定分组进行分组。|

## <a name="example"></a>示例

```
<KeyBindings>
  <KeyBinding guid="guidWidgetPackage" id="cmdidUpdateWidget"
    editor="guidWidgetEditor" key1="VK_F5"/>
  <KeyBinding guid="guidWidgetPackage" id="cmdidRunWidget"
    editor="guidWidgetEditor" key1="VK_F5" mod1="Control"/>
</KeyBindings>
```

## <a name="see-also"></a>请参阅
- [键绑定元素](../extensibility/keybindings-element.md)
- [可视化工作室命令表 （.vsct） 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
