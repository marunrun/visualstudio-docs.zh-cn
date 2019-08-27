---
title: 命名元素 （Visual Studio 模板） |Microsoft Docs
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#Name
helpviewer_keywords:
- Name element [Visual Studio project templates]
ms.assetid: 48788dbf-7da0-4443-8061-aab966fc22c8
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 6b0365740f5ea8ab20ed79d077134afd32356bcc
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66344723"
---
# <a name="name-element-visual-studio-templates"></a>Name 元素 （Visual Studio 模板）
指定的模板的名称，如所示**新的项目**或**添加新项**对话框。

 \<VSTemplate> \<TemplateData> \<Name>

## <a name="syntax"></a>语法

```xml
<Name> Template Name </Name>
```

```xml
<Name Package="{PackageID}" ID="ResourceID" />
```

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|特性|描述|
|---------------|-----------------|
|`Package`|适用于高级的用户情形的可选属性。<br /><br /> 指定 Visual Studio 包的 GUID id。|
|`ID`|适用于高级的用户情形的可选属性。<br /><br /> 指定 Visual Studio 资源 id。|

### <a name="child-elements"></a>子元素
 无。

### <a name="parent-elements"></a>父元素

|元素|描述|
|-------------|-----------------|
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|必需的元素。<br /><br /> 将此模板分类并定义此模板在 **“新建项目”** 或 **“添加新项”** 对话框中的显示方式。|

## <a name="text-value"></a>文本值
 文本值是必需的除非`Package`和`ID`使用属性。

 此文本提供的模板的名称。

## <a name="remarks"></a>备注
 `Name` 是 `TemplateData` 的必需子元素。

## <a name="example"></a>示例
 下面的示例演示用于的项目模板的元数据[!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)]应用程序。

```xml
<VSTemplate Type="Project" Version="3.0.0"
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <Name>My template</Name>
        <Description>A basic template</Description>
        <Icon>TemplateIcon.ico</Icon>
        <ProjectType>CSharp</ProjectType>
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
- [Visual Studio 模板架构参考](../extensibility/visual-studio-template-schema-reference.md)
- [创建项目和项模板](../ide/creating-project-and-item-templates.md)