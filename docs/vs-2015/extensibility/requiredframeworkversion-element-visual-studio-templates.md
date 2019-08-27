---
title: RequiredFrameworkVersion 元素 （Visual Studio 模板） |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- <RequiredFrameworkVersion> (Visual Studio Templates)
- RequiredFrameworkVersion (Visual Studio Templates)
ms.assetid: 08a4f609-51a5-4723-b89f-99277fb18871
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: ce312d7951f4c1be720604c006f9afcd63f364d3
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68163652"
---
# <a name="requiredframeworkversion-element-visual-studio-templates"></a>RequiredFrameworkVersion 元素（Visual Studio 模板）
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

指定模板所需的最低.NET Framework 版本。架构层次结构。  
  
 \<VSTemplate >  
 \<TemplateData >  
 \<RequiredFrameworkVersion>  
  
## <a name="syntax"></a>语法  
  
```  
<RequiredFrameworkVersion> .... </RequiredFrameworkVersion>  
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
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|必需的元素。<br /><br /> 此模板分类并定义如何显示在**新的项目**或**添加新项**对话框。|  
  
## <a name="text-value"></a>文本值  
 需要一个文本值。  
  
 文本必须为.NET Framework 所需的模板的最低版本号。  
  
## <a name="remarks"></a>备注  
 `RequiredFrameworkVersion` 是可选元素。 如果该模板仅支持特定的最低版本和更高版本，如果任何.NET Framework，请使用此元素。  
  
## <a name="see-also"></a>请参阅  
 [Visual Studio 模板架构参考](../extensibility/visual-studio-template-schema-reference.md)   
 [创建项目和项模板](../ide/creating-project-and-item-templates.md)   
 [面向特定的 .NET Framework 版本](../ide/targeting-a-specific-dotnet-framework-version.md)
