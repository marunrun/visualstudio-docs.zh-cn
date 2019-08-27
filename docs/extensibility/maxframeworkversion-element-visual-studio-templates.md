---
title: MaxFrameworkVersion 元素 （Visual Studio 模板） |Microsoft Docs
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- <MaxFrameworkVersion> Element (Visual Studio Templates)
- MaxFrameworkVersion Element (Visual Studio Templates)
ms.assetid: f732a9d3-fc29-405b-9298-01ea83fc58b8
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 0a00e174e3454dcb054c13252ef699a7cbc87df8
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66318598"
---
# <a name="maxframeworkversion-element-visual-studio-templates"></a>MaxFrameworkVersion 元素 （Visual Studio 模板）

指定模板所需的.NET framework 的最大版本。 它确定在可用的最大值**目标框架版本**下拉列表中的**新项目**对话框。 为了使用户能够选择的框架版本，还必须指定[RequiredFrameworkVersion](../extensibility/requiredframeworkversion-element-visual-studio-templates.md)作为模板的最低.NET Framework 版本。

> [!IMPORTANT]
> 在 Visual Studio 2017 版本 15.6 版中，启动**目标框架版本**下拉列表中不再是中的显示模板的筛选器**模板**一部分**新项目**对话框。 相反，**目标框架版本**用作所选模板的 framework 选取器下拉列表。

 \<VSTemplate> \<TemplateData> \<MaxFrameworkVersion>

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
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|必需的元素。<br /><br /> 此模板分类并定义如何显示在**新的项目**或**添加新项**对话框。|

## <a name="text-value"></a>文本值
 需要一个文本值。

 此文本必须由模板允许的.NET framework 的最高版本号。

## <a name="remarks"></a>备注

`MaxFrameworkVersion` 是可选元素。 `MaxFrameworkVersion`应忽略元素，除非它是必需的以免无意中限制模板支持.NET Framework 版本。 它应该也省略如果.NET Framework 不是适用于该模板。

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

在此示例中，最高版本的.NET framework 的所需的模板，以表示`MaxFrameworkVersion`，是 4.7.1。 使用此模板创建的项目可面向.NET Framework 4.7.1 它之前的版本。

## <a name="see-also"></a>请参阅

- [Visual Studio 模板架构参考](../extensibility/visual-studio-template-schema-reference.md)
- [创建项目和项模板](../ide/creating-project-and-item-templates.md)
