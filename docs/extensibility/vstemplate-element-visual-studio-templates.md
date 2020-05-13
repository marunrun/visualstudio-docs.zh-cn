---
title: VSTemplate 元素（视觉工作室模板） |微软文档
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#VSTemplate
helpviewer_keywords:
- VSTemplate element [Visual Studio project templates]
ms.assetid: f8ac561b-3b0b-4246-9ec9-118d2447e9a9
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 651e8b6dbbe11c450b105f3185e7e987bb30da9b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80697870"
---
# <a name="vstemplate-element-visual-studio-templates"></a>VSTemplate 元素（可视化工作室模板）
包含有关项目模板、项目模板或初学者工具包的所有元数据。

## <a name="syntax"></a>语法

```csharp
<VSTemplate Type="TemplateType" Version="x.x.x">
    <TemplateData>    </TemplateData>
    <TemplateContent>    </TemplateContent>
    ...
</VSTemplate>
```

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

| 特性 | 描述 |
|-----------| - |
| `Type` | 将模板标识为项目模板或项目模板。 此属性可以具有`Project`或`Item`的值。 |
| `Version` | 指定模板的版本号。 中的[!INCLUDE[vs_dev10_long](../code-quality/includes/vs_dev10_long_md.md)]模板，并且[!INCLUDE[vs_dev11_long](../data-tools/includes/vs_dev11_long_md.md)]`Version`具有 的属性`3.0.0`值 。 |

### <a name="child-elements"></a>子元素

|元素|描述|
|-------------|-----------------|
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|必需元素。<br /><br /> 指定对模板进行分类的数据，并定义模板在 **"新项目**"或 **"添加新项目**"对话框中的显示方式。|
|[模板内容](../extensibility/templatecontent-element-visual-studio-templates.md)|必需元素。<br /><br /> 指定模板的内容。|
|[WizardExtension](../extensibility/wizardextension-element-visual-studio-templates.md)|可选元素。|
|[WizardData](../extensibility/wizarddata-element-visual-studio-templates.md)|可选元素。|

### <a name="parent-elements"></a>父元素
 无。

## <a name="remarks"></a>备注
 该`VSTemplate`元素是 *.vstemplate*文件的根元素。

## <a name="example"></a>示例
 下面的示例显示了[!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)]应用程序的项目模板的元数据。

```xml
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
            <ProjectItem>Form1.cs</ProjectItem>
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
