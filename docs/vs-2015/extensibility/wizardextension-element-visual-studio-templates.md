---
title: WizardExtension 元素 （Visual Studio 模板） |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#WizardExtension
helpviewer_keywords:
- WizardExtension element [Visual Studio Templates]
- <WizardExtension> element [Visual Studio Templates]
ms.assetid: d54b01c1-50f5-4b65-828c-686e2321cc8c
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 69e35d4bebf7a16a1429be674ba3533b4f082b05
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68201916"
---
# <a name="wizardextension-element-visual-studio-templates"></a>WizardExtension 元素（Visual Studio 模板）
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

包含用于自定义模板向导的注册元素。  
  
 \<VSTemplate >  
 ...  
 \<WizardExtension>  
  
## <a name="syntax"></a>语法  
  
```  
<WizardExtension>  
    <Assembly>... </Assembly>  
    <FullClassName>... </FullClassName>  
</WizardExtension>  
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 以下各部分描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
 无。  
  
### <a name="child-elements"></a>子元素  
  
|元素|描述|  
|-------------|-----------------|  
|[Assembly](../extensibility/assembly-element-visual-studio-template-wizard-extension.md)|必需的元素。<br /><br /> 指定的名称或显示在全局程序集缓存中的程序集的强名称。 必须有至少一个`Assembly`中的元素`WizardExtension`元素。|  
|[FullClassName](../extensibility/fullclassname-element-visual-studio-template-wizard-extension.md)|必需的元素。<br /><br /> 实现的类的完全限定的名称`IWizard`接口。 必须有至少一个`FullClassName`中的元素`WizardExtension`元素。|  
  
### <a name="parent-elements"></a>父元素  
  
|元素|描述|  
|-------------|-----------------|  
|[VSTemplate](../extensibility/vstemplate-element-visual-studio-templates.md)|包含项目模板、 项模板或初学者工具包的所有元数据。|  
  
## <a name="remarks"></a>备注  
 `WizardExtension` 是 `VSTemplate` 的可选子元素。  
  
## <a name="example"></a>示例  
 下面的示例演示的标准项目模板的元数据[!INCLUDE[csprcs](../includes/csprcs-md.md)]Windows 应用程序。  
  
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
 [Visual Studio 模板架构参考](../extensibility/visual-studio-template-schema-reference.md)   
 [创建项目和项模板](../ide/creating-project-and-item-templates.md)   
 [如何：使用向导来处理项目模板](../extensibility/how-to-use-wizards-with-project-templates.md)
