---
title: 使用托管包框架实现项目类型（C#） |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], creating with MPF
- MPF projects
- managed package framework, creating projects
ms.assetid: 926de536-eead-415b-9451-f1ddc8c44630
caps.latest.revision: 21
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 066695c6d94603d0a0474243ed05dece4cc0bd1f
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74300361"
---
# <a name="using-the-managed-package-framework-to-implement-a-project-type-c"></a>使用托管包框架实现项目类型 (C#)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

托管包框架（MPF）提供C#可用于实现自己的项目类型的类，也可以从继承。 MPF 实现了许多 Visual Studio 所需的接口，从而让你自由地集中精力实现项目类型的细节。  
  
## <a name="using-the-mpf-project-source-code"></a>使用 MPF 项目源代码  
 项目的托管包框架（MPFProj）提供用于创建和管理新项目系统的帮助程序类。 与 MPF 中的其他类不同，项目类不包括在随 Visual Studio 一起提供的程序集中。 相反，项目类作为[2013](https://archive.codeplex.com/?p=mpfproj12)中项目的源代码提供。  
  
 若要将此项目添加到 VSPackage 解决方案，请执行以下操作：  
  
1. 将 MPFProj 文件下载到*MPFProjectDir*。  
  
2. 在*MPFProjectDir*\Dev10\Src\CSharp\ProjectBase.file 中，更改以下块：  
  
```  
<!-- Provide a default value for $(ProjectBasePath) -->  
  <PropertyGroup>  
    <ProjectBasePath >MPFProjDir\Dev10\Src\CSharp</ProjectBasePath>  
  </PropertyGroup>  
```  
  
1. 创建 VSPackage 项目。  
  
2. 卸载 VSPackage 项目。  
  
3. 编辑 VSPackage 文件，方法是在其他 `<Import>` 块之前添加以下块：  
  
```  
<Import Project="MPFProjectDir\Dev10\Src\CSharp\ProjectBase.files" />  
  <PropertyGroup>  
    <!--To specify a different registry root to register your package, uncomment the TargetRegistryRoot tag and specify a registry root in it.  
    <TargetRegistryRoot></TargetRegistryRoot>-->  
    <RegisterOutputPackage>true</RegisterOutputPackage>  
    <RegisterWithCodebase>true</RegisterWithCodebase>  
  </PropertyGroup>  
```  
  
1. 保存项目。  
  
2. 关闭并重新打开 VSPackage 解决方案。  
  
3. 重新打开 VSPackage 项目。 应会看到名为 ProjectBase 的新目录。  
  
4. 将以下引用添加到 VSPackage 项目：  
  
     Microsoft.Build.Tasks.4.0  
  
5. 生成项目。  
  
## <a name="hierarchy-classes"></a>层次结构类  
 下表汇总了支持项目层次结构的 MPFProj 中的类。 有关详细信息，请参阅[层次结构和选择](../../extensibility/internals/hierarchies-and-selection.md)。  
  
|类名称|  
|----------------|  
|`Microsoft.VisualStudio.Package.HierarchyNode`|  
|`Microsoft.VisualStudio.Package.ProjectNode`|  
|`Microsoft.VisualStudio.Package.ProjectContainerNode`|  
|`Microsoft.VisualStudio.Package.FileNode`|  
|`Microsoft.VisualStudio.Package.FolderNode`|  
|`Microsoft.VisualStudio.Package.ReferenceContainerNode`|  
|`Microsoft.VisualStudio.Package.ReferenceNode`|  
|`Microsoft.VisualStudio.Package.ProjectReferenceNode`|  
|`Microsoft.VisualStudio.Package.ComReferenceNode`|  
|`Microsoft.VisualStudio.Package.AssemblyReferenceNode`|  
|`Microsoft.VisualStudio.Package.BuildDependency`|  
  
## <a name="document-handling-classes"></a>文档处理类  
 下表列出了支持文档处理的 MPF 中的类。 有关详细信息，请参阅[打开和保存项目项](../../extensibility/internals/opening-and-saving-project-items.md)。  
  
|类名称|  
|----------------|  
|`Microsoft.VisualStudio.Package.DocumentManager`|  
|`Microsoft.VisualStudio.Package.FileDocumentManager`|  
  
## <a name="configuration-and-output-classes"></a>配置和输出类  
 下表列出了 MPF 中的类，这些类允许项目类型支持多个配置，例如调试和发布以及项目输出的集合。 有关详细信息，请参阅[管理配置选项](../../extensibility/internals/managing-configuration-options.md)。  
  
|类名称|  
|----------------|  
|`Microsoft.VisualStudio.Package.ConfigProvider`|  
|`Microsoft.VisualStudio.Package.ProjectConfig`|  
|`Microsoft.VisualStudio.Package.BuildableProjectConfig`|  
|`Microsoft.VisualStudio.Package.OutputGroup`|  
|`Microsoft.VisualStudio.Package.ProjectElement`|  
  
## <a name="automation-support-classes"></a>自动化-支持类  
 下表列出了支持自动化的 MPF 中的类，以便您的项目类型的用户可以编写外接程序。  
  
|类名称|  
|----------------|  
|`Microsoft.VisualStudio.Package.Automation.OAProject`|  
|`Microsoft.VisualStudio.Package.Automation.OANavigableProjectItems`|  
|`Microsoft.VisualStudio.Package.Automation.OAProjectItems`|  
|`Microsoft.VisualStudio.Package.Automation.OAProjectItem`|  
|`Microsoft.VisualStudio.Package.Automation.OANestedProjectItem`|  
  
## <a name="properties-classes"></a>Properties 类  
 下表列出了 MPF 中的类，这些类允许项目类型添加用户可以在属性浏览器中浏览和修改的属性。  
  
|类名称|  
|----------------|  
|`Microsoft.VisualStudio.Package.LocalizableProperties`|  
|`Microsoft.VisualStudio.Package.NodeProperties`|  
|`Microsoft.VisualStudio.Package.FileNodeProperties`|  
|`Microsoft.VisualStudio.Package.ProjectNodeProperties`|  
|`Microsoft.VisualStudio.Package.FolderNodeProperties`|  
|`Microsoft.VisualStudio.Package.ReferenceNodeProperties`|
