---
title: 创建选项页 |微软文档
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
ms.openlocfilehash: 368efaa78a56723d4a72c482bea9ee739385127e
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80709149"
---
# <a name="create-options-pages"></a>创建选项页
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]在托管包框架中，通过在 **"工具"** 菜单[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]下添加 **"选项**"页来扩展 IDE 派生的<xref:Microsoft.VisualStudio.Shell.DialogPage>类。

 实现给定**工具选项**页的对象与<xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute>对象的特定 VS 包相关联。

 因为当 IDE 显示特定页面时，环境会实例化实现特定**工具选项**页的对象：

- **工具选项**页应在其自己的对象上实现，而不是在实现 VSPackage 的对象上实现。

- 对象无法实现多个**工具选项**页。

## <a name="register-as-a-tools-options-page-provider"></a>注册为工具选项页面提供程序
 通过**工具选项**页面支持用户配置的 VSPackage 通过应用应用于**Tools Options**<xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute><xref:Microsoft.VisualStudio.Shell.Package>实现的实例来指示提供这些工具选项页的对象。

 对于实现**工具选项**页的每个<xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute><xref:Microsoft.VisualStudio.Shell.DialogPage>派生类型，必须有一个实例。

 的每个<xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute>实例都使用实现 **"工具选项"** 页的类型、包含用于标识**工具选项**页的类别和子类别的字符串以及将类型注册为提供**工具选项**页的资源信息。

## <a name="persist-tools-options-page-state"></a>持久工具选项页面状态
 如果在启用了自动化支持后注册**了"工具选项"** 页实现，则 IDE 将保留页面的状态以及所有其他**工具选项**页。

 VSPackage 可以使用 管理自己的持久性<xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute>。 只应使用一种或另一种持久性方法。

## <a name="implement-dialogpage-class"></a>实现对话页类
 提供 VSPackage 实现<xref:Microsoft.VisualStudio.Shell.DialogPage>派生类型的对象可以利用以下继承功能：

- 默认用户界面窗口。

- 如果<xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute>应用于类，或者该<xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute.SupportsProfiles%2A>属性设置为`true`<xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute>应用于类的属性，则可用的默认持久性机制。

- 自动化支持。

  使用<xref:Microsoft.VisualStudio.Shell.DialogPage>实现**工具选项**页的对象的最低要求是添加公共属性。

  如果类正确注册为 **"工具选项"** 页提供程序，则其公共属性在 **"工具"** 菜单的 **"选项**"部分以属性网格的形式可用。

  所有这些默认功能都可以重写。 例如，要创建更复杂的用户界面，只需要重写 的<xref:Microsoft.VisualStudio.Shell.DialogPage.Window%2A>默认实现。

## <a name="example"></a>示例
 以下是选项页面的简单"Hello world"实现。 将以下代码添加到由 Visual Studio 程序包模板创建的默认项目中，并选择了 **"菜单命令"** 选项，这将充分演示选项页面功能。

### <a name="description"></a>描述
 以下类定义一个最小的"Hello world"选项页。 打开时，用户可以在属性网格中设置`HelloWorld`公共属性。

### <a name="code"></a>代码
 [!code-csharp[UI_UserSettings_ToolsOptionPages#11](../../extensibility/internals/codesnippet/CSharp/creating-options-pages_1.cs)]
 [!code-vb[UI_UserSettings_ToolsOptionPages#11](../../extensibility/internals/codesnippet/VisualBasic/creating-options-pages_1.vb)]

### <a name="description"></a>描述
 将以下属性应用于包类使选项页在加载包时可用。 数字是类别和页面的任意资源 ID，末尾的布尔值指定页面是否支持自动化。

### <a name="code"></a>代码
 [!code-csharp[UI_UserSettings_ToolsOptionPages#07](../../extensibility/internals/codesnippet/CSharp/creating-options-pages_2.cs)]
 [!code-vb[UI_UserSettings_ToolsOptionPages#07](../../extensibility/internals/codesnippet/VisualBasic/creating-options-pages_2.vb)]

### <a name="description"></a>描述
 以下事件处理程序显示的结果，具体取决于选项页中设置的属性的值。 它使用<xref:Microsoft.VisualStudio.Shell.Package.GetDialogPage%2A>该方法，结果显式转换为自定义选项页类型，以访问页面公开的属性。

 在包模板生成的项目中，从`MenuItemCallback`函数调用此函数以将其附加到添加到 **"工具"** 菜单的默认命令。

### <a name="code"></a>代码
 [!code-csharp[UI_UserSettings_ToolsOptionPages#08](../../extensibility/internals/codesnippet/CSharp/creating-options-pages_3.cs)]
 [!code-vb[UI_UserSettings_ToolsOptionPages#08](../../extensibility/internals/codesnippet/VisualBasic/creating-options-pages_3.vb)]

## <a name="see-also"></a>请参阅
- [扩展用户设置和选项](../../extensibility/extending-user-settings-and-options.md)
- [选项页的自动化支持](../../extensibility/internals/automation-support-for-options-pages.md)
