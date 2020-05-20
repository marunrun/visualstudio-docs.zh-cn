---
title: 应用程序页上的 C# 项目属性
ms.date: 10/30/2018
ms.topic: reference
f1_keywords:
- cs.ProjectPropertiesApplicationWPF
- cs.ProjectPropertiesApplication
helpviewer_keywords:
- Project Designer, Application page
- Application page in Project Designer
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: ef9a38fc13d0d9c9f6b912f4cb2b83971d105c29
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "75595821"
---
# <a name="application-page-project-designer-c"></a>“项目设计器”->“应用程序”页 (C#)

使用“项目设计器”的“应用程序”页指定项目的应用程序设置和属性。

若要访问“应用程序”页，请在**解决方案资源管理器**中选择项目节点（而非“解决方案”节点）。 然后在菜单栏上依次选择“项目”   > “属性”  。 当“项目设计器”  出现时，单击“应用程序”  选项卡。

[!INCLUDE[note_settings_general](../../data-tools/includes/note_settings_general_md.md)]

## <a name="general-application-settings"></a>常规应用程序设置

以下选项用于配置应用程序的常规设置。

**程序集名称**

指定将保存程序集清单的输出文件的名称。 更改此属性也将更改“输出名称”属性  。

也可以使用 [/out（C# 编译器选项）](/dotnet/csharp/language-reference/compiler-options/out-compiler-option)从命令行进行此更改。

若要以编程方式访问此属性，请参阅 <xref:VSLangProj.ProjectProperties.AssemblyName%2A>。

**默认命名空间**

为添加到项目中的文件指定基命名空间。

有关在代码中创建命名空间的详细信息，请参阅[命名空间](/dotnet/csharp/language-reference/keywords/namespace)。

若要以编程方式访问此属性，请参阅 <xref:VSLangProj.ProjectProperties.RootNamespace%2A>。

**目标框架**

指定应用程序面向的 .NET 版本。 此选项可以有不同的值，具体取决于计算机上安装的 .NET 版本。

对于 .NET Framework 项目，默认值与创建项目时指定的目标框架一致。

对于面向 .NET Core 的项目，可用版本将如下显示：

![.NET Core 项目的目标框架版本](../media/application-target-framework.png)

> [!NOTE]
> 第一次打开对话框时将自动设置[“系统必备”对话框](../../ide/reference/prerequisites-dialog-box.md)中所列的必备组件包。 如果随后更改项目的目标框架，则必须手动选择必备组件，以便与新目标框架相匹配。

有关详细信息，请参阅[框架定位概述](../../ide/visual-studio-multi-targeting-overview.md)。

**输出类型**

指定要生成的应用程序类型。 值因项目类型而异。 例如，对于“控制台应用”项目，可以指定“Windows 应用程序”、“控制台应用程序”或者“类库”作为输出类型     。

对于 Web 应用程序项目，必须指定“类库”  。

有关“输出类型”的详细信息，请参阅 [/target（C# 编译器选项）](/dotnet/csharp/language-reference/compiler-options/target-compiler-option)。

有关如何以编程方式访问此属性的信息，请参阅 <xref:VSLangProj.ProjectProperties.OutputType%2A>。

**自动生成绑定重定向**

如果应用或其组件引用同一程序集的多个版本，则绑定重定向将添加到项目中。 如果要在项目文件中手动定义绑定重定向，请取消选中“自动生成绑定重定向”  。

有关重定向的详细信息，请参阅[重定向程序集版本](/dotnet/framework/configure-apps/redirect-assembly-versions)。

**启动对象**

定义应用程序加载时要调用的入口点。 此选项通常设置为应用程序中的主窗体或当应用程序启动时应运行的 `Main` 过程。 类库没有入口点，因此它们为此属性提供的唯一选项是“(未设置)”  。

默认情况下，在 WPF 应用项目中，此选项设置为“(未设置)”  。 另一个选项为 \[projectname].App。 在 WPF 项目中，必须将启动 URI 设置为在应用程序启动时加载 UI 资源。 要执行此操作，请打开项目中的 Application.xaml 文件，并将 `StartupUri` 属性设置为项目中的 .xaml 文件，例如 Window1.xaml。 有关可接受的根元素的列表，请参阅 <xref:System.Windows.Application.StartupUri%2A>。 此外，还必须在项目的一个类中定义 `public static void Main()` 方法。 此类将在“启动对象”  列表中显示为 *ProjectName.ClassName*。 然后可以将该类选作启动对象。

有关详细信息，请参阅 [/main（C# 编译器选项）](/dotnet/csharp/language-reference/compiler-options/main-compiler-option)。 若要以编程方式访问此属性，请参阅 <xref:VSLangProj.ProjectProperties.StartupObject%2A>。

**程序集信息**

此按钮将打开[程序集信息](../../ide/reference/assembly-information-dialog-box.md)对话框。

## <a name="resources"></a>资源

“资源”选项可帮助你为应用配置资源设置  。

**图标和清单**

默认情况下，此单选按钮处于选中状态，“图标”  和“清单”  选项处于启用状态。 因此，你可以选择自己的图标，或选择不同的清单生成选项。 除非要为项目提供资源文件，否则请保留此单选按钮的选中状态。

**图标**

设置要用作程序图标的 .ico 文件  。 单击“浏览”按钮浏览现有图形或键入所需文件的名称  。 有关详细信息，请参阅 [/win32icon（C# 编译器选项）](/dotnet/csharp/language-reference/compiler-options/win32icon-compiler-option)。

若要以编程方式访问此属性，请参阅 <xref:VSLangProj.ProjectProperties.ApplicationIcon%2A>。

有关创建图标的信息，请参阅[图标的图像编辑器](/cpp/windows/image-editor-for-icons)。

**Manifest**

当应用程序在 Windows Vista 上以用户帐户控制 (UAC) 模式运行时，选择一个清单生成选项。 此选项可以有下列值：

- **嵌入带默认设置的清单**。 支持 Visual Studio 在 Windows Vista 上的典型操作方式，即，将安全信息嵌入应用程序的可执行文件中，并指定 `requestedExecutionLevel` 为 `AsInvoker`。 这是默认选项。

- **创建不带清单的应用程序**。 此方法称为*虚拟化*。 若要与早期的应用程序兼容，则使用此选项。

- **Properties\app.manifest**。 此选项对通过 ClickOnce 或 Registration-Free COM 部署的应用程序而言是必需的。 如果通过使用 ClickOnce 部署发布应用程序，“清单”  会自动设置为此选项。

**资源文件**

若要为项目提供资源文件，请选中此单选按钮。 选择此选项会禁用“图标”  和“清单”  选项。

输入路径名或使用“浏览”按钮 ( **...** )，以向项目添加 Win32 资源文件。

有关详细信息，请参阅[为 .NET 应用创建资源文件](/dotnet/framework/resources/creating-resource-files-for-desktop-apps)。
