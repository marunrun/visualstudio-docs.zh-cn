---
title: TemplateID 元素 （Visual Studio 模板） |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#TemplateID
helpviewer_keywords:
- <TemplateID> element [Visual Studio Templates]
- TemplateID element [Visual Studio Templates]
ms.assetid: 6ca24b4e-0325-4a9e-855e-0cbbe7361d8f
caps.latest.revision: 16
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: f1a52b360994c53eef69ceafa45828ec1020be16
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68186427"
---
# <a name="templateid-element-visual-studio-templates"></a>TemplateID 元素（Visual Studio 模板）
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

指定到项模板由一组分类的项模板的标识符[TemplateGroupID](../extensibility/templategroupid-element-visual-studio-templates.md)元素。  
  
 \<VSTemplate >  
 \<TemplateData >  
 \<TemplateID >  
  
## <a name="syntax"></a>语法  
  
```  
<TemplateID> ... </TemplateID>  
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
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|必需的元素。<br /><br /> 将此模板分类并定义此模板在 **“新建项目”** 或 **“添加新项”** 对话框中的显示方式。|  
  
## <a name="text-value"></a>文本值  
 一个`string`，表示到项模板由一组分类的项模板的标识符`TemplateGroupID`元素。  
  
## <a name="remarks"></a>备注  
 `TemplateID` 是可选元素。  
  
 如果.vstemplate 文件中省略`TemplateID`元素，则[名称](../extensibility/name-element-visual-studio-templates.md)元素用作模板标识符。  
  
 值`TemplateID`元素使用与项目系统注册 (HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\11.0\Projects\\) 中显示的筛选器模板**添加新项**对话框。  
  
## <a name="see-also"></a>请参阅  
 [Visual Studio 模板架构参考](../extensibility/visual-studio-template-schema-reference.md)   
 [创建项目和项模板](../ide/creating-project-and-item-templates.md)
