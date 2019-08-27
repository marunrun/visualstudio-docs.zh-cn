---
title: 格式设置、 XML、 文本编辑器选项对话框 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-xml-tools
ms.topic: conceptual
ms.assetid: bb539b3a-027c-4b2f-906e-403e0e22ba8d
caps.latest.revision: 9
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 588bf415a801a9244cd9a046e0c503c0b238db58
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63417419"
---
# <a name="formatting-xml-text-editor-options-dialog-box"></a>格式化，XML，文本编辑器，“选项”对话框
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

使用此对话框可以指定“XML 编辑器”的格式化设置。 您可以访问**选项**对话框从**工具**菜单。  
  
> [!NOTE]
> 当您选择这些设置才可用**文本编辑器**文件夹中， **XML**文件夹，然后**格式设置**选项从**选项**对话框。  
  
## <a name="attributes"></a>特性  
 **保留手动特性格式设置**  
 属性不会重新格式化。 这是默认设置。  
  
> [!NOTE]
> 如果属性在多行上，编辑器将对每行属性进行缩进，以便与父元素的缩进匹配。  
  
 **对齐属性每个在其自己的行上**  
 使第二个以及后续的属性纵向对齐，以便与第一个属性的缩进匹配。 以下 XML 文本是如何对齐属性的示例。  
  
```  
<item id = "123-A"  
      name = "hammer"  
      price = "9.95">  
</item>  
```  
  
## <a name="auto-reformat"></a>自动重新格式化  
 **在从剪贴板粘贴时**  
 重新格式化从剪贴板粘贴的 XML 文本。  
  
 **完成结束标记时**  
 在完成结束标记时重新格式化元素。  
  
## <a name="mixed-content"></a>混合内容  
 **默认情况下保留混合的内容**  
 确定编辑器是否重新格式化混合内容。 默认情况下，编辑器尝试重新格式化混合内容，除非在 `xml:space="preserve"` 范围内找到该内容。  
  
 如果元素中包含文本和标记的混合，将认为内容是混合内容。 以下是包含混合内容的元素示例。  
  
```  
<dir>c:\data\AlphaProject\  
  <file readOnly="false">test1.txt</file>  
  <file readOnly="false">test2.txt</file>  
</dir>  
```  
  
## <a name="see-also"></a>请参阅  
 [XML 文档属性，属性窗口](../xml-tools/xml-document-properties-properties-window.md)   
 [“XML 编辑器”的组件](../xml-tools/xml-editor-components.md)
