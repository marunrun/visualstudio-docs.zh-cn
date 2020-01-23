---
title: 应用程序页上的 VB 项目属性
ms.date: 10/30/2018
ms.topic: reference
f1_keywords:
- vb.ProjectPropertiesApplicationWPF
- vb.ProjectPropertiesApplication
helpviewer_keywords:
- Project Designer, Application page
- Application page in Project Designer
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: fe303f86b282e7e803dacc1dd8f4d3c1d6b72121
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75595808"
---
# <a name="application-page-project-designer-visual-basic"></a>Application Page, Project Designer (Visual Basic)

使用项目设计器的“应用程序”  页可指定项目的应用程序设置和属性。

若要访问“应用程序”  页，请在**解决方案资源管理器**中选择项目节点（而非“解决方案”  节点）。 然后在菜单栏上依次选择“项目”   > “属性”  。 当“项目设计器”出现时，选择“应用程序”选项卡   。

[!INCLUDE[note_settings_general](../../data-tools/includes/note_settings_general_md.md)]

## <a name="general-application-settings"></a>常规应用程序设置

以下选项用于配置应用程序的常规设置。

### <a name="assembly-name"></a>程序集名称

指定将包含程序集清单的输出文件的名称。 如果更改此属性，“输出名称”  属性也会随之更改。

此外，还可以使用 [/out (Visual Basic)](/dotnet/visual-basic/reference/command-line-compiler/out) 编译器开关，通过命令提示符指定输出文件名。

有关如何以编程方式访问此属性的信息，请参阅 <xref:VSLangProj.ProjectProperties.AssemblyName%2A>。

### <a name="root-namespace"></a>根命名空间

指定项目中所有文件的基命名空间。 例如，如果将“根命名空间”  设置为 `Project1`，并且在代码中的任何命名空间外有 `Class1`，则其命名空间为 `Project1.Class1`。 如果代码中的命名空间 `Class2` 内有 `Order`，则其命名空间为 `Project1.Order.Class2`。

如果清除“根命名空间”  ，则可以在代码中指定项目的命名空间结构。

> [!NOTE]
> 如果在 [Namespace 语句](/dotnet/visual-basic/language-reference/statements/namespace-statement)中使用 `Global` 关键字，则可以在项目的根命名空间外部定义命名空间。 如果清除“根命名空间”  ，无需在 `Namespace` 语句中使用 `Global` 关键字，`Global` 便可成为顶级命名空间。 有关详细信息，请参阅 [Visual Basic 中的命名空间](/dotnet/visual-basic/programming-guide/program-structure/namespaces)中的“Namespace 语句中的 Global 关键字”。

有关如何在代码中创建命名空间的信息，请参阅 [Namespace 语句](/dotnet/visual-basic/language-reference/statements/namespace-statement)。

有关根命名空间属性的详细信息，请参阅 [/rootnamespace](/dotnet/visual-basic/reference/command-line-compiler/rootnamespace)。

有关如何以编程方式访问此属性的信息，请参阅 <xref:VSLangProj.ProjectProperties.RootNamespace%2A>。

### <a name="target-framework-all-configurations"></a>目标框架（所有配置）

指定应用程序面向的 .NET 版本。 此选项可以有不同的值，具体取决于计算机上安装的 .NET 版本。

对于 .NET Framework 项目，默认值与创建项目时指定的目标框架一致。

> [!NOTE]
> 第一次打开对话框时将自动设置[“系统必备”对话框](../../ide/reference/prerequisites-dialog-box.md)中所列的必备组件包。 如果随后更改项目的目标框架，则必须手动指定必备组件，以便与新目标框架相匹配。

有关详细信息，请参阅[框架定位概述](../../ide/visual-studio-multi-targeting-overview.md)。

### <a name="application-type"></a>应用程序类型

指定要生成的应用程序类型。 值因项目类型而异。 例如，对于“Windows 窗体应用”项目，可以指定“Windows 窗体应用程序”、“类库”、“控制台应用程序”、“Windows 服务”或“Web 控件库”       。

对于 Web 应用程序项目，必须指定“类库”  。

有关“应用程序类型”  属性的详细信息，请参阅 [/target (Visual Basic)](/dotnet/visual-basic/reference/command-line-compiler/target)。 有关如何以编程方式访问此属性的信息，请参阅 <xref:VSLangProj.ProjectProperties.OutputType%2A>。

### <a name="auto-generate-binding-redirects"></a>自动生成绑定重定向

如果应用或其组件引用同一程序集的多个版本，则绑定重定向将添加到项目中。 如果要在项目文件中手动定义绑定重定向，请取消选中“自动生成绑定重定向”  。

有关重定向的详细信息，请参阅[重定向程序集版本](/dotnet/framework/configure-apps/redirect-assembly-versions)。

### <a name="startup-form--startup-object--startup-uri"></a>启动窗体/启动对象/启动 URI

指定应用程序的启动窗体或入口点。

如果“启用应用程序框架”  处于选中状态（默认设置），则此列表的标题为“启动窗体”  ，并且仅显示窗体，因为应用程序框架仅支持启动窗体，不支持对象。

如果项目是 WPF 浏览器应用程序，则此列表的标题为“启动 URI”  ，默认值为“Page1.xaml”  。 “启动 URI”  列表用于指定应用程序启动时显示的用户界面资源（一种 XAML 元素）。 有关详细信息，请参阅 <xref:System.Windows.Application.StartupUri%2A>。

如果“启用应用程序框架”  处于清除状态，则此列表将变为“启动对象”  ，并且同时显示窗体和带有 `Sub Main` 的类或模块。

“启动对象”  定义应用程序加载时要调用的入口点。 此选项通常设置为应用程序中的主窗体或当应用程序启动时应运行的 `Sub Main` 过程。 类库没有入口点，因此它们为此属性提供的唯一选项是“(无)”  。 有关详细信息，请参阅 [/main](/dotnet/visual-basic/reference/command-line-compiler/main)。 若要以编程方式访问此属性，请参阅 <xref:VSLangProj.ProjectProperties.StartupObject%2A>。

### <a name="icon"></a>图标

设置要用作程序图标的 .ico 文件。 选择“\<浏览...>”  以浏览现有图形。 有关详细信息，请参阅 [/win32icon](/dotnet/visual-basic/reference/command-line-compiler/win32icon)（或 [/win32icon（C# 编译器选项）](/dotnet/csharp/language-reference/compiler-options/win32icon-compiler-option)）。 若要以编程方式访问此属性，请参阅 <xref:VSLangProj.ProjectProperties.ApplicationIcon%2A>。

### <a name="assembly-information"></a>程序集信息

单击此按钮以显示[“程序集信息”对话框](../../ide/reference/assembly-information-dialog-box.md)。

### <a name="enable-application-framework"></a>启用应用程序框架

指定项目是否使用应用程序框架。 此选项的设置会影响“启动窗体”  /“启动对象”  中可用的选项。

如果选中此复选框，应用程序会使用标准 `Sub Main`。 选中此复选框将启用“Windows 应用程序框架属性”  节中的功能，同时会要求选择启动窗体。

如果清除此复选框，应用程序会使用“启动窗体”  中指定的自定义 `Sub Main`。 在此情况下，可以指定启动对象（方法或类中的自定义 `Sub Main`）或窗体。 与此同时，“Windows 应用程序框架属性”  节中的选项变为不可用。

### <a name="view-windows-settings"></a>查看 Windows 设置

单击此按钮以生成并打开 app.manifest 文件  。 Visual Studio 使用此文件生成应用程序的清单数据。 然后通过修改 app.manifest 中的 `<requestedExecutionLevel>` 标记来设置 UAC 请求的执行级别，如下所示  ：

`<requestedExecutionLevel level="asInvoker" />`

ClickOnce 在 `asInvoker` 级别或虚拟化模式下运行（无清单生成）。 若要指定虚拟化模式，请从 app.manifest 中删除整个标记。

有关清单生成的详细信息，请参阅 [Windows Vista 上的 ClickOnce 部署](../../deployment/clickonce-deployment-on-windows-vista.md)。

## <a name="windows-application-framework-properties"></a>Windows 应用程序框架属性

“Windows 应用程序框架属性”  节提供以下设置。 仅当“启用应用程序框架”  复选框处于选中状态时，这些选项才可用。

> [!TIP]
> 本部分后面的一节介绍了特定于 Windows Presentation Foundation (WPF) 应用的“Windows 应用程序框架属性”设置  。

### <a name="enable-xp-visual-styles"></a>启用 XP 视觉样式

启用或禁用 Windows XP 视觉样式，也称为 *Windows XP 主题*。 Windows XP 视觉样式可启用一些控件，例如带有圆角和动态颜色的控件。 默认为已启用。

### <a name="make-single-instance-application"></a>生成一个实例应用程序

选中此复选框可防止用户运行应用程序的多个实例。 此复选框默认处于清除  状态，这样就可以运行多个应用程序实例了。 有关详细信息，请参阅 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.StartupNextInstance> 事件。

### <a name="save-mysettings-on-shutdown"></a>关闭时保存 My.Settings

选中此复选框以指定用户关闭其计算机时保存应用程序的 `My.Settings` 设置。 默认设置为已启用。 如果此选项处于禁用状态，可通过调用 `My.Settings.Save` 手动保存应用程序设置。

### <a name="authentication-mode"></a>身份验证模式

选择“Windows”  （默认值）以指定使用 Windows 身份验证来标识当前登录的用户。 可以使用 `My.User` 对象在运行时检索此信息。 如果要提供自己的代码来对用户进行身份验证，而不是使用默认的 Windows 身份验证方法，则选择“由应用程序定义”  。

### <a name="shutdown-mode"></a>关闭模式

选择“当启动窗体关闭时”  （默认值）以指定应用程序在设置为启动窗体的窗体关闭时退出，即使其他窗体处于打开状态也是如此。 选择“当最后一个窗体关闭时”  以指定应用程序在最后一个窗体关闭或者显式调用 `My.Application.Exit` 或 `End` 语句时退出。

选择“在显式关闭时”  以指定应用程序在用户显式调用 `Shutdown` 时退出。

选择“在最后一个窗口关闭时”  以指定应用程序在最后一个窗口关闭或者用户显式调用 `Shutdown` 时退出。 此为默认设置。

选择“在主窗口关闭时”  以指定应用程序在主窗口关闭或者用户显式调用 `Shutdown` 时退出。

### <a name="splash-screen"></a>初始屏幕

选择要用作初始屏幕的窗体。 之前必须使用过窗体或模板来创建初始屏幕。 默认值为“(无)”  。

### <a name="view-application-events"></a>查看应用程序事件

单击此按钮以显示可以在其中为应用程序框架事件 `Startup`、`Shutdown`、`UnhandledException`、`StartupNextInstance` 和 `NetworkAvailabilityChanged` 写入事件的事件代码文件。 还可以重写某些应用程序框架方法。 例如，可以通过重写 `OnInitialize` 来更改初始屏幕的显示行为。

## <a name="windows-application-framework-properties-for-windows-presentation-foundation-wpf-apps"></a>Windows Presentation Foundation (WPF) 应用的 Windows 应用程序框架属性

当项目为 Windows Presentation Foundation (WPF) 应用时，“Windows 应用程序框架属性”部分提供以下设置  。 仅当“启用应用程序框架”  复选框处于选中状态时，这些选项才可用。 此表中列出的选项仅适用于 WPF 或 WPF 浏览器应用程序。 不适用于 WPF 用户控件或自定义控件库。

### <a name="shutdown-mode"></a>关闭模式

此属性仅适用于 Windows Presentation Foundation (WPF) 应用程序。

选择“在显式关闭时”  以指定应用程序在用户显式调用 <xref:System.Windows.Application.Shutdown%2A> 时退出。

选择“在最后一个窗口关闭时”  以指定应用程序在最后一个窗口关闭或者用户显式调用 <xref:System.Windows.Application.Shutdown%2A> 时退出。 此为默认设置。

选择“在主窗口关闭时”  以指定应用程序在主窗口关闭或者用户显式调用 <xref:System.Windows.Application.Shutdown%2A> 时退出。

有关使用此设置的详细信息，请参阅 <xref:System.Windows.Application.Shutdown%2A>

### <a name="edit-xaml"></a>编辑 XAML

此按钮在 XAML 编辑器中打开应用程序定义文件 (Application.xaml)。 单击此按钮时，Application.xaml 将在应用程序定义节点处打开  。 可能需要编辑此文件才能执行某些任务，例如定义资源。 如果应用程序定义文件不存在，项目设计器将创建一个。

### <a name="view-application-events"></a>查看应用程序事件

此按钮在代码编辑器中显示 `Application` 类文件 (Application.xaml.vb  )。 如果该文件不存在，项目设计器将创建一个具有适当类名和命名空间的此类文件。

<xref:System.Windows.Application> 对象在应用程序状态出现某些变化时（例如，在应用程序启动或关闭时）引发事件。 有关此类公开的事件的完整列表，请参阅 <xref:System.Windows.Application>。 这些事件在 `Application` 分部类的用户代码节中进行处理。
