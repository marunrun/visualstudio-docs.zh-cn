---
title: 预览图像元素（视觉工作室模板） |微软文档
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- <PreviewImage> Element (Visual Studio Templates)
- PreviewImage Element (Visual Studio Templates)
ms.assetid: d1796f20-523b-4e0d-8ac3-ca87f3b5a9b6
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f20cfe5f3ef35b23a52972ef1e3b7d9d4adc5a39
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80702007"
---
# <a name="previewimage-element-visual-studio-templates"></a>预览图像元素（视觉工作室模板）
为将显示在 **"新项目**"或 **"添加新项目**"对话框中的预览图像指定预览图像（作为文件名）。

 \<VStemplate \<>模板数据\<>预览图像>

## <a name="syntax"></a>语法

```
<PreviewImage>"filename"</PreviewImage>
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
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|必需元素。<br /><br /> 对模板进行分类，并定义如何在 **"新项目**"或"**添加新项目**"对话框中显示模板。|

## <a name="text-value"></a>文本值
 需要一个文本值。

 文本必须是表示文件名的字符串。

## <a name="remarks"></a>备注
 `PreviewImage` 是可选元素。

## <a name="see-also"></a>请参阅
- [可视化工作室模板架构参考](../extensibility/visual-studio-template-schema-reference.md)
- [创建项目和项模板](../ide/creating-project-and-item-templates.md)
