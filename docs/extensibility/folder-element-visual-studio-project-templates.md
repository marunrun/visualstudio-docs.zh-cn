---
title: Folder 元素（Visual Studio 项目模板） |Microsoft Docs
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#Folder
helpviewer_keywords:
- Folder element [Visual Studio project templates]
ms.assetid: 558e3d41-0db5-4c44-82bb-6bb87892b093
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: b05ef44896e5cd428584c7efed267f130597ee35
ms.sourcegitcommit: f27084e64c79e6428746a20dda92795df996fb31
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85769580"
---
# <a name="folder-element-visual-studio-project-templates"></a>Folder 元素（Visual Studio 项目模板）
指定将添加到项目中的文件夹。

 \<VSTemplate> \<TemplateContent>
 \<Project>
 \<Folder>

## <a name="syntax"></a>语法

```
<Folder Name="Project Folder">
    <Folder> ... </Folder>
    <ProjectItem> ... </ProjectItem>
</Folder>
```

## <a name="attributes-and-elements"></a>特性和元素
 以下各部分描述了特性、子元素和父元素。

### <a name="attributes"></a>属性

|特性|说明|
|---------------|-----------------|
|`Name`|必需的特性。<br /><br /> 项目文件夹的名称。|
|`TargetFolderName`|可选特性。<br /><br /> 指定从模板创建项目时为文件夹指定的名称。 此属性可用于使用参数替换创建文件夹名称，或使用无法直接在 *.zip*文件中使用的国际字符串命名文件夹。|

### <a name="child-elements"></a>子元素

|元素|描述|
|-------------|-----------------|
|`Folder`|指定要添加到项目的文件夹。 `Folder`元素可以包含子 `Folder` 元素。|
|[ProjectItem](../extensibility/projectitem-element-visual-studio-item-templates.md)|指定要添加到项目中的文件。|

### <a name="parent-elements"></a>父元素

|元素|描述|
|-------------|-----------------|
|[Project](../extensibility/project-element-visual-studio-templates.md)|[TemplateContent](../extensibility/templatecontent-element-visual-studio-templates.md)的可选子元素。|

## <a name="remarks"></a>注解
 `Folder`是的一个可选子级 `Project` 。

 你可以使用以下任一方法将项目项组织到模板的文件夹中：

- 在模板 *.zip*文件中包含文件夹，并通过在元素中指定文件的路径 *.vstemplate* `ProjectItem` （不包含元素）将这些文件夹添加到 .vstemplate 文件中的项目 `Folder` 。 这是建议的方法。 例如：

     `...`

     `<ProjectItem>\Folder\item.cs</ProjectItem>`

     `<ProjectItem>Form1.cs</ProjectItem>`

     `...`

- 将文件夹包含在 *.zip*文件中，并将其添加到包含元素的 *.vstemplate*文件中的项目 `Folder` 。 例如：

     `...`

     `<Folder name="Folder">`

     `<ProjectItem>item.cs</ProjectItem>`

     `</Folder>`

     `<ProjectItem>Form1.cs</ProjectItem>`

     `...`

- 不要在模板 *.zip*文件中包含文件夹，但使用元素的属性添加文件夹 `TargetFileName` `ProjectItem` 。 例如：

     `...`

     `<ProjectItem TargetFileName="\Folder\item.cs">item.cs</ProjectItem>`

     `<ProjectItem>Form1.cs</ProjectItem>`

     `...`

## <a name="example"></a>示例
 下面的示例演示了 Windows 应用程序的项目模板的元数据 [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] 。

```
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
            <Folder Name="Properties">
                <ProjectItem>AssemblyInfo.cs</ProjectItem>
                <ProjectItem>Resources.resx</ProjectItem>
                <ProjectItem>Resources.Designer.cs</ProjectItem>
                <ProjectItem>Settings.settings</ProjectItem>
                <ProjectItem>Settings.Designer.cs</ProjectItem>
            </Folder>
        </Project>
    </TemplateContent>
</VSTemplate>
```

## <a name="see-also"></a>请参阅
- [Visual Studio 模板架构参考](../extensibility/visual-studio-template-schema-reference.md)
- [创建项目和项模板](../ide/creating-project-and-item-templates.md)
- [项目项元素（Visual Studio 项模板）](../extensibility/projectitem-element-visual-studio-item-templates.md)
