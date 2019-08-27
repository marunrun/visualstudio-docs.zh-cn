---
title: Assembly 元素 （Visual Studio 模板向导扩展） |Microsoft Docs
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#Assembly
helpviewer_keywords:
- Assembly element [Visual Studio Template Wizard Extension]
- <Assembly> element [Visual Studio Template Wizard Extension]
ms.assetid: 0c3dc280-1753-4ea2-a13c-d31d13b935b2
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 68fb795005f1f653893147f7013117112f803211
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66352223"
---
# <a name="assembly-element-visual-studio-template-wizard-extension"></a>Assembly 元素 （Visual Studio 模板向导扩展）
指定的名称或实现的程序集的强名称`IWizard`接口。

 \<VSTemplate > \<WizardExtension >\<程序集 >

## <a name="syntax"></a>语法

```
<Assembly>AssemblyName</Assembly>
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
|[WizardExtension](../extensibility/wizardextension-element-visual-studio-templates.md)|包含用于自定义模板向导的注册元素。|

## <a name="text-value"></a>文本值
 需要一个文本值。

 此文本指定实现的程序集`IWizard`接口。 此程序集名称必须指定为完整的程序集名称。 例如 `MyAssembly, Version=1.0.3300.0, Culture=neutral, PublicKeyToken=b03f5f7f11dd0a3a, Custom = null`。

## <a name="remarks"></a>备注
 `Assembly` 是 `WizardExtension` 的必需子元素。

## <a name="example"></a>示例
 下面的示例演示的标准项目模板的元数据[!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)]Windows 应用程序。

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
    <WizardExtension>
        <Assembly>MyWizard, Version=1.0.3300.0, Culture=neutral, PublicKeyToken=b03f5f7f11dd0a3a, Custom=null</Assembly>
        <FullClassName>MyWizard.CustomWizard</FullClassName>
    </WizardExtension>
</VSTemplate>
```

## <a name="see-also"></a>请参阅

- [Visual Studio 模板架构参考](../extensibility/visual-studio-template-schema-reference.md)
- [创建项目和项模板](../ide/creating-project-and-item-templates.md)
- [如何：使用向导来处理项目模板](../extensibility/how-to-use-wizards-with-project-templates.md)