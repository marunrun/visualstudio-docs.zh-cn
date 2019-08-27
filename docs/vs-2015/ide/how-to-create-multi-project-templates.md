---
title: 如何：创建多项目模板 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio templates, creating multi-project templates
- project templates, creating multi-project templates
- multi-project templates
ms.assetid: 8c7f7065-137e-40ad-868d-37e007270efd
caps.latest.revision: 19
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 394c9adf6794ae6e6c547a46e1fe469e0c642ba8
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68176689"
---
# <a name="how-to-create-multi-project-templates"></a>如何：创建多项目模板
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

多项目模板用作两个或多个项目的容器。 如果基于多项目模板的项目是从“新建项目”对话框中创建的，则模板中的每个项目都会添加到解决方案  。  
  
 多项目模板必须包括以下各项，并压缩为 .zip 文件：  
  
- 整个多项目模板的根 .vstemplate 文件。 此根 .vstemplate 文件包含“新建项目”对话框中显示的元数据，并指定查找此模板中项目的 .vstemplate 文件的位置  。 此文件必须位于 .zip 文件的根目录中。  
  
- 一个或多个文件夹，其中包含完整的项目模板所需的文件。 这包括项目的所有代码文件，以及项目的 .vstemplate 文件。  
  
  例如，具有两个项目的多项目模板 .zip 文件具有以下文件和目录：  
  
  MultiProjectTemplate.vstemplate  
  
  \Project1\Project1.vstemplate  
  
  \Project1\Project1.vbproj  
  
  \Project1\Class.vb  
  
  \Project2\Project2.vstemplate  
  
  \Project2\Project2.vbproj  
  
  \Project2\Class.vb  
  
  多项目模板的根 .vstemplate 文件不同于单项目模板，表现在以下方面：  
  
- `VSTemplate` 元素的 `Type` 属性包含值：`ProjectGroup`。 例如:  
  
  ```  
  <VSTemplate Version="2.0.0" Type="ProjectGroup"  
      xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">  
  ```  
  
- `TemplateContent` 元素包含的 `ProjectCollection` 元素具有一个或多个用于定义指向所含项目中 .vstemplate 文件的路径的 `ProjectTemplateLink` 元素。 例如：  
  
  ```  
  <TemplateContent>  
      <ProjectCollection>  
          <ProjectTemplateLink>  
              Project1\Project1.vstemplate  
          </ProjectTemplateLink>  
          <ProjectTemplateLink>  
              Project2\Project2.vstemplate  
          </ProjectTemplateLink>  
      </ProjectCollection>  
  </TemplateContent>  
  ```  
  
  多项目模板的行为也不同于常规模板。 多项目模板具有以下独特的特征：  
  
- 无法通过“新建项目”对话框向多项目模板中的各个项目分配名称  。 改为使用 `ProjectTemplateLink` 元素的 `ProjectName` 属性指定每个项目的名称。 有关详细信息，请参阅下一节的第一个示例。  
  
- 多项目模板可以包含以不同的语言编写的项目，但通过使用 `ProjectType` 元素，仅可将整个模板本身放置在一个类别中。  
  
### <a name="to-create-a-multi-project-template"></a>创建多项目模板  
  
1. 创建要在多项目模板中包括的项目。  
  
2. 创建每个项目的 .vstemplate 文件。 有关详细信息，请参阅[如何：创建项目模板](../ide/how-to-create-project-templates.md)。  
  
3. 创建根 .vstemplate 文件，使其包含多项目模板的元数据。 有关详细信息，请参阅下一节的第一个示例。  
  
4. 选择要在模板中包含的文件和文件夹，右键单击所选文件，单击“发送至”，然后单击“压缩的文件夹(zip 格式)”   。 这些文件和文件夹会压缩到一个 .zip 文件中。  
  
5. 将该 .zip 模板文件放入 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 项目模板目录。 默认情况下，此目录为 \My Documents\Visual Studio Version\Templates\ProjectTemplates\\  。  
  
## <a name="example"></a>示例  
 此示例演示一个基本的多项目根 .vstemplate 文件。 在此示例中，模板包含两个项目：`My Windows Application` 和 `My Class Library`。 `ProjectName` 元素的 `ProjectTemplateLink` 特性可为 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 设置要分配给此项目的名称。 如果不存在 `ProjectName` 特性，则会使用 .vstemplate 文件的名称作为项目名称。  
  
```  
<VSTemplate Version="2.0.0" Type="ProjectGroup"  
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
            <ProjectTemplateLink ProjectName="My Class Library">  
                ClassLib\MyTemplate.vstemplate  
            </ProjectTemplateLink>  
        </ProjectCollection>  
    </TemplateContent>  
</VSTemplate>  
```  
  
## <a name="example"></a>示例  
 此示例使用 `SolutionFolder` 元素，可以将项目划分为两个组，`Math Classes` 和 `Graphics Classes`。 该模板包含四个项目，其中两个位于每个解决方案文件夹中。  
  
```  
<VSTemplate Version="2.0.0" Type="ProjectGroup"  
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
 [创建项目和项模板](../ide/creating-project-and-item-templates.md)   
 [Visual Studio 模板架构参考](../extensibility/visual-studio-template-schema-reference.md)   
 [如何：创建项目模板](../ide/how-to-create-project-templates.md)   
 [Visual Studio 模板架构参考](../extensibility/visual-studio-template-schema-reference.md)   
 [SolutionFolder 元素（Visual Studio 模板）](../extensibility/solutionfolder-element-visual-studio-templates.md)   
 [ProjectTemplateLink 元素（Visual Studio 模板）](../extensibility/projecttemplatelink-element-visual-studio-templates.md)
