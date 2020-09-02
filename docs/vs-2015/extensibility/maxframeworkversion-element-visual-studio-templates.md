---
title: " (Visual Studio 模板) 的 MaxFrameworkVersion 元素 |Microsoft Docs"
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- <MaxFrameworkVersion> Element (Visual Studio Templates)
- MaxFrameworkVersion Element (Visual Studio Templates)
ms.assetid: f732a9d3-fc29-405b-9298-01ea83fc58b8
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 4a1c27e42574429dbb6b2eaeb140db484bf29db5
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68194332"
---
# <a name="maxframeworkversion-element-visual-studio-templates"></a>MaxFrameworkVersion 元素（Visual Studio 模板）
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

指定模板所需的 .NET Framework 的最高版本。 它根据在 "**添加新项目**" 对话框的 "**目标框架版本**" 框中选择的值，确定模板是否显示在 "**添加新项目**" 对话框的 "**模板**" 部分中。  
  
 \<VSTemplate>  
 \<MaxFrameworkVersion>  
  
## <a name="syntax"></a>语法  
  
```  
<MaxFrameworkVersion> ... </MaxFrameworkVersion>  
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
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|必需的元素。<br /><br /> 将模板分类并定义它在 " **新建项目** " 或 " **添加新项** " 对话框中的显示方式。|  
  
## <a name="text-value"></a>文本值  
 需要一个文本值。  
  
 文本必须是模板允许的 .NET Framework 的最高版本号。  
  
## <a name="remarks"></a>备注  
 `MaxFrameworkVersion` 是可选元素。 .Vstemplate 文件的部分中的元素 `TemplateData` 充当 "**添加新项目**" 对话框的 "**模板**" 部分的筛选器。 仅 `MaxFrameworkVersion` 根据在 "**添加新项目**" 对话框的 "**目标框架版本**" 框中选择的值显示其 .NET Framework 要求小于元素值的模板。 `MaxFrameworkVersion`除非需要，否则应省略元素，因此，如果模板与较新版本的 .NET Framework 一起使用，则不会无意间显示模板。  
  
## <a name="example"></a>示例  
 下面的示例演示标准类模板的元数据 [!INCLUDE[csprcs](../includes/csprcs-md.md)] 。  
  
```  
<VSTemplate Type="Item" Version="3.0.0"  
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">  
    <TemplateData>  
        <Name>MyClass</Name>  
        <Description>My custom C# class template.</Description>  
        <Icon>Icon.ico</Icon>  
        <ProjectType>CSharp</ProjectType>  
        <MaxFrameworkVersion>3.5</MaxFrameworkVersion>  
        <DefaultName>MyClass</DefaultName>  
    </TemplateData>  
    <TemplateContent>  
        <ProjectItem>MyClass.cs</ProjectItem>  
    </TemplateContent>  
</VSTemplate>  
```  
  
 在此示例中，模板所需的 .NET Framework 的最高版本 `MaxFrameworkVersion` 为3.5。 仅当在 "**添加新项目**" 对话框的 "**目标框架版本**" 框中选择 "3.0" 或 "3.5" 时，才会显示上述模板。  
  
## <a name="see-also"></a>另请参阅  
 [Visual Studio 模板架构参考](../extensibility/visual-studio-template-schema-reference.md)   
 [创建项目和项模板](../ide/creating-project-and-item-templates.md)
