---
title: TemplateData 元素 （Visual Studio 模板） |Microsoft Docs
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#TemplateData
helpviewer_keywords:
- TemplateData element [Visual Studio project templates]
ms.assetid: db17ec9b-bfdf-46b1-bbe7-5ccc140056e2
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f9647330aaca2c2ae91aa7e461da17cf4dc3f8c3
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66316674"
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

| 元素 | 描述 |
| - | - |
| [名称](../extensibility/name-element-visual-studio-templates.md) | 必需的元素。<br /><br /> 指定的模板的名称中出现**新的项目**或**添加新项**对话框。 |
| [说明](../extensibility/description-element-visual-studio-templates.md) | 必需的元素。<br /><br /> 指定模板的说明中所示**新的项目**或**添加新项**对话框。 |
| [图标](../extensibility/icon-element-visual-studio-templates.md) | 必需的元素。<br /><br /> 指定的路径和用作中显示该图标的图像文件的文件名**新的项目**或**添加新项**对话框中的，为模板。 |
| [ProjectType](../extensibility/projecttype-element-visual-studio-templates.md) | 必需的元素。<br /><br /> 将分类的项目模板，使其显示在指定的组**新的项目**对话框。 |
| [ProjectSubType](../extensibility/projectsubtype-element-visual-studio-templates.md) | 可选元素。<br /><br /> 将分类的项目模板，使其出现在中的指定子类别下**新的项目**对话框。 |
| [TemplateID](../extensibility/templateid-element-visual-studio-templates.md) | 可选元素。<br /><br /> 指定模板 id。 |
| [TemplateGroupID](../extensibility/templategroupid-element-visual-studio-templates.md) | 可选元素。<br /><br /> 指定模板组 id。 |
| [SortOrder](../extensibility/sortorder-element-visual-studio-templates.md) | 可选元素。<br /><br /> 指定一个值，用于排列在同一类别中的其他模板之间的模板中显示该值**新的项目**或**添加新项**对话框。 |
| [CreateNewFolder](../extensibility/createnewfolder-element-visual-studio-templates.md) | 可选元素。<br /><br /> 指定是否在实例化项目的创建包含文件夹。 |
| [DefaultName](../extensibility/defaultname-element-visual-studio-templates.md) | 可选元素。<br /><br /> 在创建时指定 Visual Studio 项目系统将生成的项目或项目的名称。 |
| [ProvideDefaultName](../extensibility/providedefaultname-element-visual-studio-templates.md) | 可选元素。<br /><br /> 指定是否在创建时，Visual Studio 项目系统将生成项目或项的默认名称。 |
| [PromptForSaveOnCreation](../extensibility/promptforsaveoncreation-element-visual-studio-templates.md) | 可选元素。<br /><br /> 指定项目是否可以创建为临时项目 (Visual Studio 2017 仅)。 |
| [EnableLocationBrowseButton](../extensibility/enablelocationbrowsebutton-element-visual-studio-templates.md) | 可选元素。<br /><br /> 指定是否**浏览**按钮现已推出**新项目**对话框，以便用户可以轻松地修改保存新项目的默认目录。 |
| [Hidden](../extensibility/hidden-element-visual-studio-templates.md) | 可选元素。<br /><br /> 指定模板是否出现在**新的项目**或**添加新项**对话框。 |
| [NumberOfParentCategoriesToRollUp](../extensibility/numberofparentcategoriestorollup-visual-studio-templates.md) | 可选元素。<br /><br /> 指定将显示在此模板的父类别数**新的项目**对话框。 |
| [LocationFieldMRUPrefix](../extensibility/locationfieldmruprefix-element-visual-studio-templates.md) | 可选元素。 |
| [LocationField](../extensibility/locationfield-element-visual-studio-project-templates.md) | 可选元素。<br /><br /> 指定是否**位置**文本框中**新项目**对话框的已启用、 禁用或隐藏项目模板。 |
| [RequiredFrameworkVersion](../extensibility/requiredframeworkversion-element-visual-studio-templates.md) | 可选元素。<br /><br /> 如果该模板仅支持特定的最低版本和更高版本，如果任何.NET Framework，请使用此元素。 |
| [SupportsMasterPage](../extensibility/supportsmasterpage-element-visual-studio-templates.md) | 可选元素。<br /><br /> 指定模板是否支持 web 项目的主页面。 |
| [SupportsCodeSeparation](../extensibility/supportscodeseparation-element-visual-studio-templates.md) | 可选元素。<br /><br /> 指定是否在模板支持单独的代码或代码隐藏页模型，用于 web 项目。 |
| [SupportsLanguageDropDown](../extensibility/supportslanguagedropdown-element-visual-studio-templates.md) | 可选元素。<br /><br /> 指定该模板是完全相同的多个语言，以及是否**语言**选项才可用**新项目**对话框。 |
| [TargetPlatformName](../extensibility/targetplatformname-element-visual-studio-templates.md) | 可选元素。<br /><br /> 指定项目模板面向的平台。 此元素指定的项目模板用于创建[!INCLUDE[win8_appname_long](../debugger/includes/win8_appname_long_md.md)]应用。 |

### <a name="parent-elements"></a>父元素

|元素|描述|
|-------------|-----------------|
|[VSTemplate](../extensibility/vstemplate-element-visual-studio-templates.md)|必需的元素。<br /><br /> 包含项目模板、 项模板或初学者工具包的所有元数据。|

## <a name="remarks"></a>备注
 `TemplateData` 是必需的元素。

 如果不包括可选元素，使用该元素的默认值。

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