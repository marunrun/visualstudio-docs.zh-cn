---
title: 对项目和配置属性的支持 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project properties, supporting with Visual Studio SDK
- configuration properties, supporting with Visual Studio SDK
ms.assetid: 9fcfaa0f-7b41-4b68-82ec-7a151dca5d7e
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c21d552e26add3a5159febd666c1f60573697535
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80704903"
---
# <a name="support-for-project-and-configuration-properties"></a>支持项目和配置属性
集成开发环境 （IDE） 中的[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]**"属性**"窗口可以显示项目和配置属性。 您可以为自己的项目类型提供属性页，以便用户可以为应用程序设置属性。

 通过在**解决方案资源管理器**中选择项目节点，然后单击 **"项目**"菜单上**的属性**，可以打开包含项目和配置属性的对话框。 在[!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)][!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)]和 和 和 派生自这些语言的项目类型中，此对话框在["常规、环境、选项"对话框](../../ide/reference/general-environment-options-dialog-box.md)中显示为选项卡式页面。 有关详细信息，请参阅[不在生成中：演练：公开项目和配置属性 （C#）。](https://msdn.microsoft.com/library/d850d63b-25e2-4505-9f3d-eb038d7c1d0e)

 项目管理包框架 （MPFProj） 提供用于创建和管理新项目系统的帮助程序类。 您可以在[项目 MPF - Visual Studio 2013](https://github.com/tunnelvisionlabs/MPFProj10)找到源代码和编译说明。

## <a name="persistence-of-project-and-configuration-properties"></a>项目和配置属性的持久性
 项目和配置属性将保留在具有与项目类型关联的任何文件名扩展名的项目文件中，例如 .csproj、.vbproj 和 .myproj。 语言项目通常使用模板文件生成项目文件。 但是，实际上有几种方法可以关联项目类型和模板。 有关详细信息，请参阅[模板目录说明 （。Vsdir） 文件](../../extensibility/internals/template-directory-description-dot-vsdir-files.md)。

 项目和配置属性是通过向模板文件添加项来创建的。 然后，这些属性可用于使用使用此模板的项目类型创建的任何项目。 [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)]项目和 MPFProj 都使用[模板文件的"不在生成中：MS构建概述](/previous-versions/visualstudio/visual-studio-2008/ms171452(v=vs.90))"架构。 这些文件具有每个配置的属性组部分。 项目的属性通常保留在第一属性组部分，该部分具有设置为空字符串的配置参数。

 以下代码显示基本 MSBuild 项目文件的开始。

```
<Project MSBuildVersion="2.0" DefaultTargets="Build" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
  <PropertyGroup>
    <Configuration Condition=" '$(Configuration)' == '' ">Debug</Configuration>
    <Name>SomeProjectSix</Name>
    <SchemaVersion>2.0</SchemaVersion>
  </PropertyGroup>
  <PropertyGroup Condition=" '$(Configuration)' == 'Debug' ">
    <Optimize>false</Optimize>
  </PropertyGroup>
  <PropertyGroup Condition=" '$(Configuration)' == 'Release' ">
    <Optimize>true</Optimize>
```

 在此项目文件中，`<Name>`并且`<SchemaVersion>`是项目属性，并且`<Optimize>`是配置属性。

 项目负责保留项目文件的项目和配置属性。

> [!NOTE]
> 项目可以通过仅保留与其默认值不同的属性值来优化持久性。

## <a name="support-for-project-and-configuration-properties"></a>支持项目和配置属性
 类`Microsoft.VisualStudio.Package.SettingsPage`实现项目和配置属性页。 默认`SettingsPage`实现向泛型属性网格中的用户提供公共属性。 该方法`Microsoft.VisualStudio.Package.HierarchyNode.GetPropertyPageGuids`选择派生自`SettingsPage`项目属性网格的类。 该方法`Microsoft.VisualStudio.Package.ProjectNode.GetConfigPropertyPageGuids`选择派生自`SettingsPage`配置属性网格的类。 项目类型应重写这些方法以选择适当的属性页。

 类`SettingsPage`和`Microsoft.VisualStudio.Package.ProjectNode`类提供以下方法来保留项目和配置属性：

- `Microsoft.VisualStudio.Package.ProjectNode.GetProjectProperty`并`Microsoft.VisualStudio.Package.ProjectNode.SetProjectProperty`保留项目属性。

- `Microsoft.VisualStudio.Package.SettingsPage.GetConfigProperty`并`Microsoft.VisualStudio.Package.SettingsPage.SetConfigProperty`保留配置属性。

  > [!NOTE]
  > 和 类的实现使用`Microsoft.Build.BuildEngine`（MSBuild） 方法从项目文件中获取和设置项目和配置属性。 `Microsoft.VisualStudio.Package.ProjectNode` `Microsoft.VisualStudio.Package.SettingsPage`

  派生自`SettingsPage`的类必须实现`Microsoft.VisualStudio.Package.SettingsPage.ApplyChanges`并`Microsoft.VisualStudio.Package.SettingsPage.BindProperties`保留项目文件的项目或配置属性。

## <a name="provideobjectattribute-and-registry-path"></a>提供对象属性和注册表路径
 派生的`SettingsPage`类设计为跨 VSPackages 共享。 为了使 VSPackage 能够创建派生自 的`SettingsPage`类，请将 a`Microsoft.VisualStudio.Shell.ProvideObjectAttribute`添加到派生自`Microsoft.VisualStudio.Shell.Package`的类。

 [!code-csharp[VSSDKSupportProjectConfigurationProperties#1](../../extensibility/internals/codesnippet/CSharp/support-for-project-and-configuration-properties_1.cs)]
 [!code-vb[VSSDKSupportProjectConfigurationProperties#1](../../extensibility/internals/codesnippet/VisualBasic/support-for-project-and-configuration-properties_1.vb)]

 附加到该属性的 VS 包并不重要。 当 VSPackage 注册时[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]，将注册任何可创建对象的类 ID （CLSID），以便调用 可以<xref:Microsoft.VisualStudio.Shell.Interop.ILocalRegistry.CreateInstance%2A>创建它。

 可以创建的对象的注册表路径通过组合<xref:Microsoft.VisualStudio.Shell.Package.UserRegistryRoot%2A>、单词、CLSID 和对象类型的 guid 来确定。 如果`MyProjectPropertyPage`类的 guid 为 {3c693da2-5bca-49b3-bd95-ffe0a39d723}，并且用户注册Root 是HKEY_CURRENT_USER\软件\微软_VisualStudio_8.0Exp， 然后注册表路径将是HKEY_CURRENT_USER\软件\微软_VisualStudio_8.0Exp_CLSID\\{3c693da2-5bca-49b3-bd95-ffe0a39d723}。

## <a name="project-and-configuration-property-attributes-and-layout"></a>项目和配置属性属性和布局
 <xref:System.ComponentModel.DisplayNameAttribute><xref:System.ComponentModel.DescriptionAttribute>和<xref:System.ComponentModel.CategoryAttribute>属性确定泛型属性页中的项目和配置属性的布局、标记和说明。 这些属性分别确定选项的类别、显示名称和说明。

> [!NOTE]
> 等效属性、SR 类别、LocDisplayName 和 SR 描述，使用字符串资源进行本地化，并在[项目 MPF 中定义 - Visual Studio 2013](https://github.com/tunnelvisionlabs/MPFProj10)。

 考虑以下代码片断：

 [!code-vb[VSSDKSupportProjectConfigurationProperties#2](../../extensibility/internals/codesnippet/VisualBasic/support-for-project-and-configuration-properties_2.vb)]
 [!code-csharp[VSSDKSupportProjectConfigurationProperties#2](../../extensibility/internals/codesnippet/CSharp/support-for-project-and-configuration-properties_2.cs)]

 配置`MyConfigProp`属性在配置属性页上显示为类别中**的"我的****配置**属性" 如果选择了该选项，则说明"**我的描述**"将显示在说明面板中。

## <a name="see-also"></a>请参阅
- [添加和删除属性页](../../extensibility/adding-and-removing-property-pages.md)
- [项目](../../extensibility/internals/projects.md)
- [模板目录说明 (.Vsdir) 文件](../../extensibility/internals/template-directory-description-dot-vsdir-files.md)
