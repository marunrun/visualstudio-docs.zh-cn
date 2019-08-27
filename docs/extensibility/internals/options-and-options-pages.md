---
title: 选项和选项页 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Tools Options pages [Visual Studio SDK], managed package framework support
- managed package framework, Tools Options pages support
- support, Tools Options pages
- Tools Options pages [Visual Studio SDK], layouts
- Tools Options pages [Visual Studio SDK], attributes
ms.assetid: e6c0e636-5ec3-450e-b395-fc4bb9d75918
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 7c336503b80e2af34ac58c7debde16895d7f2585
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66314854"
---
# <a name="options-and-options-pages"></a>选项和选项页
单击**选项**上**工具**菜单打开**选项**对话框。 在此对话框中选项统称为选项页。 在导航窗格中的树控件包括选项类别和每个类别都有选项页。 当选择一个页面时，其选项将显示在右窗格中。 这些页面，您可以更改的值确定的 VSPackage 状态的选项。

## <a name="support-for-options-pages"></a>选项页的支持
 <xref:Microsoft.VisualStudio.Shell.Package>类为创建选项页和选项类别提供支持。 <xref:Microsoft.VisualStudio.Shell.DialogPage>类实现的选项页。

 默认实现<xref:Microsoft.VisualStudio.Shell.DialogPage>到一个通用的属性网格中的用户提供其公共属性。 通过重写页后，可以创建具有其自己的用户界面 (UI) 的自定义选项页上的各种方法，可以自定义此行为。 有关详细信息，请参阅[创建选项页](../../extensibility/creating-an-options-page.md)。

 <xref:Microsoft.VisualStudio.Shell.DialogPage>类实现<xref:Microsoft.VisualStudio.Shell.IProfileManager>，后者提供持久性选项页的和还为用户设置。 默认实现<xref:Microsoft.VisualStudio.Shell.IProfileManager.LoadSettingsFromStorage%2A>和<xref:Microsoft.VisualStudio.Shell.IProfileManager.SaveSettingsToStorage%2A>方法持久保存到注册表的用户部分的属性更改，如果与字符串可以转换该属性。

## <a name="options-page-registry-path"></a>选项页注册表路径
 默认情况下，由选项页的属性的注册表路径确定通过组合<xref:Microsoft.VisualStudio.Shell.Package.UserRegistryRoot%2A>，word dialogpage 派生和选项页类的类型名称。 例如，可能会按如下所示定义选项页类。

 [!code-csharp[VSSDKSupportForOptionsPages#1](../../extensibility/internals/codesnippet/CSharp/options-and-options-pages_1.cs)]
 [!code-vb[VSSDKSupportForOptionsPages#1](../../extensibility/internals/codesnippet/VisualBasic/options-and-options-pages_1.vb)]

 如果<xref:Microsoft.VisualStudio.Shell.Package.UserRegistryRoot%2A>为 HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\8.0Exp，则属性名称 / 值对的 HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\8.0Exp\DialogPage\ 子项Company.OptionsPage.OptionsPageGeneral。

 选项页本身的注册表路径由组合<xref:Microsoft.VisualStudio.Shell.Package.ApplicationRegistryRoot%2A>，单词、 ToolsOptionsPages，和选项页的类别和名称。 例如，如果自定义选项页具有类别，我的选项页面和<xref:Microsoft.VisualStudio.Shell.Package.ApplicationRegistryRoot%2A>为 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0Exp，则选项页具有注册表项，HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0Exp\ToolsOptionsPages\My 选项 Pages\Custom。

## <a name="toolsoptions-page-attributes-and-layout"></a>工具/选项页属性和布局
 <xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute>属性确定在导航树中的类别的自定义选项页分**选项**对话框。 <xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute>属性将与提供的接口的 VSPackage 相关联的选项页。 考虑以下代码片断：

 [!code-csharp[VSSDKSupportForOptionsPages#2](../../extensibility/internals/codesnippet/CSharp/options-and-options-pages_2.cs)]
 [!code-vb[VSSDKSupportForOptionsPages#2](../../extensibility/internals/codesnippet/VisualBasic/options-and-options-pages_2.vb)]

 这会将声明 MyPackage 提供了两个选项页面，OptionsPageGeneral 和 OptionsPageCustom。 中**选项**对话框中，这两个选项页将出现在**我选项页**作为类别**常规**并**自定义**分别。

## <a name="option-attributes-and-layout"></a>属性选项和布局
 此页提供了用户界面 (UI) 确定自定义选项页中的选项的外观。 布局、 设置标签和通用选项页中的选项的说明确定由以下属性：

- <xref:System.ComponentModel.CategoryAttribute> 确定选项的类别。

- <xref:System.ComponentModel.DisplayNameAttribute> 确定选项的显示名称。

- <xref:System.ComponentModel.DescriptionAttribute> 确定选项的说明。

  > [!NOTE]
  > 等效的属性、 SRCategory、 LocDisplayName 和 SRDescription，使用字符串资源本地化和中定义[托管的项目示例](http://go.microsoft.com/fwlink/?LinkId=122774)。

  考虑以下代码片断：

  [!code-csharp[VSSDKSupportForOptionsPages#3](../../extensibility/internals/codesnippet/CSharp/options-and-options-pages_3.cs)]
  [!code-vb[VSSDKSupportForOptionsPages#3](../../extensibility/internals/codesnippet/VisualBasic/options-and-options-pages_3.vb)]

  在作为选项页上会显示 OptionInteger 选项**整数选项**中**我的选项**类别。 如果选择了说明，**我整数选项**，将显示在描述框中。

## <a name="accessing-options-pages-from-another-vspackage"></a>从另一个 VSPackage 访问选项页
 托管和管理选项页的 VSPackage 可以以编程方式访问从另一个 VSPackage 使用自动化模型。 例如，下面的代码中的 VSPackage 注册为托管选项页。

 [!code-csharp[VSSDKSupportForOptionsPages#4](../../extensibility/internals/codesnippet/CSharp/options-and-options-pages_4.cs)]
 [!code-vb[VSSDKSupportForOptionsPages#4](../../extensibility/internals/codesnippet/VisualBasic/options-and-options-pages_4.vb)]

 下面的代码段从 MyOptionPage 获取 OptionInteger 的值：

 [!code-csharp[VSSDKSupportForOptionsPages#5](../../extensibility/internals/codesnippet/CSharp/options-and-options-pages_5.cs)]
 [!code-vb[VSSDKSupportForOptionsPages#5](../../extensibility/internals/codesnippet/VisualBasic/options-and-options-pages_5.vb)]

 当<xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute>属性注册选项页，将页面注册下 AutomationProperties 密钥 if`SupportsAutomation`属性的自变量是`true`。 自动化检查此注册表项以查找相关联的 VSPackage 和自动化，然后通过托管的选项页面，在这种情况下，我的网格页中访问的属性。

 通过组合确定的自动化属性的注册表路径<xref:Microsoft.VisualStudio.Shell.Package.ApplicationRegistryRoot%2A>，单词、 AutomationProperties，和选项页的类别和名称。 例如，如果选项页具有 My Category 类别中，我的网格页名称，和<xref:Microsoft.VisualStudio.Shell.Package.ApplicationRegistryRoot%2A>，HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0Exp，则该自动化属性具有注册表项，HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0Exp\AutomationProperties\My Category\My 网格页。

> [!NOTE]
> 规范名称，我 Category.My 网格页中，是此密钥的名称子项的值。