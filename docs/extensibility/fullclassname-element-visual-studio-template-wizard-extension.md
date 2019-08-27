---
title: FullClassName 元素 （VS 模板向导扩展）
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: conceptual
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#FullClassName
helpviewer_keywords:
- FullClassName element [Visual Studio project template]
ms.assetid: 651e1010-d529-4856-85ff-c77ceca5d2ed
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 63b7e480944e8f5519db1c9cfd123c07a0cf6208
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66342629"
---
# <a name="fullclassname-element-visual-studio-template-wizard-extension"></a>FullClassName 元素 （Visual Studio 模板向导扩展）
实现的类的完全限定的名称`IWizard`接口。

 \<VSTemplate > \<WizardExtension >...\<FullClassName>

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

|元素|描述|
|-------------|-----------------|
|[WizardExtension](../extensibility/wizardextension-element-visual-studio-templates.md)|包含用于自定义模板向导的注册元素。|

## <a name="text-value"></a>文本值
 需要一个文本值。

 此文本指定实现的类`IWizard`接口。 指定的类必须存在于由指定的程序集[程序集](../extensibility/assembly-element-visual-studio-template-wizard-extension.md)元素。

## <a name="remarks"></a>备注
 `FullClassName` 是 `WizardExtension` 的必需子元素。

## <a name="example"></a>示例
 下面的示例演示的标准项目模板的元数据[!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)]Windows 应用程序。

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
- [如何：使用向导来处理项目模板](../extensibility/how-to-use-wizards-with-project-templates.md)