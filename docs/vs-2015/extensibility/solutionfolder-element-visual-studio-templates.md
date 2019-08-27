---
title: SolutionFolder 元素 （Visual Studio 模板） |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#SolutionFolder
helpviewer_keywords:
- <SolutionFolder> element [Visual Studio Templates]
- SolutionFolder element [Visual Studio Templates]
ms.assetid: 963f0398-fb50-4d8e-879d-d48f8b7c6d80
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 84d0c1765a14f60363b71fcdec182d448cb4f112
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68205541"
---
# <a name="solutionfolder-element-visual-studio-templates"></a>SolutionFolder 元素（Visual Studio 模板）
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

对多项目模板中的项目进行分组。  
  
 \<VSTemplate >  
 \<TemplateContent>  
 \<ProjectCollection>  
 \<SolutionFolder>  
  
## <a name="syntax"></a>语法  
  
```  
<SolutionFolder Name="DirectoryName">  
    ...  
</SolutionFolder>  
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 以下各部分描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|特性|描述|  
|---------------|-----------------|  
|`Name`|必需的特性。<br /><br /> 解决方案文件夹的名称。|  
  
### <a name="child-elements"></a>子元素  
  
|元素|描述|  
|-------------|-----------------|  
|[ProjectTemplateLink](../extensibility/projecttemplatelink-element-visual-studio-templates.md)|可选元素。<br /><br /> 指定多项目模板中一个项目的 .vstemplate 文件的路径。|  
|`SolutionFolder`|可选元素。<br /><br /> 对多项目模板中的项目进行分组。|  
  
### <a name="parent-elements"></a>父元素  
  
|元素|描述|  
|-------------|-----------------|  
|[ProjectCollection](../extensibility/projectcollection-element-visual-studio-templates.md)|指定多项目模板的组织和内容。|  
|`SolutionFolder`|对多项目模板中的项目进行分组。|  
  
## <a name="remarks"></a>备注  
 多项目模板用作两个或多个项目的容器。 `SolutionFolder`元素用于将模板中的项目组织到组。 通过`SolutionFolder`元素指定的文件夹被创建为[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]的项目中的解决方案文件夹。 多项目模板的详细信息，请参阅[如何：创建多项目模板](../ide/how-to-create-multi-project-templates.md)。  
  
## <a name="example"></a>示例  
 此示例使用`SolutionFolder`元素，可以将多项目模板划分为两个组，`Math Classes`和`Graphics Classes`。 该模板包含四个项目，其中两个位于每个解决方案文件夹中。  
  
```  
<VSTemplate Version="3.0.0" Type="ProjectGroup"  
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">  
    <TemplateData>  
        <Name>Multi-Project Template Sample</Name>  
        <Description>An example of a multi-project template</Description>  
        <Icon>Icon.ico</Icon>  
        <ProjectType>VisualBasic</ProjectType>  
    </TemplateData>  
    <TemplateContent>  
        <ProjectCollection>  
            <SolutionFolder Name="Math Classes">  
                <ProjectTemplateLink ProjectName="MathClassLib1">  
                    MathClassLib1\MyTemplate.vstemplate  
                </ProjectTemplateLink>  
                <ProjectTemplateLink ProjectName="MathClassLib2">  
                    MathClassLib2\MyTemplate.vstemplate  
                </ProjectTemplateLink>  
            </SolutionFolder>  
            <SolutionFolder Name="Graphics Classes">  
                <ProjectTemplateLink ProjectName="GraphicsClassLib1">  
                    GraphicsClassLib1\MyTemplate.vstemplate  
                </ProjectTemplateLink>  
                <ProjectTemplateLink ProjectName="GraphicsClassLib2">  
                    GraphicsClassLib2\MyTemplate.vstemplate  
                </ProjectTemplateLink>  
            </SolutionFolder>  
        </ProjectCollection>  
    </TemplateContent>  
</VSTemplate>  
```  
  
## <a name="see-also"></a>请参阅  
 [Visual Studio 模板架构参考](../extensibility/visual-studio-template-schema-reference.md)   
 [创建项目和项模板](../ide/creating-project-and-item-templates.md)   
 [如何：创建多项目模板](../ide/how-to-create-multi-project-templates.md)
