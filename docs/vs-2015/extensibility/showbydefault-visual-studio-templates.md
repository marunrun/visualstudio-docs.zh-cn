---
title: ShowByDefault （Visual Studio 模板） |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#ShowByDefault
helpviewer_keywords:
- <ShowByDefault> element [Visual Studio Templates]
- ShowByDefault element [Visual Studio Templates]
ms.assetid: 7be783f6-0ef6-42bc-924a-df9a2eba7781
caps.latest.revision: 8
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 98779743f1e7c68f579334d74d3651357c6ee0b4
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68184131"
---
# <a name="showbydefault-visual-studio-templates"></a>ShowByDefault（Visual Studio 模板）
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

如果`false`，指定将仅显示该模板在指定[TemplateGroupID](../extensibility/templategroupid-element-visual-studio-templates.md)。  
  
 \<VSTemplate >  
 \<TemplateData >  
 \<ShowByDefault>  
  
## <a name="syntax"></a>语法  
  
```  
<ShowByDefault> true/false </ShowByDefault>  
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
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|将此模板分类并定义此模板在 **“新建项目”** 或 **“添加新项”** 对话框中的显示方式。|  
  
## <a name="text-value"></a>文本值  
 需要一个文本值。  
  
 文本必须为 `true` 或 `false`。 如果为 true，则指定将对所有项目类型显示该模板。 如果为 false，则该将仅在指定的 `TemplateGroupID` 下显示该模板。  
  
## <a name="remarks"></a>备注  
 `ShowByDefault` 是可选元素。 默认值为 `true`。  
  
## <a name="example"></a>示例  
 以下示例阐释 [!INCLUDE[csprcs](../includes/csprcs-md.md)] 模板的元数据。  
  
```  
<VSTemplate Type="Project" Version="3.0.0"  
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">  
    <TemplateData>  
        <Name>My template</Name>  
        <Description>A basic template</Description>  
        <Icon>TemplateIcon.ico</Icon>  
        <ProjectType>CSharp</ProjectType>  
        <ShowByDefault>false</ShowByDefault>  
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
 [创建项目和项模板](../ide/creating-project-and-item-templates.md)   
 [Visual Studio 模板架构参考](../extensibility/visual-studio-template-schema-reference.md)   
 [TemplateGroupID 元素（Visual Studio 模板）](../extensibility/templategroupid-element-visual-studio-templates.md)
