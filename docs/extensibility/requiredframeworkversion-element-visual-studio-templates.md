---
title: " (Visual Studio 模板) 的 RequiredFrameworkVersion 元素 |Microsoft Docs"
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- <RequiredFrameworkVersion> (Visual Studio Templates)
- RequiredFrameworkVersion (Visual Studio Templates)
ms.assetid: 08a4f609-51a5-4723-b89f-99277fb18871
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 060ebc0633de67d93257e24c2dff24d2aa0970da
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80701503"
---
# <a name="requiredframeworkversion-element-visual-studio-templates"></a> (Visual Studio 模板的 RequiredFrameworkVersion 元素) 

指定模板所需的 .NET Framework 的最低版本。 这会使 " **目标框架版本** " 下拉列表显示在 " **新建项目** " 对话框中。 `RequiredFrameworkVersion`元素还决定了下拉列表中可用的最小值。

> [!IMPORTANT]
> 从 Visual Studio 2017 版本15.6 开始，"**新项目**" 对话框的 "**模板**" 部分中的 "**目标框架版本**" 下拉列表不再是所显示模板的筛选器。 下拉列表功能作为所选模板的框架选取器。

 \<VSTemplate> \<TemplateData>
 \<RequiredFrameworkVersion>

## <a name="syntax"></a>语法

```xml
<RequiredFrameworkVersion> .... </RequiredFrameworkVersion>
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

 文本必须是模板所需的 .NET Framework 的最小版本号。

## <a name="remarks"></a>备注

`RequiredFrameworkVersion` 是可选元素。 仅在以下情况下使用此元素：如果该模板支持 .NET Framework 的任何)  (和更高版本。 如果你指定 `RequiredFrameworkVersion` 元素，而你的模板不支持 .NET Framework 的特定最低版本，则 " **目标 Framework 版本** " 下拉列表将显示 "不适用"。

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

在此示例中，模板所需的 .NET Framework 的最低版本 `RequiredFrameworkVersion` 为3.0。 使用此模板创建的项目可面向从3.0 开始 .NET Framework 版本。

## <a name="see-also"></a>请参阅

- [Visual Studio 模板架构参考](../extensibility/visual-studio-template-schema-reference.md)
- [创建项目和项模板](../ide/creating-project-and-item-templates.md)
- [框架定位概述](../ide/visual-studio-multi-targeting-overview.md)
