---
title: 对项目类型 （C#） 使用托管包框架 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], creating with MPF
- MPF projects
- managed package framework, creating projects
ms.assetid: 926de536-eead-415b-9451-f1ddc8c44630
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 7ca9dda0b699e0f70b0c945ab9ecfe9f9f4dcda6
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80704123"
---
# <a name="using-the-managed-package-framework-to-implement-a-project-type-c"></a>使用托管包框架实现项目类型 (C#)
托管包框架 （MPF） 提供可用于或继承的 C# 类来实现您自己的项目类型。 MPF 实现了 Visual Studio 希望项目类型提供的许多接口，让您可以自由地专注于实现项目类型的详细信息。

## <a name="using-the-mpf-project-source-code"></a>使用 MPF 项目源代码
 项目管理包框架 （MPFProj） 提供用于创建和管理新项目系统的帮助程序类。 与 MPF 中的其他类不同，项目类不包括在 Visual Studio 附带的程序集中。 相反，项目类在[2013 年项目 MPF](https://github.com/tunnelvisionlabs/MPFProj10)中作为源代码提供。

 要将此项目添加到 VSPackage 解决方案，请执行以下操作：

1. 下载MPFProj文件到*MPF项目迪尔*。

2. 在*MPFProjectDir*[Dev10]Src_CSharp_ProjectBase.文件中，更改以下块：

```
<!-- Provide a default value for $(ProjectBasePath) -->
  <PropertyGroup>
    <ProjectBasePath >MPFProjDir\Dev10\Src\CSharp</ProjectBasePath>
  </PropertyGroup>
```

1. 创建 VSPackage 项目。

2. 卸载 VSPackage 项目。

3. 通过在其他`<Import>`块之前添加以下块来编辑 VSPackage .csproj 文件：

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

3. 重新打开 VSPackage 项目。 您应该会看到一个名为 ProjectBase 的新目录。

4. 添加以下对 VSPackage 项目的引用：

     微软.生成.任务.4.0

5. 生成项目。

## <a name="hierarchy-classes"></a>层次结构类
 下表总结了 MPFProj 中支持项目层次结构的类。 有关详细信息，请参阅[层次结构和选择](../../extensibility/internals/hierarchies-and-selection.md)。

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
 下表列出了支持文档处理的 MPF 中的类。 有关详细信息，请参阅[打开和保存项目项目](../../extensibility/internals/opening-and-saving-project-items.md)。

|类名称|
|----------------|
|`Microsoft.VisualStudio.Package.DocumentManager`|
|`Microsoft.VisualStudio.Package.FileDocumentManager`|

## <a name="configuration-and-output-classes"></a>配置和输出类
 下表列出了 MPF 中的类，这些类允许项目类型支持多种配置，如调试和发布以及项目输出集合。 有关详细信息，请参阅[管理配置选项](../../extensibility/internals/managing-configuration-options.md)。

|类名称|
|----------------|
|`Microsoft.VisualStudio.Package.ConfigProvider`|
|`Microsoft.VisualStudio.Package.ProjectConfig`|
|`Microsoft.VisualStudio.Package.BuildableProjectConfig`|
|`Microsoft.VisualStudio.Package.OutputGroup`|
|`Microsoft.VisualStudio.Package.ProjectElement`|

## <a name="automation-support-classes"></a>自动化支持类
 下表列出了支持自动化的 MPF 中的类，以便项目类型的用户可以编写加载项。

|类名称|
|----------------|
|`Microsoft.VisualStudio.Package.Automation.OAProject`|
|`Microsoft.VisualStudio.Package.Automation.OANavigableProjectItems`|
|`Microsoft.VisualStudio.Package.Automation.OAProjectItems`|
|`Microsoft.VisualStudio.Package.Automation.OAProjectItem`|
|`Microsoft.VisualStudio.Package.Automation.OANestedProjectItem`|

## <a name="properties-classes"></a>属性类
 下表列出了 MPF 中的类，这些类允许项目类型添加用户可以在属性浏览器中浏览和修改的属性。

|类名称|
|----------------|
|`Microsoft.VisualStudio.Package.LocalizableProperties`|
|`Microsoft.VisualStudio.Package.NodeProperties`|
|`Microsoft.VisualStudio.Package.FileNodeProperties`|
|`Microsoft.VisualStudio.Package.ProjectNodeProperties`|
|`Microsoft.VisualStudio.Package.FolderNodeProperties`|
|`Microsoft.VisualStudio.Package.ReferenceNodeProperties`|
