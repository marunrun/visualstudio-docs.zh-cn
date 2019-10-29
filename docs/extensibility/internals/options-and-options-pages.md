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
ms.openlocfilehash: 963a73a3a8e079b2171c88e901913990892715cd
ms.sourcegitcommit: dcbb876a5dd598f2538e62e1eabd4dc98595b53a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2019
ms.locfileid: "72981889"
---
# <a name="options-and-options-pages"></a>选项和选项页
单击 "**工具**" 菜单上的 "**选项**" 将打开 "**选项**" 对话框。 此对话框中的选项统称为 "选项页"。 导航窗格中的树控件包含选项类别，每个类别都包含 "选项" 页。 选择某个页面后，其选项将显示在右窗格中。 这些页面使你可以更改用于确定 VSPackage 状态的选项的值。

## <a name="support-for-options-pages"></a>支持选项页
 <xref:Microsoft.VisualStudio.Shell.Package> 类为创建选项页和选项类别提供支持。 <xref:Microsoft.VisualStudio.Shell.DialogPage> 类实现了选项页。

 <xref:Microsoft.VisualStudio.Shell.DialogPage> 的默认实现向用户提供其公共属性。 您可以通过重写页面上的各种方法来自定义此行为，以创建具有其自己的用户界面（UI）的自定义选项页。 有关详细信息，请参阅[创建选项页](../../extensibility/creating-an-options-page.md)。

 <xref:Microsoft.VisualStudio.Shell.DialogPage> 类实现 <xref:Microsoft.VisualStudio.Shell.IProfileManager>，后者为选项页提供持久性，还用于用户设置。 <xref:Microsoft.VisualStudio.Shell.IProfileManager.LoadSettingsFromStorage%2A> 和 <xref:Microsoft.VisualStudio.Shell.IProfileManager.SaveSettingsToStorage%2A> 方法的默认实现将属性更改保存到注册表的用户部分（如果可以将属性转换为字符串或从字符串转换为）。

## <a name="options-page-registry-path"></a>选项页注册表路径
 默认情况下，由 "选项" 页管理的属性的注册表路径由 "选项" 页面类 <xref:Microsoft.VisualStudio.Shell.Package.UserRegistryRoot%2A>、单词 Dialogpage 派生和类型名称的组合确定。 例如，可以按如下所示定义选项页类。

 [!code-csharp[VSSDKSupportForOptionsPages#1](../../extensibility/internals/codesnippet/CSharp/options-and-options-pages_1.cs)]
 [!code-vb[VSSDKSupportForOptionsPages#1](../../extensibility/internals/codesnippet/VisualBasic/options-and-options-pages_1.vb)]

 如果 <xref:Microsoft.VisualStudio.Shell.Package.UserRegistryRoot%2A> HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\8.0Exp，则属性名称和值对是 HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\8.0Exp\DialogPage\Company.OptionsPage.OptionsPageGeneral. 的子项。

 "选项" 页本身的注册表路径是通过组合 <xref:Microsoft.VisualStudio.Shell.Package.ApplicationRegistryRoot%2A>、word、ToolsOptionsPages 和 "选项" 页类别和名称确定的。 例如，如果 "自定义选项" 页具有 "类别"、"我的选项" 页和 "<xref:Microsoft.VisualStudio.Shell.Package.ApplicationRegistryRoot%2A> HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0Exp，则" 选项 "页将包含注册表项 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0 exp \ ToolsOptionsPages \ i 选项 Pages\Custom。

## <a name="toolsoptions-page-attributes-and-layout"></a>"工具/选项" 页属性和布局
 <xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute> 特性确定将自定义选项页分组到 "**选项**" 对话框的导航树中的类别。 <xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute> 特性将选项页与提供接口的 VSPackage 相关联。 考虑以下代码片断：

 [!code-csharp[VSSDKSupportForOptionsPages#2](../../extensibility/internals/codesnippet/CSharp/options-and-options-pages_2.cs)]
 [!code-vb[VSSDKSupportForOptionsPages#2](../../extensibility/internals/codesnippet/VisualBasic/options-and-options-pages_2.vb)]

 这声明 MyPackage 提供了两个选项页： OptionsPageGeneral 和 OptionsPageCustom。 在 "**选项**" 对话框中，这两个选项页在 "**我的选项页**" 类别中分别显示为 "**常规**" 和 "**自定义**"。

## <a name="option-attributes-and-layout"></a>选项属性和布局
 页面提供的用户界面（UI）确定自定义选项页中选项的外观。 "常规选项" 页中的选项布局、标签和说明由以下属性确定：

- <xref:System.ComponentModel.CategoryAttribute> 确定选项的类别。

- <xref:System.ComponentModel.DisplayNameAttribute> 确定选项的显示名称。

- <xref:System.ComponentModel.DescriptionAttribute> 确定选项的说明。

  > [!NOTE]
  > 等效属性、SRCategory、LocDisplayName 和 SRDescription，使用字符串资源进行本地化，并在[托管项目示例](/azure/devops/integrate/index)中定义。

  考虑以下代码片断：

  [!code-csharp[VSSDKSupportForOptionsPages#3](../../extensibility/internals/codesnippet/CSharp/options-and-options-pages_3.cs)]
  [!code-vb[VSSDKSupportForOptionsPages#3](../../extensibility/internals/codesnippet/VisualBasic/options-and-options-pages_3.vb)]

  "选项" 页上的 "OptionInteger" 选项显示为 "**我的选项**" 类别中的**整数选项**。 如果选择了该选项，则 "说明" 框中会显示 "**我的整数" 选项**。

## <a name="accessing-options-pages-from-another-vspackage"></a>访问其他 VSPackage 的选项页
 承载和管理选项页的 VSPackage 可以通过使用自动化模型以编程方式从另一个 VSPackage 访问。 例如，在以下代码中，VSPackage 注册为承载选项页。

 [!code-csharp[VSSDKSupportForOptionsPages#4](../../extensibility/internals/codesnippet/CSharp/options-and-options-pages_4.cs)]
 [!code-vb[VSSDKSupportForOptionsPages#4](../../extensibility/internals/codesnippet/VisualBasic/options-and-options-pages_4.vb)]

 以下代码片段从 MyOptionPage 中获取 OptionInteger 的值：

 [!code-csharp[VSSDKSupportForOptionsPages#5](../../extensibility/internals/codesnippet/CSharp/options-and-options-pages_5.cs)]
 [!code-vb[VSSDKSupportForOptionsPages#5](../../extensibility/internals/codesnippet/VisualBasic/options-and-options-pages_5.vb)]

 当 <xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute> 属性注册选项页时，如果该特性的 `SupportsAutomation` 参数 `true`，则该页将在 Automationproperties.livesetting 项下进行注册。 自动检查此注册表项以查找关联的 VSPackage，然后通过 "托管选项" 页（在本例中为 "我的网格" 页）访问属性。

 自动化属性的注册表路径是通过组合 <xref:Microsoft.VisualStudio.Shell.Package.ApplicationRegistryRoot%2A>、word、Automationproperties.livesetting 和 options 页面类别和名称确定的。 例如，如果 "选项" 页具有 "我的类别" 类别、"我的网格" 页名称和 <xref:Microsoft.VisualStudio.Shell.Package.ApplicationRegistryRoot%2A>HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0Exp，则自动化属性将具有注册表项 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0Exp\AutomationProperties\My Category\My 网格页。

> [!NOTE]
> 规范名称 "我的 Category.My" 网格页是此项的 Name 子项的值。