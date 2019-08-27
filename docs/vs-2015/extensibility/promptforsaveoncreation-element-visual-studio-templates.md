---
title: PromptForSaveOnCreation 元素 （Visual Studio 模板） |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#PromptForSaveOnCreation
helpviewer_keywords:
- PromptForSaveOnCreation element [Visual Studio project templates]
ms.assetid: 75174674-0c3c-4b57-b2fd-6ea8e817b67d
caps.latest.revision: 19
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: a523190a9e5c143667355c222e0fbe9441cc231a
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65675361"
---
# <a name="promptforsaveoncreation-element-visual-studio-templates"></a>PromptForSaveOnCreation 元素（Visual Studio 模板）
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

指定是否提示用户输入保存位置通过项目**新的项目**对话框中创建项目时。 如果此元素设置为`true`，然后提示用户输入保存位置; 如果`false`，则不会提示。 （即，创建一个临时项目。）  
  
 \<VSTemplate>  
 \<TemplateData>  
 \<PromptForSaveOnCreation>  
  
## <a name="syntax"></a>语法  
  
```  
<PromptForSaveOnCreation> true/false </PromptForSaveOnCreation>  
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
  
 文本必须是`true`或`false`， `true` ，该值指示将提示用户输入保存位置创建新项目时。  
  
## <a name="remarks"></a>备注  
 `PromptForSaveOnCreation` 是可选元素。 默认值为 `false`。  
  
 临时项目是指那些可以创建和修改而不在磁盘上保存该项目的内容。 有关详细信息，请参阅[NIB 临时项目](https://msdn.microsoft.com/9cf1944c-7045-44cc-8701-7b0eb4099f2b)。  
  
## <a name="example"></a>示例  
 下面的示例设置的值`PromptForSaveOnCreation`等于`false`，它指定允许为创建为临时项目的项目。  
  
```  
<VSTemplate Type="Project" Version="3.0.0"  
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">  
    <TemplateData>  
        <Name>My template</Name>  
        <Description>A basic template</Description>  
        <Icon>TemplateIcon.ico</Icon>  
        <ProjectType>CSharp</ProjectType>  
        <PromptForSaveOnCreation>false</PromptForSaveOnCreation>  
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
</VSTemplate>  
```  
  
## <a name="see-also"></a>请参阅  
 [Visual Studio 模板架构参考](../extensibility/visual-studio-template-schema-reference.md)   
 [创建项目和项模板](../ide/creating-project-and-item-templates.md)
