---
title: 格式设置，XML，文本编辑器，"选项" 对话框 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-xml-tools
ms.topic: conceptual
ms.assetid: bb539b3a-027c-4b2f-906e-403e0e22ba8d
caps.latest.revision: 9
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 962321a1ab1a1ca5332300eea0d21781a9e4bbf5
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72670973"
---
# <a name="formatting-xml-text-editor-options-dialog-box"></a>格式化，XML，文本编辑器，“选项”对话框
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

使用此对话框可以指定“XML 编辑器”的格式化设置。 可以从 "**工具**" 菜单访问 "**选项**" 对话框。

> [!NOTE]
> 选择 "**文本编辑器**" 文件夹、" **XML** " 文件夹，然后选择 "**选项**" 对话框中的 "**格式**设置" 选项时，可以使用这些设置。

## <a name="attributes"></a>特性
 **保留手动属性格式化**属性不会重新格式化。 这是默认设置。

> [!NOTE]
> 如果属性在多行上，编辑器将对每行属性进行缩进，以便与父元素的缩进匹配。

 **每个属性在各自的行上对齐**垂直对齐第二个属性和后续属性以匹配第一个属性的缩进。 以下 XML 文本是如何对齐属性的示例。

```
<item id = "123-A"
      name = "hammer"
      price = "9.95">
</item>
```

## <a name="auto-reformat"></a>自动重新格式化
 **从剪贴板粘贴时**重新格式化从剪贴板粘贴的 XML 文本。

 **结束标记完成时**完成结束标记时重新格式化元素。

## <a name="mixed-content"></a>混合内容
 **默认情况下保留混合内容**确定编辑器是否重新格式化混合内容。 默认情况下，编辑器尝试重新格式化混合内容，除非在 `xml:space="preserve"` 范围内找到该内容。

 如果元素中包含文本和标记的混合，将认为内容是混合内容。 以下是包含混合内容的元素示例。

```
<dir>c:\data\AlphaProject\
  <file readOnly="false">test1.txt</file>
  <file readOnly="false">test2.txt</file>
</dir>
```

## <a name="see-also"></a>请参阅
 [Xml 文档属性，"属性" 窗口](../xml-tools/xml-document-properties-properties-window.md) [XML 编辑器组件](../xml-tools/xml-editor-components.md)
