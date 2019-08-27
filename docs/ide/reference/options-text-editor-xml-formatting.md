---
title: 选项, 文本编辑器, XML, 格式设置
ms.date: 10/29/2018
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.XML.Formatting
ms.assetid: 203e60b2-7b80-4ff4-9fa1-aa9f4374377b
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: e20b2f7ebe351aa050ea66468fb33aba8e4a31bc
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62969262"
---
# <a name="options-text-editor-xml-formatting"></a>选项, 文本编辑器, XML, 格式设置

使用“格式设置”选项页指定 XML 文档中元素和属性的格式设置方式。 要访问 XML 格式设置选项，请选择“工具” > “选项” > “文本编辑器” > “XML”，然后选择“格式设置”。

## <a name="attributes"></a>特性

**保留手动特性格式设置**

请勿重新设置特性的格式。 此设置为默认设置。

> [!NOTE]
> 如果属性在多行上，编辑器将对每行属性进行缩进，以便与父元素的缩进匹配。

**在单独的行上对齐每个特性**

使第二个以及后续的特性纵向对齐，以便与第一个特性的缩进匹配。 以下 XML 文本是如何对齐属性的示例：

```xml
<item id = "123-A"
      name = "hammer"
      price = "9.95">
</item>
```

## <a name="auto-reformat"></a>自动重新格式化

**从剪贴板粘贴时**

重新设置从剪贴板粘贴的 XML 文本的格式。

**完成结束标记时**

在完成结束标记时重新设置元素的格式。

## <a name="mixed-content"></a>混合内容

**默认设置混合内容的格式。**

将尝试重新设置混合内容的格式，除非在 `xml:space="preserve"` 范围内找到该内容。 此设置为默认设置。

如果元素中包含文本和标记的混合，将认为内容是混合内容。 以下是包含混合内容的元素示例。

```xml
<dir>c:\data\AlphaProject\
  <file readOnly="false">test1.txt</file>
  <file readOnly="false">test2.txt</file>
</dir>
```

## <a name="see-also"></a>请参阅

- [XML 选项 - 杂项](options-text-editor-xml-miscellaneous.md)
- [Visual Studio 中的 XML 工具](../../xml-tools/xml-tools-in-visual-studio.md)