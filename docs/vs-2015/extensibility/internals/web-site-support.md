---
title: 网站支持 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- web site projects
ms.assetid: ce9f4266-bb64-4c09-be88-4bd6413f60d0
caps.latest.revision: 18
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: f1a96504783de466551c6fb9d055b95ba38df760
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65687692"
---
# <a name="web-site-support"></a>网站支持
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

网站项目系统是用于创建 Web 项目的项目系统。 Web 项目，然后创建 Web 应用程序。 网站项目为每个包含关联代码的网页生成一个可执行文件。 其他可执行文件是从/App_Code 文件夹中的源代码文件生成的。  
  
 网站项目系统是通过将模板和注册属性添加到现有项目系统创建的。 其中一个属性选择语言的 IntelliSense 提供程序。 当请求未缓存的智能网页时，IntelliSense 提供程序实现会处理引用并调用语言编译器。  
  
 用于编译网页的语言编译器必须注册到 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 。 您可以使用 Web.config 文件中的[ \<compiler> 元素](https://msdn.microsoft.com/library/7a151659-b803-4c27-b5ce-1c4aa0d5a823)来注册编译器，如以下示例中所示：  
  
```  
<system.codedom>  <compilers>    <compiler language="py;IronPython" extension=".py"       type="IronPython.CodeDom.PythonProvider, IronPython,       Version=1.0.2391.18146, Culture=neutral,       PublicKeyToken=b03f5f7f11d50a3a" />  </compilers></system.codedom>  
```  
  
## <a name="in-this-section"></a>本节内容  
 [网站支持模板](../../extensibility/internals/web-site-support-templates.md)  
 列出了可用于创建新的网站项目和关联项的模板。  
  
 [网站支持属性](../../extensibility/internals/web-site-support-attributes.md)  
 显示将网站项目连接到和的注册属性 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 。  
  
## <a name="related-sections"></a>相关章节  
 [Web 项目](../../extensibility/internals/web-projects.md)  
 概括介绍了两种 Web 项目、网站项目和 Web 应用程序项目。
