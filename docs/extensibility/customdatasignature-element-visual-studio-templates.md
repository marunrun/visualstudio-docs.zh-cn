---
title: 自定义数据签名元素（可视化工作室模板） |微软文档
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- <CustomDataSignature> Element (Visual Studio Templates)
- CustomDataSignature Element (Visual Studio Templates)
ms.assetid: 8c3db51d-7014-4484-802a-15aa1353dbdb
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ec8bae34da0f007bac65f26c4e442c1d03e56d08
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739440"
---
# <a name="customdatasignature-element-visual-studio-templates"></a>自定义数据签名元素（可视化工作室模板）
指定文本签名以查找自定义数据。

 \<模板>\<模板数据>\<自定义数据签名>

## <a name="syntax"></a>语法

```
<CustomDataSignature>"string"</CustomDataSignature>
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

 文本是具有查找自定义数据所需的文本签名的字符串。

## <a name="remarks"></a>备注
 `CustomDataSignature` 是可选元素。

## <a name="see-also"></a>请参阅
- [可视化工作室模板架构参考](../extensibility/visual-studio-template-schema-reference.md)
- [创建项目和项模板](../ide/creating-project-and-item-templates.md)
