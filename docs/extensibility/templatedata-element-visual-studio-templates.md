---
title: " (Visual Studio 模板) 的 TemplateData 元素 |Microsoft Docs"
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#TemplateData
helpviewer_keywords:
- TemplateData element [Visual Studio project templates]
ms.assetid: db17ec9b-bfdf-46b1-bbe7-5ccc140056e2
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f3ce0226286e8cc4623b66c043eb7bd376597118
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80699196"
---
# <a name="templatedata-element-visual-studio-templates"></a>TemplateData 元素（Visual Studio 模板）
将此模板分类并定义此模板在 **“新建项目”** 或 **“添加新项”** 对话框中的显示方式。

 \<VSTemplate> \<TemplateData>

## <a name="syntax"></a>语法

```
<TemplateData>
    <Name> ... </Name>
    <Description> ... </Description>
    <Icon> ... </Icon>
    <ProjectType> ... </ProjectType>
    ...
</TemplateData>
```

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性
 无。

### <a name="child-elements"></a>子元素

| 元素 | 说明 |
| - | - |
| [名称](../extensibility/name-element-visual-studio-templates.md) | 必需的元素。<br /><br /> 指定模板在 " **新建项目** " 或 " **添加新项** " 对话框中显示的名称。 |
| [说明](../extensibility/description-element-visual-studio-templates.md) | 必需的元素。<br /><br /> 指定在 " **新建项目** " 或 " **添加新项** " 对话框中显示的模板的说明。 |
| [Icon](../extensibility/icon-element-visual-studio-templates.md) | 必需的元素。<br /><br /> 指定图像文件的路径和文件名，该图像文件将显示在模板的 " **新建项目** " 或 " **添加新项** " 对话框中。 |
| [ProjectType](../extensibility/projecttype-element-visual-studio-templates.md) | 必需的元素。<br /><br /> 对项目模板进行分类，使其显示在 " **新建项目** " 对话框中的指定组下。 |
| [ProjectSubType](../extensibility/projectsubtype-element-visual-studio-templates.md) | 可选元素。<br /><br /> 对项目模板进行分类，使其显示在 " **新建项目** " 对话框中的指定子类别下。 |
| [TemplateID](../extensibility/templateid-element-visual-studio-templates.md) | 可选元素。<br /><br /> 指定模板 ID。 |
| [TemplateGroupID](../extensibility/templategroupid-element-visual-studio-templates.md) | 可选元素。<br /><br /> 指定模板组 ID。 |
| [SortOrder](../extensibility/sortorder-element-visual-studio-templates.md) | 可选元素。<br /><br /> 指定一个值，该值用于在同一类别中的其他模板之间进行排列，如在 " **新建项目** " 或 " **添加新项** " 对话框中显示的模板。 |
| [CreateNewFolder](../extensibility/createnewfolder-element-visual-studio-templates.md) | 可选元素。<br /><br /> 指定在实例化项目时是否创建包含文件夹。 |
| [DefaultName](../extensibility/defaultname-element-visual-studio-templates.md) | 可选元素。<br /><br /> 指定 Visual Studio 项目系统在创建项目或项时为其生成的名称。 |
| [ProvideDefaultName](../extensibility/providedefaultname-element-visual-studio-templates.md) | 可选元素。<br /><br /> 指定在创建项目或项时，Visual Studio 项目系统是否会生成默认名称。 |
| [PromptForSaveOnCreation](../extensibility/promptforsaveoncreation-element-visual-studio-templates.md) | 可选元素。<br /><br /> 指定是否可以将项目创建为仅)  (Visual Studio 2017 的临时项目。 |
| [EnableLocationBrowseButton](../extensibility/enablelocationbrowsebutton-element-visual-studio-templates.md) | 可选元素。<br /><br /> 指定 "**新建项目**" 对话框中的 "**浏览**" 按钮是否可用，以便用户可以轻松地修改保存新项目的默认目录。 |
| [Hidden](../extensibility/hidden-element-visual-studio-templates.md) | 可选元素。<br /><br /> 指定模板是否出现在 " **新建项目** " 或 " **添加新项** " 对话框中。 |
| [NumberOfParentCategoriesToRollUp](../extensibility/numberofparentcategoriestorollup-visual-studio-templates.md) | 可选元素。<br /><br /> 指定将在 " **新建项目** " 对话框中显示模板的父类别的数目。 |
| [LocationFieldMRUPrefix](../extensibility/locationfieldmruprefix-element-visual-studio-templates.md) | 可选元素。 |
| [LocationField](../extensibility/locationfield-element-visual-studio-project-templates.md) | 可选元素。<br /><br /> 指定是否为项目模板启用、禁用或隐藏 "**新项目**" 对话框中的 "**位置**" 文本框。 |
| [RequiredFrameworkVersion](../extensibility/requiredframeworkversion-element-visual-studio-templates.md) | 可选元素。<br /><br /> 如果模板仅支持特定的最低版本及更高版本的 .NET Framework，请使用此元素。 |
| [SupportsMasterPage](../extensibility/supportsmasterpage-element-visual-studio-templates.md) | 可选元素。<br /><br /> 指定模板是否支持 web 项目的母版页。 |
| [SupportsCodeSeparation](../extensibility/supportscodeseparation-element-visual-studio-templates.md) | 可选元素。<br /><br /> 指定模板是否支持 web 项目的代码分离或代码隐藏页面模型。 |
| [SupportsLanguageDropDown](../extensibility/supportslanguagedropdown-element-visual-studio-templates.md) | 可选元素。<br /><br /> 指定对于多种语言，模板是否相同，以及是否在 "**新建项目**" 对话框中提供 "**语言**" 选项。 |
| [TargetPlatformName](../extensibility/targetplatformname-element-visual-studio-templates.md) | 可选元素。<br /><br /> 指定项目模板面向的平台。 此元素指定使用项目模板创建 [!INCLUDE[win8_appname_long](../debugger/includes/win8_appname_long_md.md)] 应用。 |

### <a name="parent-elements"></a>父元素

|元素|说明|
|-------------|-----------------|
|[VSTemplate](../extensibility/vstemplate-element-visual-studio-templates.md)|必需的元素。<br /><br /> 包含项目模板、项模板或初学者工具包的所有元数据。|

## <a name="remarks"></a>备注
 `TemplateData` 是必需的元素。

 如果不包含可选元素，则使用该元素的默认值。

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

## <a name="see-also"></a>另请参阅
- [Visual Studio 模板架构参考](../extensibility/visual-studio-template-schema-reference.md)
- [创建项目和项模板](../ide/creating-project-and-item-templates.md)
