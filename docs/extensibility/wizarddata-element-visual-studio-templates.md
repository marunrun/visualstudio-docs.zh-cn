---
title: WizardData 元素 （Visual Studio 模板） |Microsoft Docs
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#WizardData
helpviewer_keywords:
- WizardData element [Visual Studio Templates]
- <WizardData> element [Visual Studio Templates]
ms.assetid: d0403a16-5d07-4fe5-b474-19ae3d9fd3ab
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ad5ae7e2e83cb0f8db6cf0b2482547e66ab89497
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66350767"
---
# <a name="wizarddata-element-visual-studio-templates"></a>WizardData 元素（Visual Studio 模板）

指定自定义 XML

```xml
\<VSTemplate>
\<WizardData>
```

## <a name="syntax"></a>语法

```xml
<WizardData>
    <!-- XML to pass to the custom wizard extension -->
    ...
</WizardData>
```

## <a name="attributes-and-elements"></a>特性和元素

以下各部分描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

无。

### <a name="child-elements"></a>子元素

无。

### <a name="parent-elements"></a>父元素

|元素|描述|
|-------------|-----------------|
|[VSTemplate](../extensibility/vstemplate-element-visual-studio-templates.md)|必需的元素。<br /><br /> 包含项目模板、 项模板或初学者工具包的所有元数据。|

## <a name="text-value"></a>文本值

文本值是可选的。

此文本指定要传递给指定的自定义向导扩展的自定义 XML [WizardExtension](../extensibility/wizardextension-element-visual-studio-templates.md)元素。

## <a name="remarks"></a>备注

可以在此元素中指定任何 XML。 XML 将会作为参数传递给自定义向导扩展，允许使用此元素的内容的扩展名。 对此数据不进行任何验证。

内容**WizardData**保持不变，作为参数的字符串字典中的参数内传递元素`IWizard.RunStarted`方法。 字典的键名为`$wizarddata$`。

## <a name="example"></a>示例

下面的示例演示的标准项目模板的元数据C#Windows 应用程序。

```xml
<VSTemplate Version="3.0.0" Type="Item"
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <Name>MyTemplate</Name>
        <Description>Template using IWizard extension</Description>
        <Icon>TemplateIcon.ico</Icon>
        <ProjectType>CSharp</ProjectType>
    </TemplateData>
    <TemplateContent>
        <Project File="MyTemplate.csproj">
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
    <WizardExtension>
        <Assembly>MyWizard, Version=1.0.3300.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a, Custom=null</Assembly>
        <FullClassName>MyWizard.CustomWizard</FullClassName>
    </WizardExtension>
    <WizardData>
        <!-- XML to pass to the custom wizard extension -->
    </WizardData>
</VSTemplate>
```

## <a name="see-also"></a>请参阅

- [Visual Studio 模板架构参考](../extensibility/visual-studio-template-schema-reference.md)
- [创建项目和项模板](../ide/creating-project-and-item-templates.md)
- [WizardExtension 元素（Visual Studio 模板）](../extensibility/wizardextension-element-visual-studio-templates.md)
- [如何：使用向导来处理项目模板](../extensibility/how-to-use-wizards-with-project-templates.md)