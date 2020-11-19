---
title: " (Visual Studio 模板) 的 ProvideDefaultName 元素 |Microsoft Docs"
description: 了解 ProvideDefaultName 元素以及它如何指定 Visual Studio 将在 "添加新项" 或 "新建项目" 对话框中生成默认的 Visual Studio 名称。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#ProvideDefaultName
helpviewer_keywords:
- ProvideDefaultName element [Visual Studio project templates]
ms.assetid: 7b0e7b20-fd6b-42e2-81d0-e5100cea0528
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 7732c6f02ae5ec086a89bd9ade5c00ea533a68f2
ms.sourcegitcommit: 86e98df462b574ade66392f8760da638fe455aa0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/19/2020
ms.locfileid: "94903801"
---
# <a name="providedefaultname-element-visual-studio-templates"></a> (Visual Studio 模板的 ProvideDefaultName 元素) 
指定 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 项目系统是否会在 " **添加新项** " 或 " **新建项目** " 对话框中生成模板的默认名称。

 \<VSTemplate> \<TemplateData>
 \<ProvideDefaultName>

## <a name="syntax"></a>语法

```xml
<ProvideDefaultName> true/false </ProvideDefaultName>
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
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|必需的元素。<br /><br /> 将此模板分类并定义此模板在 **“新建项目”** 或 **“添加新项”** 对话框中的显示方式。|

## <a name="text-value"></a>文本值
 需要一个文本值。

 文本必须是 `true` 或 `false` ，指示是否在 " **添加新项** " 或 " **新建项目** " 对话框中生成模板的默认名称。

## <a name="remarks"></a>注解
 `ProvideDefaultName` 是可选元素。 默认值为 `true`。

 如果 `ProvideDefaultName` 元素为 `false` ，则 "**添加新项**" 和 "**新建项目**" 对话框的 "**名称**" 框中将包含值 `<Enter_name>` 。

 使用 [DefaultName](../extensibility/defaultname-element-visual-studio-templates.md) 元素在 " **添加新项** " 和 " **新建项目** " 对话框中指定项目或项的默认名称。 如果元素的值 `ProvideDefaultName` 为，则 `true` 省略项目的元素时，将 `DefaultName` 用模板名称填充对话框，即 [name](../extensibility/name-element-visual-studio-templates.md) 元素中的值。

## <a name="example"></a>示例
 下面的代码示例将 `ProvideDefaultName` 元素设置为 `false` 。

```
<VSTemplate Type="Item" Version="3.0.0"
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <Name>MyClass</Name>
        <Description>My custom C# class.</Description>
        <Icon>Icon.ico</Icon>
        <ProjectType>CSharp</ProjectType>
        <ProvideDefaultName>false</ProvideDefaultName>
    </TemplateData>
    <TemplateContent>
        <ProjectItem>MyClass.cs</ProjectItem>
    </TemplateContent>
</VSTemplate>
```

## <a name="see-also"></a>请参阅
- [Visual Studio 模板架构参考](../extensibility/visual-studio-template-schema-reference.md)
- [创建项目和项模板](../ide/creating-project-and-item-templates.md)
