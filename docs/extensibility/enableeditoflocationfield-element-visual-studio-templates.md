---
title: EnableEditOfLocationField 元素 （Visual Studio 模板） |Microsoft Docs
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- EnableEditOfLocationField (Visual Studio project templates)
ms.assetid: 51a91963-8a3f-4741-928e-bc90c11473bb
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 82a65115ce5df0f57ad9e6ea18a5637e035fed66
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66334543"
---
# <a name="enableeditoflocationfield-element-visual-studio-templates"></a>EnableEditOfLocationField 元素 （Visual Studio 模板）
指定用户可以编辑位置字段。

 \<VSTemplate> \<TemplateData> \<EnableEditOfLocationField>

## <a name="syntax"></a>语法

```
<EnableEditOfLocationField> true/false </EnableEditOfLocationField>
```

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性
 None

### <a name="child-elements"></a>子元素
 None

### <a name="parent-elements"></a>父元素

|元素|描述|
|-------------|-----------------|
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|必需的元素。<br /><br /> 将此模板分类并定义此模板在 **“新建项目”** 或 **“添加新项”** 对话框中的显示方式。|

## <a name="text-value"></a>文本值
 需要一个文本值。

 文本必须是`true`或`false`，则表示用户可以编辑**位置**上的文本框**新项目**对话框。

## <a name="remarks"></a>备注
 `EnableEditOfLocationField` 是可选元素。 默认值是`true`，它允许用户在编辑中的值**位置**中的文本框**新项目**对话框。

 在中**新的项目**对话框中，**位置**文本框中指定新的项目的保存位置的目录。

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
        <EnableEditOfLocationField>false</EnableEditOfLocationField>
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