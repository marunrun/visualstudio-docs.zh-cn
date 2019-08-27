---
title: PreviewImage 元素 （Visual Studio 模板） |Microsoft Docs
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- <PreviewImage> Element (Visual Studio Templates)
- PreviewImage Element (Visual Studio Templates)
ms.assetid: d1796f20-523b-4e0d-8ac3-ca87f3b5a9b6
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 86ed3e6f438f399547996245531c2848ac7bdb83
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66336092"
---
# <a name="previewimage-element-visual-studio-templates"></a>PreviewImage 元素 （Visual Studio 模板）
指定的预览图像，为的文件名称，将出现在任何一个的预览图像**新的项目**或**添加新项**对话框。

 \<VSTemplate> \<TemplateData> \<PreviewImage>

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
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|必需的元素。<br /><br /> 此模板分类并定义如何显示在**新的项目**或**添加新项**对话框。|

## <a name="text-value"></a>文本值
 需要一个文本值。

 文本必须是一个字符串，表示文件名称。

## <a name="remarks"></a>备注
 `PreviewImage` 是可选元素。

## <a name="see-also"></a>请参阅
- [Visual Studio 模板架构参考](../extensibility/visual-studio-template-schema-reference.md)
- [创建项目和项模板](../ide/creating-project-and-item-templates.md)