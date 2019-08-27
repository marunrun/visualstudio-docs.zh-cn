---
title: FullClassName 元素 （Visual Studio 模板向导扩展） |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#FullClassName
helpviewer_keywords:
- FullClassName element [Visual Studio project template]
ms.assetid: 651e1010-d529-4856-85ff-c77ceca5d2ed
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: c6cd466a41c61da929e9acc1619f384a3621f9c0
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68204330"
---
# <a name="fullclassname-element-visual-studio-template-wizard-extension"></a>FullClassName 元素（Visual Studio 模板向导扩展）
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

实现的类的完全限定的名称`IWizard`接口。  
  
 \<VSTemplate >  
 \<WizardExtension>  
 ...  
 \<FullClassName>  
  
## <a name="syntax"></a>语法  
  
```  
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
