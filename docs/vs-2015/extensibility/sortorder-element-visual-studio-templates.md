---
title: SortOrder 元素 （Visual Studio 模板） |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#SortOrder
helpviewer_keywords:
- SortOrder element [Visual Studio Templates]
- <SortOrder> element [Visual Studio Templates]
ms.assetid: 151932c1-f08a-4f78-a8d0-bd2f32211a9c
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 825ec785a83cae0aaa8a31ae1375e956228b634e
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68205514"
---
# <a name="sortorder-element-visual-studio-templates"></a>SortOrder 元素（Visual Studio 模板）
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

指定一个值，用于排列在同一类别中的其他模板之间的模板中显示该值**新的项目**或**添加新项**对话框。  
  
 \<VSTemplate >  
 \<TemplateData >  
 \<SortOrder>  
  
## <a name="syntax"></a>语法  
  
```  
<SortOrder> ... </SortOrder>  
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
 需要一个文本值。  
  
 `integer`表示排序顺序值。  
  
## <a name="remarks"></a>备注  
 `SortOrder` 是可选元素。 默认值为 100，并且所有值都必须为 10 的倍数。  
  
 `SortOrder`元素忽略为用户创建的模板。 所有用户创建的模板进行按字母顺序都排序。  
  
 中将显示具有较低的排序顺序值的模板**新的项目**或**新添加项**之前具有高排序顺序值的模板对话框的。  
  
## <a name="example"></a>示例  
 下面的示例演示一种标准的元数据[!INCLUDE[csprcs](../includes/csprcs-md.md)]类模板。  
  
```  
<VSTemplate Type="Item" Version="3.0.0"  
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">  
    <TemplateData>  
        <Name>MyClass</Name>  
        <Description>My custom C# class template.</Description>  
        <Icon>Icon.ico</Icon>  
        <ProjectType>CSharp</ProjectType>  
        <SortOrder>290</SortOrder>  
        <DefaultName>MyClass</DefaultName>  
    </TemplateData>  
    <TemplateContent>  
        <ProjectItem>MyClass.cs</ProjectItem>  
    </TemplateContent>  
</VSTemplate>  
```  
  
 在此示例中，`SortOrder`元素是相对较高。 很可能其他[!INCLUDE[csprcs](../includes/csprcs-md.md)]项模板将具有`SortOrder`值低于`290`，并将此模板前**新项**对话框。  
  
## <a name="see-also"></a>请参阅  
 [Visual Studio 模板架构参考](../extensibility/visual-studio-template-schema-reference.md)   
 [创建项目和项模板](../ide/creating-project-and-item-templates.md)
