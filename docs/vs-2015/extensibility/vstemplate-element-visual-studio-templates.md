---
title: " (Visual Studio 模板) 的 .Vstemplate 元素 |Microsoft Docs"
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#VSTemplate
helpviewer_keywords:
- VSTemplate element [Visual Studio project templates]
ms.assetid: f8ac561b-3b0b-4246-9ec9-118d2447e9a9
caps.latest.revision: 21
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: e8219f12eed091858a43c2bd5092b8b06f8320bc
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62422884"
---
# <a name="vstemplate-element-visual-studio-templates"></a>VSTemplate 元素（Visual Studio 模板）
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

包含有关项目模板、项模板或初学者工具包的所有元数据。  
  
## <a name="syntax"></a>语法  
  
```  
<VSTemplate Type="TemplateType" Version="x.x.x">  
    <TemplateData>    </TemplateData>  
    <TemplateContent>    </TemplateContent>  
    ...  
</VSTemplate>  
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|特性|说明|  
|---------------|-----------------|  
|`Type`|将模板标识为项目模板或项模板。 此属性的值可以是 `Project` 或 `Item` 。|  
|`Version`|指定模板的版本号。 和中的模板的 [!INCLUDE[vs_dev10_long](../includes/vs-dev10-long-md.md)] [!INCLUDE[vs_dev11_long](../includes/vs-dev11-long-md.md)] `Version` 属性值为 `3.0.0` 。|  
  
### <a name="child-elements"></a>子元素  
  
|元素|描述|  
|-------------|-----------------|  
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|必需的元素。<br /><br /> 指定对模板进行分类的数据，并定义它在 " **新建项目** " 或 " **添加新项** " 对话框中的显示方式。|  
|[TemplateContent](../extensibility/templatecontent-element-visual-studio-templates.md)|必需的元素。<br /><br /> 指定模板的内容。|  
|[WizardExtension](../extensibility/wizardextension-element-visual-studio-templates.md)|可选元素。|  
|[WizardData](../extensibility/wizarddata-element-visual-studio-templates.md)|可选元素。|  
  
### <a name="parent-elements"></a>父元素  
 无。  
  
## <a name="remarks"></a>备注  
 `VSTemplate`元素是 .vstemplate 文件的根元素。  
  
## <a name="example"></a>示例  
 下面的示例演示应用程序的项目模板的元数据 [!INCLUDE[csprcs](../includes/csprcs-md.md)] 。  
  
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
</VSTemplate>  
```  
  
## <a name="see-also"></a>另请参阅  
 [Visual Studio 模板架构参考](../extensibility/visual-studio-template-schema-reference.md)   
 [创建项目和项模板](../ide/creating-project-and-item-templates.md)
