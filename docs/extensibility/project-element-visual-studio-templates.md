---
title: " (Visual Studio 模板) 的项目元素 |Microsoft Docs"
description: 了解项目元素及其如何指定要添加到项目中的文件或目录。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#Project
helpviewer_keywords:
- Project element [Visual Studio Templates]
- <Project> element [Visual Studio Templates]
ms.assetid: 1da15ea6-26e2-462b-a03e-584ef4996579
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 652d438d6a0fdf0c42648ded7d3dc9c18b0212ff
ms.sourcegitcommit: 3d96f7a8c9affab40358c3e81e3472db31d841b2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2020
ms.locfileid: "94672380"
---
# <a name="project-element-visual-studio-templates"></a>Visual Studio 模板 (项目元素) 
指定要添加到项目中的文件或目录。

 \<VSTemplate> \<TemplateContent>
 \<Project>

## <a name="syntax"></a>语法

```
<Project
    File="MyProject.proj"
    TargetFileName="MyTargetProject.proj"
    ReplaceParameters="true/false">
    IgnoreProjectParameter="$myCustomParameter$"
        ...
</Project>
```

## <a name="attributes-and-elements"></a>特性和元素
 以下各部分描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|属性|描述|
|---------------|-----------------|
|`File`|必需的特性。<br /><br /> 指定模板 *.zip* 文件中的项目文件的名称。|
|`ReplaceParameters`|可选特性。<br /><br /> 一个布尔值，指定在从模板创建项目时，项目文件是否具有必须替换的参数值。 默认值为 `false`。|
|`TargetFileName`|可选特性。<br /><br /> 指定从模板创建项目时项目文件的名称。|
|`IgnoreProjectParameter`|可选特性。<br /><br /> 指定是否应将项目添加到当前解决方案。 如果自定义参数的值 "$*myCustomParameter*$" 存在于参数替换文件中，则会创建该项目，但不会将其添加为当前打开的解决方案的一部分。|

### <a name="child-elements"></a>子元素

|元素|说明|
|-------------|-----------------|
|[文件夹](../extensibility/folder-element-visual-studio-project-templates.md)|可选元素。<br /><br /> 指定要添加到项目的文件夹。|
|[ProjectItem](../extensibility/projectitem-element-visual-studio-project-templates.md)|可选元素。<br /><br /> 指定要添加到项目中的文件。|

### <a name="parent-elements"></a>父元素

|元素|说明|
|-------------|-----------------|
|[TemplateContent](../extensibility/templatecontent-element-visual-studio-templates.md)|必需的元素。|

## <a name="remarks"></a>注解
 `Project` 是 `TemplateContent` 的可选子元素。

 `Project`元素用于指定项目，因此仅在项目模板中有效。

 `Project` 元素可以包含 [文件夹](../extensibility/folder-element-visual-studio-project-templates.md) 子元素或 [项目](../extensibility/projectitem-element-visual-studio-project-templates.md) 项子元素，但不能同时包含 `Folder` 和 `ProjectItem` 子元素。

 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 会根据用户在 " **新建项目** " 对话框中输入的名称自动重命名项目文件名。 `TargetFileName`如果要为使用模板创建的项目文件提供备用文件名，请使用特性。

## <a name="example"></a>示例
 下面的示例演示应用程序的项目模板的元数据 [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] 。

```
<VSTemplate Type="Project" Version="3.0.0"
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <Name>My template</Name>
        <Description>A basic starter kit</Description>
        <Icon>TemplateIcon.ico</Icon>
        <ProjectType>CSharp</ProjectType>
    </TemplateData>
    <TemplateContent>
        <Project File="MyStarterKit.csproj">
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
- [项目项元素 (Visual Studio 项目模板) ](../extensibility/projectitem-element-visual-studio-project-templates.md)
- [文件夹元素 (Visual Studio 项目模板) ](../extensibility/folder-element-visual-studio-project-templates.md)
