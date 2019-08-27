---
title: TemplateContent 元素 （Visual Studio 模板） |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#TemplateContent
helpviewer_keywords:
- TemplateContent element [Visual Studio project templates]
ms.assetid: 90ae401c-b294-49ac-98da-e0d274f5bebb
caps.latest.revision: 15
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: fe87bff62c1044442b579664fb789f918a2e6c2d
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68186461"
---
# <a name="templatecontent-element-visual-studio-templates"></a>TemplateContent 元素（Visual Studio 模板）
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

指定模板的内容。  
  
 \<VSTemplate >  
 \<TemplateContent>  
  
## <a name="syntax"></a>语法  
  
```  
<TemplateContent>  
    ...  
</TemplateContent>  
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|特性|描述|  
|---------------|-----------------|  
|[BuildOnLoad](../extensibility/buildprojectonload-visual-studio-templates.md)|指定是否生成解决方案，从模板创建项目。|  
  
### <a name="child-elements"></a>子元素  
  
|元素|描述|  
|-------------|-----------------|  
|[ProjectCollection](../extensibility/projectcollection-element-visual-studio-templates.md)|可选元素。<br /><br /> 指定多项目模板的组织和内容。|  
|[Project](../extensibility/project-element-visual-studio-templates.md)|可选元素。<br /><br /> 指定要添加到项目文件或目录。|  
|[参考资料](../extensibility/references-element-visual-studio-templates.md)|可选元素。<br /><br /> 指定所需的项模板的程序集引用。|  
|[ProjectItem](../extensibility/projectitem-element-visual-studio-item-templates.md)|可选元素。<br /><br /> 指定模板中包含的文件。|  
|[CustomParameters](../extensibility/customparameters-element-visual-studio-templates.md)|可选元素。<br /><br /> 指定从模板创建项目或项时要使用的所有自定义参数。|  
  
### <a name="parent-elements"></a>父元素  
  
|元素|描述|  
|-------------|-----------------|  
|[VSTemplate](../extensibility/vstemplate-element-visual-studio-templates.md)|必需的元素。<br /><br /> 包含项目模板、 项模板或初学者工具包的所有元数据。|  
  
## <a name="remarks"></a>备注  
 `TemplateContent` 是必需的元素。  
  
## <a name="example"></a>示例  
 下面的示例演示用于的项目模板的元数据[!INCLUDE[csprcs](../includes/csprcs-md.md)]应用程序。  
  
```  
<VSTemplate Type="Project" Version="3.0.0"  
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">  
    <TemplateData>  
        <Name>My template</Name>  
        <Description>A basic starter kit</Description>  
        <Icon>TemplateIcon.ico</Icon>  
        <ProjectType>CSharp</ProjectType>  
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
 [Visual Studio 模板架构参考](../extensibility/visual-studio-template-schema-reference.md)   
 [创建项目和项模板](../ide/creating-project-and-item-templates.md)
