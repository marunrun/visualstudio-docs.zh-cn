---
title: 启用位置浏览按钮元素（视觉工作室模板） |微软文档
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#EnableLocationBrowseButton
helpviewer_keywords:
- EnableLocationBrowseButton [Visual Studio project templates]
ms.assetid: a12d10d8-af49-482a-af77-e084fd07a47d
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 263157d5c6fefc208f28caa55475ba329a0d230f
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80711978"
---
# <a name="enablelocationbrowsebutton-element-visual-studio-templates"></a>启用位置浏览按钮元素（可视化工作室模板）
指定 **"浏览"** 按钮在 **"新项目**"对话框中是否可用，以便用户可以轻松地修改保存新项目的默认目录。

 \<VS模板>\<模板数据>\<启用位置浏览按钮>

## <a name="syntax"></a>语法

```
<EnableLocationBrowseButton> true/false </EnableLocationBrowseButton>
```

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性
 无。

### <a name="child-elements"></a>子元素
 无。

### <a name="parent-elements"></a>父元素

|元素|描述|
|-------------|-----------------|
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|必需元素。<br /><br /> 将此模板分类并定义此模板在 **“新建项目”** 或 **“添加新项”** 对话框中的显示方式。|

## <a name="text-value"></a>文本值
 需要一个文本值。

 文本必须为 或`true``false`，指示是否在 **"新项目**"对话框上显示 **"浏览**"按钮。

## <a name="remarks"></a>备注
 `EnableLocationBrowseButton` 是可选元素。 默认值为`true`，在 **"新项目**"对话框中显示 **"浏览**"按钮。

 在"**新项目**"对话框中，"**位置**"文本框指定保存新项目的目录。 **"浏览"** 按钮通过显示 **"项目位置**"对话框来帮助您修改此目录，该对话框使您能够轻松导航到计算机中可用的其他目录，然后选择该目录作为保存新项目的目录。

## <a name="example"></a>示例
 下面的示例演示了[!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)]Windows 应用程序的元数据。

```
<VSTemplate Type="Project" Version="3.0.0"
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <Name>My template</Name>
        <Description>A basic starter kit</Description>
        <Icon>TemplateIcon.ico</Icon>
        <ProjectType>CSharp</ProjectType>
        <EnableLocationBrowseButton>false</EnableLocationBrowseButton>
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
