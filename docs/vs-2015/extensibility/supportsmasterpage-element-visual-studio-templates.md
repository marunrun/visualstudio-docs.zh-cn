---
title: SupportsMasterPage 元素 （Visual Studio 模板） |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#SupportsMasterPage
helpviewer_keywords:
- <SupportsMasterPage> element [Visual Studio Templates]
- SupportsMasterPage element [Visual Studio Templates]
ms.assetid: ce877a6a-9bba-4fd9-92fb-0a8dfec9e75b
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 051bde61132d286c3941a12c2e970aa2019fc0b7
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68160477"
---
# <a name="supportsmasterpage-element-visual-studio-templates"></a>SupportsMasterPage 元素（Visual Studio 模板）
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

指定是否**选择母版页**上启用复选框**添加新项**对话框。  
  
 \<VSTemplate >  
 \<TemplateData >  
 \<SupportsMasterPage>  
  
## <a name="syntax"></a>语法  
  
```  
<SupportsMasterPage> true/false </SupportsMasterPage>  
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
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|指定将此模板分类并定义中的显示方式的数据**新的项目**或**新项**对话框。|  
  
## <a name="text-value"></a>文本值  
 需要一个文本值。  
  
 文本必须是`true`或`false`，以指示是否**选择母版页**上启用复选框**添加新项**对话框。  
  
## <a name="remarks"></a>备注  
 `SupportsMasterPage` 是可选元素。 默认值为 `false`。  
  
 `SupportsMasterPage`元素功能仅适用于 Web 项目模板。  
  
## <a name="example"></a>示例  
 下面的示例演示包括对母版页的支持的 Web 项目的元数据。  
  
```  
<VSTemplate Version="3.0.0" Type="Project"  
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">>  
    <TemplateData>  
        <Name>MyWebProjecStarterKit</Name>  
        <Description>A simple Web template</Description>  
        <Icon>icon.ico</Icon>  
        <ProjectType>Web</ProjectType>  
        <ProjectSubType>CSharp</ProjectSubType>  
        <DefaultName>WebSite</DefaultName>  
        <SupportsMasterPage>true</SupportsMasterPage>  
    </TemplateData>  
    <TemplateContent>  
        <Project File="WebApplication.webproj">  
            <ProjectItem>icon.ico</ProjectItem>  
            <ProjectItem OpenInEditor="true">Default.aspx</ProjectItem>  
            <ProjectItem>Default.aspx.cs</ProjectItem>  
        </Project>  
    </TemplateContent>  
</VSTemplate>  
```  
  
## <a name="see-also"></a>请参阅  
 [Visual Studio 模板架构参考](../extensibility/visual-studio-template-schema-reference.md)   
 [创建项目和项模板](../ide/creating-project-and-item-templates.md)
