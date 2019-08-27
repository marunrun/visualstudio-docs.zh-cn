---
title: BuildOnLoad 属性和元素 （Visual Studio 模板）
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#BuildOnLoad
helpviewer_keywords:
- BuildOnLoad attribute [Visual Studio Templates]
- BuildOnLoad element [Visual Studio Templates]
ms.assetid: 950f5fc1-d041-4090-9a5c-60844768a4cc
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f32056aae3c860aee250248c606bbda4dbf9506c
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66321274"
---
# <a name="buildonload-attribute-and-element"></a>BuildOnLoad 属性和元素

指定是否在创建后立即生成项目。 **BuildOnLoad**是属性和元素。

元素层次结构：

```xml
<VSTemplate>
  <TemplateData>
    <BuildOnLoad>
```

## <a name="element-syntax"></a>元素语法

```xml
<BuildOnLoad> true/false </BuildOnLoad>
```

## <a name="parent-elements"></a>父元素

|元素|描述|
|-------------|-----------------|
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|将此模板分类并定义此模板在 **“新建项目”** 或 **“添加新项”** 对话框中的显示方式。|

## <a name="text-value"></a>文本值

文本值为必填**BuildOnLoad**元素。 文本必须是`true`或`false`，该值指示是否在创建后立即生成项目。

## <a name="remarks"></a>备注

**BuildOnLoad**为可选属性。 默认值为 `false`。

## <a name="example"></a>示例

下面的示例演示的元数据C#模板时**BuildOnLoad**用作元素：

```xml
<VSTemplate Type="Project" Version="3.0.0"
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <Name>My template</Name>
        <Description>A basic template</Description>
        <Icon>TemplateIcon.ico</Icon>
        <ProjectType>CSharp</ProjectType>
        <BuildOnLoad>true</BuildOnLoad>
    </TemplateData>
    <TemplateContent>
        <Project File="MyTemplate.csproj">
            <ProjectItem>Form1.cs<ProjectItem>
            <ProjectItem>Form1.Designer.cs</ProjectItem>
            <ProjectItem>Program.cs</ProjectItem>
            <ProjectItem>Properties\AssemblyInfo.cs</ProjectItem>
            <ProjectItem>Properties\Resources.resx</ProjectItem>
            <ProjectItem>Properties\Resources.Designer.cs</ProjectItem>
            <ProjectItem>Properties\Settings.settings</ProjectItem>
            <ProjectItem>Properties\Settings.Designer.cs</ProjectItem>
        </Project>
    </TemplateContent>
</VSTemplate>
```

## <a name="see-also"></a>请参阅

- [BuildProjectOnload 元素](buildprojectonload-element-visual-studio-templates.md)
- [TemplateContent 元素](../extensibility/templatecontent-element-visual-studio-templates.md)
- [创建项目和项模板](../ide/creating-project-and-item-templates.md)
- [Visual Studio 模板架构参考](../extensibility/visual-studio-template-schema-reference.md)