---
title: 托管 Vspackage |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: devlang-csharp
ms.topic: conceptual
helpviewer_keywords:
- VSPackages, managed
- managed VSPackages
ms.assetid: a4f17068-c563-45a8-bbbf-4203ea99e9d2
caps.latest.revision: 34
manager: jillfra
ms.openlocfilehash: bde7742bc9165413abcf98bfb475c19ec0e45f51
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62838758"
---
# <a name="managed-vspackages"></a>托管的 VSPackage
以下主题介绍如何创建 VSPackage。 VSPackage 是一个软件模块，它 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 通过提供用户界面 (UI) 元素、服务、项目、编辑器和设计器来扩展集成开发环境 (IDE) 。 有关更多信息，请参见 [VSPackages](../extensibility/internals/vspackages.md)。  
  
## <a name="in-this-section"></a>本节内容  
 [使用 Visual Studio 互操作程序集](../extensibility/internals/using-visual-studio-interop-assemblies.md)  
 介绍 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 互操作程序集及其提供的命名空间的功能和位置。  
  
 [托管代码中的 HRESULT 信息](../misc/hresult-information-in-managed-code.md)  
 讨论如何在托管代码中将 HRESULT 信息转换为引发的异常和 `int` 返回值。  
  
 [Visual Studio 互操作程序集参数封送处理](../misc/visual-studio-interop-assembly-parameter-marshaling.md)  
 讨论 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 互操作程序集和 COM 接口之间的互操作性问题。  
  
 [VSPackage 和托管包框架](../misc/vspackages-and-the-managed-package-framework.md)  
 描述并列出托管包框架 (MPF) 类命名空间和 DLL 文件，并演示如何使用它们创建一个 VSPackage。  
  
 [VSPackage 中的资源](../extensibility/internals/resources-in-vspackages.md)  
 介绍如何在托管 Vspackage 中使用托管资源和非托管资源。  
  
## <a name="related-sections"></a>相关章节  
 [VSSDK 实用工具](../extensibility/internals/vssdk-utilities.md)  
 显示 VSPackage 内部和高级主题的集合。