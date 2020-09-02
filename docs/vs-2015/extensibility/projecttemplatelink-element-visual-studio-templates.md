---
title: " (Visual Studio 模板) 的 ProjectTemplateLink 元素 |Microsoft Docs"
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#ProjectTemplateLink
helpviewer_keywords:
- <ProjectTemplateLink> element [Visual Studio Templates]
- ProjectTemplateLink element [Visual Studio Templates]
ms.assetid: b0449111-8b48-45a1-a031-ea24b765e969
caps.latest.revision: 16
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: a6ee9f5d4a162f994cfea4fb3fe620599c1627b3
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65681319"
---
# <a name="projecttemplatelink-element-visual-studio-templates"></a>ProjectTemplateLink 元素（Visual Studio 模板）
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

指定多项目模板中一个项目的 .vstemplate 文件的路径。  
  
 \<VSTemplate>  
 \<TemplateContent>  
 \<ProjectCollection>  
 \<ProjectTemplateLink>  
- 或 -  
\<VSTemplate>  
 \<TemplateContent>  
 \<ProjectCollection>  
 \<SolutionFolder>  
 \<ProjectTemplateLink>  
  
## <a name="syntax"></a>语法  
  
```  
<ProjectTemplateLink ProjectName="Name">  
    PathToTemplateFile  
</ProjectTemplateLink>  
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 以下各部分描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>属性  
  
|特性|描述|  
|---------------|-----------------|  
|`ProjectName`|可选特性。<br /><br /> 指定多项目模板中每一个项目的名称。 " **新建项目** " 对话框无法为单个项目分配名称。|  
|`CopyParameters`|使主要组模板中的所有变量可复制到每个链接模板。<br /><br /> 链接模板中的参数具有前缀 `"$ext_*$"`。 例如，如果在父组模板中，参数的 `$projectname$` 值为 **ExampleProject1**，则当链接模板获得要执行的转换时，它将获取参数，该参数 `$ext_projectname$` 是 `$projectname$` 父组模板中参数的副本。<br /><br /> 这使链接模板能够共享一些只能在父组模板中方便地创建的公用参数。<br /><br /> 此特性为可选特性，未包含此特性时，它将自动默认为 `false`。<br /><br /> 在 Visual Studio 2013 Update 2 中引入。 若要引用正确的产品版本，请参阅 [在 VISUAL STUDIO 2013 SDK Update 2 中提供的引用程序集](https://msdn.microsoft.com/42b65c3e-e42b-4c39-98c8-bea285f25ffb)。|  
  
### <a name="child-elements"></a>子元素  
 无。  
  
### <a name="parent-elements"></a>父元素  
  
|元素|说明|  
|-------------|-----------------|  
|[ProjectCollection](../extensibility/projectcollection-element-visual-studio-templates.md)|指定多项目模板的组织和内容。|  
|[SolutionFolder](../extensibility/solutionfolder-element-visual-studio-templates.md)|对多项目模板中的项目进行分组。|  
  
## <a name="text-value"></a>文本值  
 需要一个文本值。  
  
 此文本指定模板的 .vstemplate 文件的路径。  
  
## <a name="remarks"></a>备注  
 多项目模板用作两个或多个项目的容器。 `ProjectTemplateLink` 元素用于指定模板中一个项目的 .vstemplate 文件的位置。 对于多项目模板中的每个项目，此模板的 .vstemplate 文件中都含有一个对应的 `ProjectTemplateLink` 元素。 有关多项目模板的详细信息，请参阅 [如何：创建多项目模板](../ide/how-to-create-multi-project-templates.md)。  
  
## <a name="example"></a>示例  
 此示例演示一个简单的多项目 .vstemplate 根文件。 在此示例中，模板包含两个项目：`My Windows Application` 和 `My Class Library`。 `ProjectName` 元素的 `ProjectTemplateLink` 特性可为 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 设置要分配给此项目的名称。 如果不存在 `ProjectName` 特性，则会使用 .vstemplate 文件的名称作为项目名称。  
  
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
            <ProjectTemplateLink ProjectName="My Windows Application">  
                WindowsApp\MyTemplate.vstemplate  
            </ProjectTemplateLink>  
            <ProjectTemplateLink ProjectName="My Class Library" CopyParameters="true">  
                ClassLib\MyTemplate.vstemplate  
            </ProjectTemplateLink>  
        </ProjectCollection>  
    </TemplateContent>  
</VSTemplate>  
```  
  
## <a name="see-also"></a>另请参阅  
 [Visual Studio 模板架构参考](../extensibility/visual-studio-template-schema-reference.md)   
 [创建项目和项模板](../ide/creating-project-and-item-templates.md)   
 [如何：创建多项目模板](../ide/how-to-create-multi-project-templates.md)
