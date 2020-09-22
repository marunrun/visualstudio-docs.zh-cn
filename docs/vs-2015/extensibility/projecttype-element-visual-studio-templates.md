---
title: " (Visual Studio 模板) 的 ProjectType 元素 |Microsoft Docs"
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#ProjectType
helpviewer_keywords:
- ProjectType element [Visual Studio project templates]
ms.assetid: ccf9d83f-c7f3-49c7-a31f-e1f22bec004c
caps.latest.revision: 20
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: b01dd370fe5e3d7a5207363c5ab7ec4f2a0254c5
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "90840368"
---
# <a name="projecttype-element-visual-studio-templates"></a>ProjectType 元素（Visual Studio 模板）
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

对项目模板进行分类，使其显示在 " **新建项目** " 或 " **添加新项** " 对话框中的指定组下。  
  
> [!WARNING]
> 从 Visual Studio 2012 开始，c + + 支持项目模板。 Visual Studio 2010 及更早版本中不支持 c + +。  
  
 \<VSTemplate>  
 \<TemplateData>  
 \<ProjectType>  
  
## <a name="syntax"></a>语法  
  
```  
<ProjectType> CSharp/VisualBasic/VC/Web </ProjectType>  
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
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|将此模板分类并定义此模板在 **“新建项目”** 或 **“添加新项”** 对话框中的显示方式。|  
  
## <a name="text-value"></a>文本值  
 需要一个文本值。  
  
 此值指定模板将创建的项目类型，并且必须包含以下值之一：  
  
- `CSharp`：指定模板创建 [!INCLUDE[csprcs](../includes/csprcs-md.md)] 项目或项。  
  
- `VisualBasic`：指定模板创建 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] 项目或项。  
  
- `Web`：指定模板创建 Web 项目或项。 如果 `ProjectType` 元素包含此值，则会在 ProjectSubType 元素中定义项目或项的语言 [ (Visual Studio 模板) ](../extensibility/projectsubtype-element-visual-studio-templates.md)。  
  
## <a name="remarks"></a>备注  
 `ProjectType` 是 `TemplateData` 的必需子元素。  
  
 元素的值 `ProjectType` 指定模板位于 " **新建项目** " 或 " **添加新项** " 对话框中的位置。 例如， `ProjectType` 值为的模板 `CSharp` 会出现在 "**新建项目**" 对话框中的 " **Visual c #** " 节点下。  
  
 可以使用 [ProjectSubType](../extensibility/projectsubtype-element-visual-studio-templates.md) 元素指定模板子类型。  
  
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
  
## <a name="see-also"></a>另请参阅  
 [Visual Studio 模板架构参考](../extensibility/visual-studio-template-schema-reference.md)   
 [创建项目和项模板](../ide/creating-project-and-item-templates.md)   
 [ProjectSubType 元素（Visual Studio 模板）](../extensibility/projectsubtype-element-visual-studio-templates.md)
