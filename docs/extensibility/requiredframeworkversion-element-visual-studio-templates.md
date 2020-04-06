---
title: 必需框架版本元素（可视化工作室模板） |微软文档
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80701503"
---
# <a name="requiredframeworkversion-element-visual-studio-templates"></a>必需框架版本元素（可视化工作室模板）

指定模板所需的 .NET 框架的最小版本。 它会导致"**新项目**"对话框中显示 **"目标框架版本**"下拉列表。 该`RequiredFrameworkVersion`元素还确定下拉列表中可用的最低值。

> [!IMPORTANT]
> 从 Visual Studio 2017 版本 15.6 开始，**目标框架版本**下拉列表不再是 **"新项目"** 对话框"**模板**"部分中显示模板的筛选器。 相反，下拉列表充当所选模板的框架选取器。

 \<>\<模板>\<需要框架版本>

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
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|必需元素。<br /><br /> 对模板进行分类，并定义如何在 **"新项目**"或"**添加新项目**"对话框中显示模板。|

## <a name="text-value"></a>文本值
 需要一个文本值。

 文本必须是模板所需的 .NET 框架的最低版本号。

## <a name="remarks"></a>备注

`RequiredFrameworkVersion` 是可选元素。 仅当模板支持 .NET Framework 的特定最小版本（以及更高版本（如果有）时，才使用此元素。 如果指定`RequiredFrameworkVersion`元素，并且模板不支持 .NET 框架的特定最小版本，**则目标框架版本**下拉列表将在不适用时显示。

## <a name="example"></a>示例

下面的示例说明了标准[!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)]类模板的元数据。

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

在此示例中，模板（由 表示）`RequiredFrameworkVersion`所需的 .NET 框架的最小版本为 3.0。 使用此模板创建的项目可以定位 .NET 框架版本，从 3.0 开始。

## <a name="see-also"></a>请参阅

- [可视化工作室模板架构参考](../extensibility/visual-studio-template-schema-reference.md)
- [创建项目和项模板](../ide/creating-project-and-item-templates.md)
- [Framework 定位概述](../ide/visual-studio-multi-targeting-overview.md)
