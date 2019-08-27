---
title: 通过并行部署注册文件扩展名 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- file extensions, registering for side-by-side
ms.assetid: 9ab046a2-147d-4167-aa14-7d661b1eaaa5
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 354b91dd1282df9726c1ee9c47f610b0dfdd9c1a
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68163701"
---
# <a name="registering-file-name-extensions-for-side-by-side-deployments"></a>注册并行部署的文件扩展名
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

通过并行环境中部署的 Vspackage，你必须注册要将文件的正确版本与关联文件扩展名[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]。 除非您使用特定于版本的文件扩展名，注册使用户能够打开你的项目和项目项文件中的适当版本[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]。  
  
## <a name="in-this-section"></a>本节内容  
 [关于文件扩展名](../extensibility/about-file-name-extensions.md)  
 讨论如何注册文件扩展名。  
  
 [指定文件扩展名的文件处理程序](../extensibility/specifying-file-handlers-for-file-name-extensions.md)  
 提供有关如何注册应用程序可以打开、 编辑和等等，特定文件扩展名的信息。  
  
 [注册文件扩展名的谓词](../extensibility/registering-verbs-for-file-name-extensions.md)  
 讨论如何注册动词。  
  
 [管理并行文件关联](../extensibility/managing-side-by-side-file-associations.md)  
 讨论如何处理通过并行安装在其中的某个特定版本[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]应被调用来打开文件。  
  
## <a name="related-sections"></a>相关章节  
 [支持多个版本的 Visual Studio](../extensibility/supporting-multiple-versions-of-visual-studio.md)  
 在开发和向最终用户部署的过程中，描述与多个版本的 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 和你的 VSPackage 相关的问题。
