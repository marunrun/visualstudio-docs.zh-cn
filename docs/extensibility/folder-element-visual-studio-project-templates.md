---
title: 文件夹元素（可视化工作室项目模板） |微软文档
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: conceptual
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
ms.openlocfilehash: cb256b8be0dd9ce68f193750bf3ff5a383d5f073
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80711466"
---
# <a name="folder-element-visual-studio-project-templates"></a>文件夹元素（可视化工作室项目模板）
指定将添加到项目的文件夹。

 \<模板>\<模板内容>\<项目>\<文件夹>

## <a name="syntax"></a>语法

```
<Folder Name="Project Folder">
    <Folder> ... </Folder>
    <ProjectItem> ... </ProjectItem>
</Folder>
```

## <a name="attributes-and-elements"></a>特性和元素
 以下各部分描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|特性|描述|
|---------------|-----------------|
|`Name`|必需的特性。<br /><br /> 项目文件夹的名称。|
|`TargetFolderName`|可选特性。<br /><br /> 指定从模板创建项目时要为文件夹提供的名称。 此属性可用于使用参数替换创建文件夹名称或使用无法直接在 *.zip*文件中直接使用的国际字符串命名文件夹。|

### <a name="child-elements"></a>子元素

|元素|描述|
|-------------|-----------------|
|`Folder`|指定要添加到项目的文件夹。 `Folder`元素可以包含子`Folder`元素。|
|[ProjectItem](../extensibility/projectitem-element-visual-studio-item-templates.md)|指定要添加到项目的文件。|

### <a name="parent-elements"></a>父元素

|元素|描述|
|-------------|-----------------|
|[Project](../extensibility/project-element-visual-studio-templates.md)|[模板内容](../extensibility/templatecontent-element-visual-studio-templates.md)的可选子元素 。|

## <a name="remarks"></a>备注
 `Folder`是`Project`的可选子项。

 可以使用以下任一方法将项目项目组织到模板中的文件夹中：

- 将文件夹包含在模板 *.zip*文件中，并通过在`ProjectItem`元素中指定文件路径（没有`Folder`元素）将它们添加到 *.vstemplate*文件中的项目。 这是建议的方法。 例如：

     `...`

     `<ProjectItem>\Folder\item.cs</ProjectItem>`

     `<ProjectItem>Form1.cs</ProjectItem>`

     `...`

- 将文件夹包含在模板 *.zip*文件中，并将它们添加到包含`Folder`元素的 *.vstemplate*文件中的项目。 例如：

     `...`

     `<Folder name="Folder">`

     `<ProjectItem>item.cs</ProjectItem>`

     `</Folder>`

     `<ProjectItem>Form1.cs</ProjectItem>`

     `...`

- 不要在模板 *.zip*文件中包含文件夹，而是使用`TargetFileName``ProjectItem`元素的属性添加文件夹。 例如：

     `...`

     `<ProjectItem TargetFileName="\Folder\item.cs">item.cs</ProjectItem>`

     `<ProjectItem>Form1.cs</ProjectItem>`

     `...`

## <a name="example"></a>示例
 下面的示例演示了[!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)]Windows 应用程序的项目模板的元数据。

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
- [可视化工作室模板架构参考](../extensibility/visual-studio-template-schema-reference.md)
- [创建项目和项模板](../ide/creating-project-and-item-templates.md)
- [项目项目元素（可视化工作室项目模板）](../extensibility/projectitem-element-visual-studio-item-templates.md)
