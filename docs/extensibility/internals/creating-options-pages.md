---
title: 创建选项页 |Microsoft Docs
description: 了解如何通过从托管包框架实现 Dialogpage 派生类，在 Visual Studio 的 "工具" 菜单下创建选项页。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- managed package framework, creating Tools Options pages
- Tools Options pages [Visual Studio SDK], creating using managed package framework
ms.assetid: 1bf11fec-dece-4943-8053-6de1483c43eb
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 4759b3590fcde116e6f106ac326ff875e9566c43
ms.sourcegitcommit: 9ce13a961719afbb389fa033fbb1a93bea814aae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/30/2020
ms.locfileid: "96328634"
---
# <a name="create-options-pages"></a>创建选项页
在 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 托管包框架中， <xref:Microsoft.VisualStudio.Shell.DialogPage> 通过在 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] "**工具**" 菜单下添加 "**选项**" 页，从派生的类扩展 IDE。

 实现给定 **工具选项** 页的对象与对象相关联的特定 vspackage <xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute> 。

 因为当 IDE 显示特定页面时，环境将实现特定 " **工具选项** " 页的对象实例化：

- " **工具" 选项** 页应在其自己的对象上实现，而不是在实现 VSPackage 的对象上实现。

- 对象无法实现多个 **工具选项** 页。

## <a name="register-as-a-tools-options-page-provider"></a>注册为工具选项页提供程序
 通过 " **工具选项** " 页支持用户配置的 VSPackage 通过将应用的的实例应用于实现来指示提供这些 **工具选项** 页的对象 <xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute> <xref:Microsoft.VisualStudio.Shell.Package> 。

 <xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute>对于 <xref:Microsoft.VisualStudio.Shell.DialogPage> 实现 "**工具选项**" 页的每个派生类型，必须有一个实例。

 的每个实例都 <xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute> 使用实现 " **工具选项** " 页的类型、包含用于标识 " **工具选项** " 页的类别和子类别的字符串，以及用于将类型注册为 "提供 **工具选项** " 页的资源信息。

## <a name="persist-tools-options-page-state"></a>持久性工具选项页状态
 如果已在启用自动化支持的情况下为 " **工具选项** " 页实现注册，IDE 将保留页面的状态以及所有其他 " **工具选项** " 页。

 VSPackage 可以使用管理自己的持久性 <xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute> 。 只应使用一个持久性方法。

## <a name="implement-dialogpage-class"></a>实现 Dialogpage 派生类
 提供 VSPackage 的派生类型实现的对象 <xref:Microsoft.VisualStudio.Shell.DialogPage> 可以利用以下继承功能：

- 默认用户界面窗口。

- 如果 <xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute> 应用于类，或者如果 <xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute.SupportsProfiles%2A> 将应用于类的属性设置为，则可以使用默认的持久性机制 `true` <xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute> 。

- 自动化支持。

  使用实现 " **工具选项** " 页的对象的最低要求 <xref:Microsoft.VisualStudio.Shell.DialogPage> 是添加了公共属性。

  如果类正确地注册为 "**工具选项**" 页提供程序，则其公共属性可在 "**工具**" 菜单的 "**选项**" 部分中以 "属性" 网格的形式提供。

  所有这些默认功能都可以重写。 例如，若要创建更复杂的用户界面，只需重写的默认实现 <xref:Microsoft.VisualStudio.Shell.DialogPage.Window%2A> 。

## <a name="example"></a>示例
 下面是一个简单的 "Hello world" 选项页实现。 将以下代码添加到 Visual Studio 包模板创建的默认项目，并选择 " **菜单命令** " 选项，可充分说明选项页面功能。

### <a name="description"></a>描述
 下面的类定义最小的 "Hello world" 选项页。 当打开时，用户可以 `HelloWorld` 在属性网格中设置公共属性。

### <a name="code"></a>代码
 [!code-csharp[UI_UserSettings_ToolsOptionPages#11](../../extensibility/internals/codesnippet/CSharp/creating-options-pages_1.cs)]
 [!code-vb[UI_UserSettings_ToolsOptionPages#11](../../extensibility/internals/codesnippet/VisualBasic/creating-options-pages_1.vb)]

### <a name="description"></a>说明
 将以下特性应用于 package 类可使选项页在包加载时可用。 这些数字是类别和页面的任意资源 Id，末尾的布尔值指定页面是否支持自动化。

### <a name="code"></a>代码
 [!code-csharp[UI_UserSettings_ToolsOptionPages#07](../../extensibility/internals/codesnippet/CSharp/creating-options-pages_2.cs)]
 [!code-vb[UI_UserSettings_ToolsOptionPages#07](../../extensibility/internals/codesnippet/VisualBasic/creating-options-pages_2.vb)]

### <a name="description"></a>说明
 下面的事件处理程序将根据在 "选项" 页中设置的属性的值来显示结果。 它使用 <xref:Microsoft.VisualStudio.Shell.Package.GetDialogPage%2A> 方法，将结果显式强制转换为自定义选项页类型，以访问由该页公开的属性。

 对于包模板生成的项目，请从函数中调用此函数， `MenuItemCallback` 以将其附加到添加到 " **工具** " 菜单的默认命令。

### <a name="code"></a>代码
 [!code-csharp[UI_UserSettings_ToolsOptionPages#08](../../extensibility/internals/codesnippet/CSharp/creating-options-pages_3.cs)]
 [!code-vb[UI_UserSettings_ToolsOptionPages#08](../../extensibility/internals/codesnippet/VisualBasic/creating-options-pages_3.vb)]

## <a name="see-also"></a>请参阅
- [扩展用户设置和选项](../../extensibility/extending-user-settings-and-options.md)
- ["选项" 页的自动化支持](../../extensibility/internals/automation-support-for-options-pages.md)
