---
title: Vspackage 和托管包框架 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: devlang-csharp
ms.topic: conceptual
helpviewer_keywords:
- managed package framework
- VSPackages, managed package framework
- managed VSPackages, managed package framework
ms.assetid: e8d80e0f-6b5b-4baf-a7df-59fd808c60cd
caps.latest.revision: 16
manager: jillfra
ms.openlocfilehash: 84fb41bfc80415535ca41d6b1a8c9dcf47124c7a
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74298234"
---
# <a name="vspackages-and-the-managed-package-framework"></a>VSPackage 和托管包框架
通过使用托管包框架（MPF）类创建 VSPackage，而不是通过使用 COM 互操作类，可以缩短开发时间。  
  
 可以通过两种方法创建托管 VSPackage：  
  
- 使用 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 包项目模板  
  
     有关详细信息，请参阅[演练：使用 Visual Studio 包模板创建菜单命令](https://msdn.microsoft.com/library/1985fa7d-aad4-4866-b356-a125b6a246de)。  
  
- 在不 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 包项目模板的情况下生成你的 VSPackage  
  
     例如，可以复制示例 VSPackage 并更改 Guid 和名称。 
  
## <a name="in-this-section"></a>本节内容  
 [托管包框架类](../misc/managed-package-framework-classes.md)  
 描述和列出了 MPF 类命名空间和 DLL 文件。  
  
## <a name="related-sections"></a>相关章节  
 [演练：使用 Visual Studio 包模板创建菜单命令](https://msdn.microsoft.com/library/1985fa7d-aad4-4866-b356-a125b6a246de)  
 说明如何创建托管 VSPackage。  
  
 [托管的 VSPackage](../misc/managed-vspackages.md)  
 介绍适用于托管代码的 Vspackage 的各个方面。