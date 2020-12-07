---
title: 选项, 文本编辑器, XML, 格式设置
description: 了解如何使用 XML 部分中的“格式设置”页面来指定 XML 文档中元素和属性的格式设置方式。
ms.custom: SEO-VS-2020
ms.date: 10/29/2018
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.XML.Formatting
ms.assetid: 203e60b2-7b80-4ff4-9fa1-aa9f4374377b
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.openlocfilehash: 9aac9420d084c64a4bd5d9199f6a7ca96b8c4281
ms.sourcegitcommit: 967c2f8c1b3f805cf42c0246389517689d971b53
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/25/2020
ms.locfileid: "96040506"
---
# <a name="options-text-editor-xml-formatting"></a>选项, 文本编辑器, XML, 格式设置

使用“格式设置”选项页指定 XML 文档中元素和属性的格式设置方式。 要访问 XML 格式设置选项，请选择“工具” > “选项” > “文本编辑器” > “XML”，然后选择“格式设置”    。

## <a name="attributes"></a>特性

**保留手动属性格式化**

请不要重新设置属性的格式。 此设置为默认设置。

> [!NOTE]
> 如果这些属性位于多行上，则编辑器会缩进属性的每一行，以与父元素的缩进大小相匹配。

**对齐属性，每个属性都位于一个单独的行上**

垂直对齐第二个属性和后续属性，以便与第一个属性的缩进大小相匹配。 以下 XML 文本是如何对齐属性的示例：

```xml
<item id = "123-A"
      name = "hammer"
      price = "9.95">
</item>
```

## <a name="auto-reformat"></a>自动重新设置格式

**从剪贴板粘贴时**

重新设置从剪贴板粘贴的 XML 文本的格式。

**在完成结束标记时**

在完成结束标记时重新设置元素的格式。

## <a name="mixed-content"></a>混合内容

**默认情况下设置混合内容的格式。**

尝试重新设置混合内容的格式，在 `xml:space="preserve"` 作用域中找到该内容时除外。 此设置为默认设置。

如果某个元素同时包含文本和标记，则这些内容会被视为混合内容。 下面是包含混合内容的元素的示例：

```xml
<dir>c:\data\AlphaProject\
  <file readOnly="false">test1.txt</file>
  <file readOnly="false">test2.txt</file>
</dir>
```

## <a name="see-also"></a>请参阅

- [XML 选项 - 杂项](options-text-editor-xml-miscellaneous.md)
- [Visual Studio 中的 XML 工具](../../xml-tools/xml-tools-in-visual-studio.md)
