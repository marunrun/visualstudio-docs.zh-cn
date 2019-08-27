---
title: CustomDataSignature 元素 （Visual Studio 模板） |Microsoft Docs
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- <CustomDataSignature> Element (Visual Studio Templates)
- CustomDataSignature Element (Visual Studio Templates)
ms.assetid: 8c3db51d-7014-4484-802a-15aa1353dbdb
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: db2b4d089495245d1a37469df1dc43a19be31866
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66351980"
---
# <a name="customdatasignature-element-visual-studio-templates"></a>CustomDataSignature 元素 （Visual Studio 模板）
指定要查找的自定义数据的文本签名。

 \<VSTemplate > \<TemplateData > \<CustomDataSignature >

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
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|必需的元素。<br /><br /> 此模板分类并定义如何显示在**新的项目**或**添加新项**对话框。|

## <a name="text-value"></a>文本值
 需要一个文本值。

 文本是一个字符串，找到自定义数据所需的文本签名。

## <a name="remarks"></a>备注
 `CustomDataSignature` 是可选元素。

## <a name="see-also"></a>请参阅
- [Visual Studio 模板架构引用](../extensibility/visual-studio-template-schema-reference.md)
- [创建项目和项模板](../ide/creating-project-and-item-templates.md)