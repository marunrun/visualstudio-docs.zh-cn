---
title: 最大框架版本元素（可视化工作室模板） |微软文档
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
ms.openlocfilehash: 9c3acf9c40499417fe180ce470224824cc89a113
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80702621"
---
# <a name="maxframeworkversion-element-visual-studio-templates"></a>最大框架版本元素（可视化工作室模板）

指定模板所需的 .NET 框架的最大版本。 它确定 **"新项目****"对话框的目标框架版本**下拉列表中可用的最高值。 为了使用户能够选择框架版本，还必须将["必需框架版本"](../extensibility/requiredframeworkversion-element-visual-studio-templates.md)指定为模板的最低 .NET 框架版本。

> [!IMPORTANT]
> 从 Visual Studio 2017 版本 15.6 开始，**目标框架版本**下拉列表不再是 **"新项目"** 对话框"**模板**"部分中显示模板的筛选器。 相反，**目标框架版本**下拉列表功能为所选模板的框架选取器。

 \<模板>\<模板数据>\<最大框架版本>

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
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|必需元素。<br /><br /> 对模板进行分类，并定义如何在 **"新项目**"或"**添加新项目**"对话框中显示模板。|

## <a name="text-value"></a>文本值
 需要一个文本值。

 文本必须是模板允许的 .NET 框架的最高版本号。

## <a name="remarks"></a>备注

`MaxFrameworkVersion` 是可选元素。 除非`MaxFrameworkVersion`需要，否则应省略该元素，以免无意中限制模板支持的 .NET Framework 版本范围。 如果 .NET 框架不适用于模板，也应省略它。

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

在此示例中，模板（由 表示）`MaxFrameworkVersion`所需的 .NET 框架的最大版本为 4.7.1。 使用此模板创建的项目可以定位 .NET 框架版本，最多 4.7.1。

## <a name="see-also"></a>请参阅

- [可视化工作室模板架构参考](../extensibility/visual-studio-template-schema-reference.md)
- [创建项目和项模板](../ide/creating-project-and-item-templates.md)
