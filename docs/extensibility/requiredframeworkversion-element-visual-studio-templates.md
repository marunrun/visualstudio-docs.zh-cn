---
title: RequiredFrameworkVersion 元素 （Visual Studio 模板） |Microsoft Docs
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- <RequiredFrameworkVersion> (Visual Studio Templates)
- RequiredFrameworkVersion (Visual Studio Templates)
ms.assetid: 08a4f609-51a5-4723-b89f-99277fb18871
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 0550fc1d286c04c61a1c0b2503326a002fde729e
ms.sourcegitcommit: 12f2851c8c9bd36a6ab00bf90a020c620b364076
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/06/2019
ms.locfileid: "66744754"
---
# <a name="requiredframeworkversion-element-visual-studio-templates"></a>RequiredFrameworkVersion 元素 （Visual Studio 模板）

指定模板所需的.NET framework 的最低版本。 它会导致**目标框架版本**下拉列表中显示**新项目**对话框。 `RequiredFrameworkVersion`元素还确定可用的下拉列表中的最小值。

> [!IMPORTANT]
> 在 Visual Studio 2017 版本 15.6 版中，启动**目标框架版本**下拉列表中不再是中的显示模板的筛选器**模板**一部分**新项目**对话框。 相反，在下拉列表中的函数作为所选模板的 framework 选取器。

 \<VSTemplate> \<TemplateData> \<RequiredFrameworkVersion>

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
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|必需的元素。<br /><br /> 此模板分类并定义如何显示在**新的项目**或**添加新项**对话框。|

## <a name="text-value"></a>文本值
 需要一个文本值。

 文本必须为.NET Framework 所需的模板的最低版本号。

## <a name="remarks"></a>备注

`RequiredFrameworkVersion` 是可选元素。 模板支持特定的最低版本 （和更高版本，如果有），才使用此元素的.NET framework。 如果指定`RequiredFrameworkVersion`元素和模板不支持特定的最小版本的.NET Framework**目标框架版本**下拉列表中显示时不适用。

## <a name="example"></a>示例

下面的示例演示一种标准的元数据[!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)]类模板。

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

在此示例中，通过该模板后，所需的.NET framework 的最低版本由`RequiredFrameworkVersion`，为 3.0。 使用此模板创建的项目可以从 3.0 开始的.NET Framework 版本为目标。

## <a name="see-also"></a>请参阅

- [Visual Studio 模板架构参考](../extensibility/visual-studio-template-schema-reference.md)
- [创建项目和项模板](../ide/creating-project-and-item-templates.md)
- [Framework 目标概述](../ide/visual-studio-multi-targeting-overview.md)
