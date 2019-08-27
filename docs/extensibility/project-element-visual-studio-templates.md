---
title: 项目元素 （Visual Studio 模板） |Microsoft Docs
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#Project
helpviewer_keywords:
- Project element [Visual Studio Templates]
- <Project> element [Visual Studio Templates]
ms.assetid: 1da15ea6-26e2-462b-a03e-584ef4996579
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 843ba7935dbddb95c9a3043deff534db9157f15b
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66336052"
---
# <a name="project-element-visual-studio-templates"></a>Project 元素 （Visual Studio 模板）
指定的文件或目录将添加到项目。

 \<VSTemplate> \<TemplateContent> \<Project>

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

|特性|描述|
|---------------|-----------------|
|`File`|必需的特性。<br /><br /> 在模板中指定的项目文件的名称 *.zip*文件。|
|`ReplaceParameters`|可选特性。<br /><br /> 一个布尔值，该值指定项目文件是否可以从模板创建项目时，必须将其替换的参数值。 默认值是 `false`。|
|`TargetFileName`|可选特性。<br /><br /> 从模板创建项目时，请指定项目文件的名称。|
|`IgnoreProjectParameter`|可选特性。<br /><br /> 指定是否应将项目添加到当前解决方案。 如果自定义参数的值"$*myCustomParameter*$"存在在参数替换文件中，项目已创建但不是作为当前打开的解决方案的一部分添加。|

### <a name="child-elements"></a>子元素

|元素|描述|
|-------------|-----------------|
|[文件夹](../extensibility/folder-element-visual-studio-project-templates.md)|可选元素。<br /><br /> 指定要添加到项目的文件夹。|
|[ProjectItem](../extensibility/projectitem-element-visual-studio-project-templates.md)|可选元素。<br /><br /> 指定要向项目中添加的文件。|

### <a name="parent-elements"></a>父元素

|元素|描述|
|-------------|-----------------|
|[TemplateContent](../extensibility/templatecontent-element-visual-studio-templates.md)|必需的元素。|

## <a name="remarks"></a>备注
 `Project` 是 `TemplateContent` 的可选子元素。

 `Project`元素是用于指定一个项目，因此，仅在项目模板中有效。

 `Project` 元素可以具有[文件夹](../extensibility/folder-element-visual-studio-project-templates.md)子元素或[ProjectItem](../extensibility/projectitem-element-visual-studio-project-templates.md)子元素中，但不是这两者的混合`Folder`和`ProjectItem`子元素。

 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 会自动重命名基于用户输入的名称的项目文件名称**新的项目**对话框。 使用`TargetFileName`属性如果您想要提供有关使用模板创建的项目文件的备用文件名称。

## <a name="example"></a>示例
 下面的示例演示用于的项目模板的元数据[!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)]应用程序。

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
- [ProjectItem 元素 （Visual Studio 项目模板）](../extensibility/projectitem-element-visual-studio-project-templates.md)
- [Folder 元素 （Visual Studio 项目模板）](../extensibility/folder-element-visual-studio-project-templates.md)