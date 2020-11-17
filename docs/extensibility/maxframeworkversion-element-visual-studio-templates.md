---
title: " (Visual Studio 模板) 的 MaxFrameworkVersion 元素 |Microsoft Docs"
description: 了解 MaxFrameworkVersion 元素及其如何指定模板所需的最高 .NET Framework 版本。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- <MaxFrameworkVersion> Element (Visual Studio Templates)
- MaxFrameworkVersion Element (Visual Studio Templates)
ms.assetid: f732a9d3-fc29-405b-9298-01ea83fc58b8
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 44345b712f448bd7eedf288d7c58cb4193e1b020
ms.sourcegitcommit: 3d96f7a8c9affab40358c3e81e3472db31d841b2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2020
ms.locfileid: "94672420"
---
# <a name="maxframeworkversion-element-visual-studio-templates"></a> (Visual Studio 模板的 MaxFrameworkVersion 元素) 

指定模板所需的 .NET Framework 的最高版本。 它确定 "**新建项目**" 对话框的 "**目标框架版本**" 下拉列表中可用的最高值。 为了使用户能够选择框架版本，还必须指定 [RequiredFrameworkVersion](../extensibility/requiredframeworkversion-element-visual-studio-templates.md) 作为模板的最小 .NET Framework 版本。

> [!IMPORTANT]
> 从 Visual Studio 2017 版本15.6 开始，"**新项目**" 对话框的 "**模板**" 部分中的 "**目标框架版本**" 下拉列表不再是所显示模板的筛选器。 相反， **目标 Framework 版本** 下拉列表功能作为所选模板的框架选取器。

 \<VSTemplate> \<TemplateData>
 \<MaxFrameworkVersion>

## <a name="syntax"></a>语法

```xml
<MaxFrameworkVersion> ... </MaxFrameworkVersion>
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
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|必需的元素。<br /><br /> 将模板分类并定义它在 " **新建项目** " 或 " **添加新项** " 对话框中的显示方式。|

## <a name="text-value"></a>文本值
 需要一个文本值。

 文本必须是模板允许的 .NET Framework 的最高版本号。

## <a name="remarks"></a>注解

`MaxFrameworkVersion` 是可选元素。 `MaxFrameworkVersion`除非需要，否则应省略元素，以免无意中限制模板 .NET Framework 版本的支持范围。 如果 .NET Framework 不适用于模板，也应该省略此方法。

## <a name="example"></a>示例

下面的示例演示标准类模板的元数据 [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] 。

```xml
<VSTemplate Type="Item" Version="3.0.0"
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <Name>MyClass</Name>
        <Description>My custom C# class template.</Description>
        <Icon>Icon.ico</Icon>
        <ProjectType>CSharp</ProjectType>
        <RequiredFrameworkVersion>3.0</RequiredFrameworkVersion>
        <MaxFrameworkVersion>4.7.1</MaxFrameworkVersion>
        <DefaultName>MyClass</DefaultName>
    </TemplateData>
    <TemplateContent>
        <ProjectItem>MyClass.cs</ProjectItem>
    </TemplateContent>
</VSTemplate>
```

在此示例中，模板所需的 .NET Framework 的最高版本 `MaxFrameworkVersion` 为4.7.1。 使用此模板创建的项目可以将 .NET Framework 版本定位到4.7.1。

## <a name="see-also"></a>请参阅

- [Visual Studio 模板架构参考](../extensibility/visual-studio-template-schema-reference.md)
- [创建项目和项模板](../ide/creating-project-and-item-templates.md)
