---
title: " (Visual Studio 模板) 的 RequiredPlatformVersion 元素 |Microsoft Docs"
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
ms.assetid: 6f0e4986-3157-4bba-aed3-c28413ebe976
caps.latest.revision: 7
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 2e5ba8cfef6674b5603cf03c73619f686338af3c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68159285"
---
# <a name="requiredplatformversion-element-visual-studio-templates"></a>RequiredPlatformVersion 元素（Visual Studio 模板）
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

指定项目模板正常运行所需的操作系统的最低版本。 此元素用于创建应用程序的项目模板 [!INCLUDE[win8_appname_long](../includes/win8-appname-long-md.md)] 。  
  
 `RequiredPlatformVersion`该值与操作系统的版本直接进行比较。 如果 `RequiredPlatformVersion` 高于操作系统版本，则该模板不会显示在 " **新建项目** " 对话框中。 若要为 [!INCLUDE[win8](../includes/win8-md.md)] 或更高版本指定模板，请将设置 `RequiredPlatformVersion` 为6.2.0。 若要为 [!INCLUDE[win81](../includes/win81-md.md)] 或更高版本指定模板，请将 RequiredPlatformVersion 设置为6.3.0。  
  
 指定 `RequiredPlatformVersion` = 8 的模板与以前的客户 [!INCLUDE[win8_appname_long](../includes/win8-appname-long-md.md)] 模板兼容。  
  
 VSTemplate  
TemplateData  
.....TargetPlatformName  
RequiredPlatformVersion  
  
## <a name="syntax"></a>语法  
  
```xml  
<RequiredPlatformVersion> OperatingSystem </RequiredPlatformVersion>  
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 无。  
  
### <a name="attributes"></a>特性  
 无。  
  
### <a name="child-elements"></a>子元素  
 无。  
  
### <a name="parent-elements"></a>父元素  
  
|元素|说明|  
|-------------|-----------------|  
|[TemplatePlatformName](../extensibility/templatedata-element-visual-studio-templates.md)|指定项目模板面向的平台。|  
  
## <a name="text-value"></a>文本值  
 需要一个文本值。  
  
## <a name="remarks"></a>备注  
 此文本指定模板所需的最低操作系统版本。  
  
## <a name="example"></a>示例  
 此示例指定项目模板面向 [!INCLUDE[win8](../includes/win8-md.md)] 或更高版本。  
  
```xml  
<VSTemplate Type="Project" Version="3.0.0"    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">  
    <TemplateData>  
        <TargetPlatformName>Windows</TargetPlatformName>  
            <RequiredPlatformVersion>6.3.0</RequiredPlatformVersion>  
  
    </TemplateData>  
    <TemplateContent>  
  
    </TemplateContent>  
</VSTemplate>  
```  
  
## <a name="see-also"></a>另请参阅  
 [ (Visual Studio 模板的 TargetPlatformName 元素) ](../extensibility/targetplatformname-element-visual-studio-templates.md)   
 [创建项目和项模板](../ide/creating-project-and-item-templates.md)   
 [Visual Studio 模板架构参考](../extensibility/visual-studio-template-schema-reference.md)
