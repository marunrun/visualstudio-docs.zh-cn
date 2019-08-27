---
title: LocationField 元素 （Visual Studio 项目模板） |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#LocationField
helpviewer_keywords:
- LocationField element [Visual Studio project templates]
ms.assetid: 6aaaa155-6ce0-4f7f-aa50-8d63d7a7c992
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: b28fe0e696b23724758bd877b6031287290f879e
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68194461"
---
# <a name="locationfield-element-visual-studio-project-templates"></a>LocationField 元素（Visual Studio 项目模板）
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

指定是否**位置**文本框中**新项目**启用、 禁用或隐藏项目模板对话框的。  
  
 \<VSTemplate >  
 \<TemplateData >  
 \<LocationField >  
  
## <a name="syntax"></a>语法  
  
```  
<LocationField> Enabled/Disabled/Hidden </LocationField>  
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
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|必需的元素。<br /><br /> 将此模板分类并定义中的显示方式**新的项目**。|  
  
## <a name="text-value"></a>文本值  
 需要一个文本值。  
  
 有效的文本的值为：  
  
- `Enabled`指定将**位置**的框**新项目**对话框的已启用。  
  
- `Disabled`指定将**位置**的框**新项目**对话框框处于禁用状态。  
  
- `Hidden`指定将**位置**的框**新项目**对话框处于隐藏状态。  
  
## <a name="remarks"></a>备注  
 默认值为 `Enabled`。  
  
 **位置**文本框中**新项目**对话框使用户能够更改默认目录来保存新项目。  
  
 中指定的值`Location`元素仅遵循所对话框中，如果基础项目系统支持它。  
  
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
        <LocationField>Disabled</LocationField>  
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
