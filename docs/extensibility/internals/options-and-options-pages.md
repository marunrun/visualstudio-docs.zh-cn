---
title: 选项和选项页面 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Tools Options pages [Visual Studio SDK], managed package framework support
- managed package framework, Tools Options pages support
- support, Tools Options pages
- Tools Options pages [Visual Studio SDK], layouts
- Tools Options pages [Visual Studio SDK], attributes
ms.assetid: e6c0e636-5ec3-450e-b395-fc4bb9d75918
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 7d21bf6d5ab7e23047a02e1188fff9a47d0cbd58
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80706839"
---
# <a name="options-and-options-pages"></a>选项和选项页
单击"**工具**"菜单上**的选项**将打开"**选项"** 对话框。 此对话框中的选项统称为选项页。 导航窗格中的树控件包括选项类别，每个类别都有选项页。 选择页面时，其选项将显示在右侧窗格中。 这些页面允许您更改确定 VSPackage 状态的选项的值。

## <a name="support-for-options-pages"></a>支持选项页
 该<xref:Microsoft.VisualStudio.Shell.Package>类支持创建选项页和选项类别。 类<xref:Microsoft.VisualStudio.Shell.DialogPage>实现一个选项页。

 的<xref:Microsoft.VisualStudio.Shell.DialogPage>默认实现向属性的通用网格中的用户提供其公共属性。 您可以通过重写页面上的各种方法来自定义此行为，以创建具有其自己的用户界面 （UI） 的自定义选项页。 有关详细信息，请参阅[创建选项页](../../extensibility/creating-an-options-page.md)。

 类<xref:Microsoft.VisualStudio.Shell.DialogPage>实现<xref:Microsoft.VisualStudio.Shell.IProfileManager>，它为选项页和用户设置提供持久性。 如果属性可以转换为字符串并从<xref:Microsoft.VisualStudio.Shell.IProfileManager.LoadSettingsFromStorage%2A>字符串<xref:Microsoft.VisualStudio.Shell.IProfileManager.SaveSettingsToStorage%2A>转换，则 和 方法的默认实现将属性保留为注册表的用户部分。

## <a name="options-page-registry-path"></a>选项页面注册表路径
 默认情况下，由选项页管理的属性的注册表路径通过组合<xref:Microsoft.VisualStudio.Shell.Package.UserRegistryRoot%2A>、单词 DialogPage 和选项页类的类型名称来确定。 例如，选项页类的定义可能如下。

 [!code-csharp[VSSDKSupportForOptionsPages#1](../../extensibility/internals/codesnippet/CSharp/options-and-options-pages_1.cs)]
 [!code-vb[VSSDKSupportForOptionsPages#1](../../extensibility/internals/codesnippet/VisualBasic/options-and-options-pages_1.vb)]

 如果<xref:Microsoft.VisualStudio.Shell.Package.UserRegistryRoot%2A>是 HKEY_CURRENT_USER\软件\Microsoft_VisualStudio_8.0Exp，则属性名称和值对是HKEY_CURRENT_USER\软件\微软_VisualStudio_8.0Exp_DialogPage_公司.OptionsPage.OptionsPage。"选项页"

 选项页的注册表路径通过组合<xref:Microsoft.VisualStudio.Shell.Package.ApplicationRegistryRoot%2A>（word、ToolsOptionsPages 和选项页类别和名称）来确定。 例如，如果"自定义选项页"具有类别"我的选项页"，并且<xref:Microsoft.VisualStudio.Shell.Package.ApplicationRegistryRoot%2A>是 HKEY_LOCAL_MACHINE_SOFTWARE_Microsoft_VisualStudio_8.0Exp，则选项页具有注册表项，HKEY_LOCAL_MACHINE_SOFTWARE_Microsoft_VisualStudio_8.0Exp_ToolsOptionPages_我的选项页面\自定义。

## <a name="toolsoptions-page-attributes-and-layout"></a>工具/选项页面属性和布局
 该<xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute>属性确定自定义选项页分组到 **"选项"** 对话框的导航树中的类别。 该<xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute>属性将选项页与提供接口的 VSPackage 关联。 考虑以下代码片断：

 [!code-csharp[VSSDKSupportForOptionsPages#2](../../extensibility/internals/codesnippet/CSharp/options-and-options-pages_2.cs)]
 [!code-vb[VSSDKSupportForOptionsPages#2](../../extensibility/internals/codesnippet/VisualBasic/options-and-options-pages_2.vb)]

 这将声明"我的包"提供两个选项页面：选项页常规和选项页面自定义。 在"**选项"** 对话框中，两个选项页分别显示在"**我的选项页"** 类别中，分别显示为 **"常规****"和"自定义**"。

## <a name="option-attributes-and-layout"></a>选项属性和布局
 页面提供的用户界面 （UI） 确定自定义选项页中选项的外观。 泛型选项页中选项的布局、标记和说明由以下属性确定：

- <xref:System.ComponentModel.CategoryAttribute>确定选项的类别。

- <xref:System.ComponentModel.DisplayNameAttribute>确定选项的显示名称。

- <xref:System.ComponentModel.DescriptionAttribute>确定选项的说明。

  > [!NOTE]
  > 等效属性、SR 类别、LocDisplayName 和 SR描述使用字符串资源进行本地化，并在[托管项目示例中](/azure/devops/integrate/index)定义。

  考虑以下代码片断：

  [!code-csharp[VSSDKSupportForOptionsPages#3](../../extensibility/internals/codesnippet/CSharp/options-and-options-pages_3.cs)]
  [!code-vb[VSSDKSupportForOptionsPages#3](../../extensibility/internals/codesnippet/VisualBasic/options-and-options-pages_3.vb)]

  "选项整数"选项在"**我的选项**"类别中显示为**整数选项**。 如果选择了该选项，则说明"**我的整数"选项**将显示在描述框中。

## <a name="accessing-options-pages-from-another-vspackage"></a>从其他 VS 包访问选项页
 可以使用自动化模型从另一个 VSPackage 以编程方式访问承载和管理选项页的 VSPackage。 例如，在以下代码中，VSPackage 注册为托管选项页。

 [!code-csharp[VSSDKSupportForOptionsPages#4](../../extensibility/internals/codesnippet/CSharp/options-and-options-pages_4.cs)]
 [!code-vb[VSSDKSupportForOptionsPages#4](../../extensibility/internals/codesnippet/VisualBasic/options-and-options-pages_4.vb)]

 以下代码片段从 MyOptionPage 获取 OptionInteger 的值：

 [!code-csharp[VSSDKSupportForOptionsPages#5](../../extensibility/internals/codesnippet/CSharp/options-and-options-pages_5.cs)]
 [!code-vb[VSSDKSupportForOptionsPages#5](../../extensibility/internals/codesnippet/VisualBasic/options-and-options-pages_5.vb)]

 当<xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute>属性注册选项页时，如果属性的`SupportsAutomation`参数为`true`，则该页将注册在自动化属性键下。 自动化检查此注册表项以查找关联的 VSPackage，然后自动化通过托管选项页（本例中为"我的网格页"）访问该属性。

 自动化属性的注册表路径通过组合<xref:Microsoft.VisualStudio.Shell.Package.ApplicationRegistryRoot%2A>、单词、自动化属性和选项页类别和名称来确定。 例如，如果选项页具有"我的类别"类别、"我的网格页"名称以及<xref:Microsoft.VisualStudio.Shell.Package.ApplicationRegistryRoot%2A>、HKEY_LOCAL_MACHINE_SOFTWARE_Microsoft_VisualStudio_8.0Exp，则自动化属性具有注册表项HKEY_LOCAL_MACHINE_SOFTWARE_Microsoft_VisualStudio_8.0Exp_自动化属性\我的类别\我的网格页面。

> [!NOTE]
> 规范名称"我的Category.My网格页"是此键的名称子键的值。
