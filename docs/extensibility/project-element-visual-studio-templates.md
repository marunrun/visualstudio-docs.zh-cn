---
title: 项目元素（可视化工作室模板） |微软文档
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
ms.openlocfilehash: 335a1e4efa62f07e10bb24b9971627d24bb13273
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80702002"
---
# <a name="project-element-visual-studio-templates"></a>项目元素（可视化工作室模板）
指定要添加到项目的文件或目录。

 \<VStemplate \<>模板内容\<>项目>

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
|`File`|必需的特性。<br /><br /> 在模板 *.zip*文件中指定项目文件的名称。|
|`ReplaceParameters`|可选特性。<br /><br /> 布尔值，用于指定项目文件是否具有从模板创建项目时必须替换的参数值。 默认值为 `false`。|
|`TargetFileName`|可选特性。<br /><br /> 指定从模板创建项目时的项目文件的名称。|
|`IgnoreProjectParameter`|可选特性。<br /><br /> 指定是否应将项目添加到当前解决方案。 如果自定义参数的值 *"$myCustom 参数*$"存在于参数替换文件中，则项目将创建，但不会作为当前打开的解决方案的一部分添加。|

### <a name="child-elements"></a>子元素

|元素|描述|
|-------------|-----------------|
|[文件夹](../extensibility/folder-element-visual-studio-project-templates.md)|可选元素。<br /><br /> 指定要添加到项目的文件夹。|
|[ProjectItem](../extensibility/projectitem-element-visual-studio-project-templates.md)|可选元素。<br /><br /> 指定要添加到项目的文件。|

### <a name="parent-elements"></a>父元素

|元素|描述|
|-------------|-----------------|
|[模板内容](../extensibility/templatecontent-element-visual-studio-templates.md)|必需元素。|

## <a name="remarks"></a>备注
 `Project` 是 `TemplateContent` 的可选子元素。

 该`Project`元素用于指定项目，因此仅在项目模板中有效。

 `Project`元素可以具有[文件夹](../extensibility/folder-element-visual-studio-project-templates.md)子元素或[ProjectItem](../extensibility/projectitem-element-visual-studio-project-templates.md)子元素，但不能混合两个`Folder`子`ProjectItem`元素和子元素。

 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]根据用户在 **"新项目**"对话框中输入的名称自动重命名项目文件名。 如果要为`TargetFileName`使用模板创建的项目文件提供备用文件名，请使用 该属性。

## <a name="example"></a>示例
 下面的示例显示了[!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)]应用程序的项目模板的元数据。

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
- [可视化工作室模板架构参考](../extensibility/visual-studio-template-schema-reference.md)
- [创建项目和项模板](../ide/creating-project-and-item-templates.md)
- [项目项目元素（可视化工作室项目模板）](../extensibility/projectitem-element-visual-studio-project-templates.md)
- [文件夹元素（可视化工作室项目模板）](../extensibility/folder-element-visual-studio-project-templates.md)
