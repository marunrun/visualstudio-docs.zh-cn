---
title: 创建选项页 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- managed package framework, creating Tools Options pages
- Tools Options pages [Visual Studio SDK], creating using managed package framework
ms.assetid: 1bf11fec-dece-4943-8053-6de1483c43eb
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 4d46055f14fdd1852e77ee78062548e5164140a3
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66340682"
---
# <a name="create-options-pages"></a>创建选项页
在中[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]托管的包框架类派生自<xref:Microsoft.VisualStudio.Shell.DialogPage>扩展[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]IDE，方法是添加**选项**页下**工具**菜单。

 一个对象，实现给定**工具选项**页是与特定的 Vspackage 相关联<xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute>对象。

 因为环境要实例化实现特定的对象**工具选项**页面时 IDE 将显示该特定页：

- 一个**工具选项**应实现页，在其自己的对象，而不是实现 VSPackage 的对象。

- 一个对象不能实现多个**工具选项**页。

## <a name="register-as-a-tools-options-page-provider"></a>注册为工具选项页上提供程序
 通过的 VSPackage 支持的用户配置**工具选项**页面指示的对象提供这些**工具选项**通过应用的实例的页面<xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute>应用于<xref:Microsoft.VisualStudio.Shell.Package>实现。

 必须有一个实例<xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute>为每个<xref:Microsoft.VisualStudio.Shell.DialogPage>的派生类型实现**工具选项**页。

 每个实例<xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute>使用实现的类型**工具选项**页上，包含的类别和子类别用于标识的字符串**工具选项**页和资源若要将该类型注册为提供的信息**工具选项**页。

## <a name="persist-tools-options-page-state"></a>保留工具选项页状态
 如果**工具选项**启用的自动化支持注册页的实现、 IDE 以及所有其他的页面的状态保持**工具选项**页。

 VSPackage 可以通过使用来管理其自己的持久性<xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute>。 应使用只有一个或另一个方法的持久性。

## <a name="implement-dialogpage-class"></a>实现 dialogpage 派生类
 对象提供的 VSPackage 的实现<xref:Microsoft.VisualStudio.Shell.DialogPage>的派生的类型可以利用以下继承的功能：

- 默认用户界面窗口。

- 一个默认持久性机制可用，或者如果<xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute>应用于类，或者如果<xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute.SupportsProfiles%2A>属性设置为`true`为<xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute>应用于类。

- 自动化的支持。

  一个对象，实现的最低要求**工具选项**页上使用<xref:Microsoft.VisualStudio.Shell.DialogPage>是添加了公共属性。

  如果作为正确注册的类**工具选项**页上提供程序，则其公共属性是可在上找到**选项**部分**工具**菜单中的窗体属性网格。

  可以重写所有这些默认的功能。 例如，若要创建更复杂的用户界面需要仅重写的默认实现<xref:Microsoft.VisualStudio.Shell.DialogPage.Window%2A>。

## <a name="example"></a>示例
 下面是将选项页的简单"Hello world"实现。 将以下代码添加到默认项目由与 Visual Studio 包模板创建**菜单命令**选项处于选中状态充分地演示选项页的功能。

### <a name="description"></a>描述
 下面的类定义最小"Hello world"选项页。 打开时，用户可以设置公共`HelloWorld`属性网格中的属性。

### <a name="code"></a>代码
 [!code-csharp[UI_UserSettings_ToolsOptionPages#11](../../extensibility/internals/codesnippet/CSharp/creating-options-pages_1.cs)]
 [!code-vb[UI_UserSettings_ToolsOptionPages#11](../../extensibility/internals/codesnippet/VisualBasic/creating-options-pages_1.vb)]

### <a name="description"></a>描述
 将以下特性应用于程序包类使页上的选项可加载包时。 数字是任意资源 Id 类别和页上，并在结束的布尔值指定页是否支持自动化。

### <a name="code"></a>代码
 [!code-csharp[UI_UserSettings_ToolsOptionPages#07](../../extensibility/internals/codesnippet/CSharp/creating-options-pages_2.cs)]
 [!code-vb[UI_UserSettings_ToolsOptionPages#07](../../extensibility/internals/codesnippet/VisualBasic/creating-options-pages_2.vb)]

### <a name="description"></a>描述
 以下事件处理程序显示的选项页中设置的属性取决于值的结果。 它使用<xref:Microsoft.VisualStudio.Shell.Package.GetDialogPage%2A>方法结果显式转换为自定义选项页类型，以访问页面所公开的属性。

 对于由包模板生成的项目，调用该函数从`MenuItemCallback`函数以将其附加到的默认命令添加到**工具**菜单。

### <a name="code"></a>代码
 [!code-csharp[UI_UserSettings_ToolsOptionPages#08](../../extensibility/internals/codesnippet/CSharp/creating-options-pages_3.cs)]
 [!code-vb[UI_UserSettings_ToolsOptionPages#08](../../extensibility/internals/codesnippet/VisualBasic/creating-options-pages_3.vb)]

## <a name="see-also"></a>请参阅
- [扩展用户设置和选项](../../extensibility/extending-user-settings-and-options.md)
- [选项页的自动化支持](../../extensibility/internals/automation-support-for-options-pages.md)