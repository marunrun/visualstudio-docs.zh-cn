---
title: ProjectExtensions 元素 (MSBuild) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: conceptual
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#ProjectExtensions
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- <ProjectExtensions> element [MSBuild]
- ProjectExtensions element [MSBuild]
ms.assetid: f95f312f-ff92-41eb-9469-ad99e236a307
caps.latest.revision: 21
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 0afc4f73ed287f753acf87bd0b112e6f5303e996
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62551244"
---
# <a name="projectextensions-element-msbuild"></a>ProjectExtensions 元素 (MSBuild)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

允许 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] 项目文件包含非 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] 信息。 `ProjectExtensions` 元素中的所有内容都将被 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] 忽略。  
  
 \<Project>  
 \<ProjectExtensions>  
  
## <a name="syntax"></a>语法  
  
```  
<ProjectExtensions>  
    Non-MSBuild information to include in file.  
</ProjectExtensions>  
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
 无  
  
### <a name="child-elements"></a>子元素  
 无  
  
### <a name="parent-elements"></a>父元素  
  
|元素|描述|  
|-------------|-----------------|  
|[Project](../msbuild/project-element-msbuild.md)|[!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] 项目文件必需的根元素。|  
  
## <a name="remarks"></a>备注  
 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] 项目中可能只会用到一个 `ProjectExtensions` 元素。  
  
## <a name="example"></a>示例  
 以下示例显示了存储在 `ProjectExtensions` 元素中的集成开发环境的信息。  
  
```  
<ProjectExtensions>  
    <VSIDE>  
        <External>  
            <!--  
            Raw XML passed to the IDE by an external source  
            -->  
        </External>  
    </VSIDE>  
</ProjectExtensions>  
```  
  
## <a name="see-also"></a>另请参阅  
 [项目文件架构参考](../msbuild/msbuild-project-file-schema-reference.md)  
 [MSBuild](msbuild.md)
