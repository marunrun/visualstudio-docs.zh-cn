---
title: EnableLocationBrowseButton 元素 （Visual Studio 模板） |Microsoft Docs
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#EnableLocationBrowseButton
helpviewer_keywords:
- EnableLocationBrowseButton [Visual Studio project templates]
ms.assetid: a12d10d8-af49-482a-af77-e084fd07a47d
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 2be2f67d08fcac39d26f9a27f76ad8aff967440b
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66334468"
---
# <a name="enablelocationbrowsebutton-element-visual-studio-templates"></a>EnableLocationBrowseButton 元素 （Visual Studio 模板）
指定是否**浏览**按钮现已推出**新项目**对话框，以便用户可以轻松地修改保存新项目的默认目录。

 \<VSTemplate> \<TemplateData> \<EnableLocationBrowseButton>

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
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|必需的元素。<br /><br /> 将此模板分类并定义此模板在 **“新建项目”** 或 **“添加新项”** 对话框中的显示方式。|

## <a name="text-value"></a>文本值
 需要一个文本值。

 文本必须是`true`或`false`，，该值指示是否显示**浏览**按钮**新项目**对话框。

## <a name="remarks"></a>备注
 `EnableLocationBrowseButton` 是可选元素。 默认值是`true`，其中显示**浏览**按钮**新项目**对话框。

 在中**新的项目**对话框中，**位置**文本框中指定新的项目的保存位置的目录。 **浏览**按钮可帮助你通过显示来修改此目录**项目位置**对话框中，使您可以轻松地导航到另一个计算机上可用的目录，并然后选择为保存新项目的目录。

## <a name="example"></a>示例
 下面的示例演示的元数据[!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)]Windows 应用程序。

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
- [Visual Studio 模板架构参考](../extensibility/visual-studio-template-schema-reference.md)
- [创建项目和项模板](../ide/creating-project-and-item-templates.md)