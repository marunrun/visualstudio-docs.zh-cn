---
title: 'FullClassName 元素 (VS template wizard extension) '
description: 了解 FullClassName 元素，以及它是实现 IWizard 接口的类的完全限定名称。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#FullClassName
helpviewer_keywords:
- FullClassName element [Visual Studio project template]
ms.assetid: 651e1010-d529-4856-85ff-c77ceca5d2ed
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 987a97a34c846f93ef52765375c1512dd8968fb1
ms.sourcegitcommit: 3d96f7a8c9affab40358c3e81e3472db31d841b2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2020
ms.locfileid: "94672738"
---
# <a name="fullclassname-element-visual-studio-template-wizard-extension"></a> (Visual Studio 模板向导扩展的 FullClassName 元素) 
实现接口的类的完全限定名称 `IWizard` 。

 \<VSTemplate> \<WizardExtension>
... \<FullClassName>

## <a name="syntax"></a>语法

```xml
<FullClassName>ClassName</FullClassName>
```

## <a name="attributes-and-elements"></a>特性和元素
 以下各部分描述了特性、子元素和父元素。

### <a name="attributes"></a>特性
 无。

### <a name="child-elements"></a>子元素
 无。

### <a name="parent-elements"></a>父元素

|元素|说明|
|-------------|-----------------|
|[WizardExtension](../extensibility/wizardextension-element-visual-studio-templates.md)|包含用于自定义模板向导的注册元素。|

## <a name="text-value"></a>文本值
 需要一个文本值。

 此文本指定实现接口的类 `IWizard` 。 指定的类必须存在于 [assembly](../extensibility/assembly-element-visual-studio-template-wizard-extension.md) 元素指定的程序集中。

## <a name="remarks"></a>注解
 `FullClassName` 是 `WizardExtension` 的必需子元素。

## <a name="example"></a>示例
 下面的示例演示了 Windows 应用程序的标准项目模板的元数据 [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] 。

```
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
</VSTemplate>
```

## <a name="see-also"></a>请参阅
- [Visual Studio 模板架构参考](../extensibility/visual-studio-template-schema-reference.md)
- [创建项目和项模板](../ide/creating-project-and-item-templates.md)
- [如何：将向导与项目模板结合使用](../extensibility/how-to-use-wizards-with-project-templates.md)
