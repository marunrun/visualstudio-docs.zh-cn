---
title: “项目设计器”->“应用程序”页 (C#) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- cs.ProjectPropertiesApplicationWPF
- cs.ProjectPropertiesApplication
helpviewer_keywords:
- Project Designer, Application page
- Application page in Project Designer
ms.assetid: f13701a8-4e2e-4474-9d60-bb43decbe0c1
caps.latest.revision: 61
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 792034d913bc7e3ca897f4f8e12736d4d78797cf
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72651708"
---
# <a name="application-page-project-designer-c"></a>“项目设计器”->“应用程序”页 (C#)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

使用“项目设计器”  的“应用程序”  页指定项目的应用程序设置和属性。

 若要访问“应用程序”  页，请在**解决方案资源管理器**中选择项目节点（而非“解决方案”  节点）。 然后在菜单栏上依次选择“项目”  、“属性”  。 当项目设计器出现时，单击“应用程序”  选项卡。

 [!INCLUDE[note_settings_general](../../includes/note-settings-general-md.md)]

## <a name="general-application-settings"></a>常规应用程序设置
 以下选项用于配置应用程序的常规设置。

 **程序集名称**指定将保存程序集清单的输出文件的名称。 更改此属性也将更改“输出名称”  属性。 也可以使用 [/out（C# 编译器选项）](https://msdn.microsoft.com/library/70d91d01-7bd2-4aea-ba8b-4e9807e9caa5)从命令行进行此更改。 若要以编程方式访问此属性，请参阅 <xref:VSLangProj.ProjectProperties.AssemblyName%2A>。

 **默认命名空间**为添加到项目中的文件指定基命名空间。

 有关在代码中创建命名空间的详细信息，请参阅[命名空间](https://msdn.microsoft.com/library/0a788423-9110-42e0-97d9-bda41ca4870f)。

 若要以编程方式访问此属性，请参阅 <xref:VSLangProj.ProjectProperties.RootNamespace%2A>。

 **目标框架**指定应用程序面向的 .NET Framework 版本。 此选项可以有不同的值，具体取决于计算机上安装的 .NET Framework 版本。

 默认情况下，该值与在“新建项目”  对话框中所选的目标框架相同。

> [!NOTE]
> 第一次打开对话框时将自动设置[“系统必备”对话框](../../ide/reference/prerequisites-dialog-box.md)中所列的必备组件包。 如果随后更改项目的目标框架，则必须手动选择必备组件，以便与新目标框架相匹配。

 有关详细信息，请参阅[如何：面向 .NET Framework 的某个版本](../../ide/how-to-target-a-version-of-the-dotnet-framework.md)和 [Visual Studio 多目标概述](../../ide/visual-studio-multi-targeting-overview.md)。

 **应用程序类型**指定要生成的应用程序类型。 对于 [!INCLUDE[win8_appname_long](../../includes/win8-appname-long-md.md)] 应用，可以指定“Windows 应用商店应用”  、“类库”  或“WinMD 文件”  。 对于其他大多数应用程序类型，可以指定“Windows 应用程序”  、“控制台应用程序”  、“类库”  、“Windows 服务”  或“Web 控件库”  。

 对于 Web 应用程序项目，必须指定“类库”  。

 如果指定“WinMD 文件”  选项，可以将类型投影到任何 Windows 运行时编程语言中。 通过将项目输出打包为 WinMD 文件，可以用多种语言编写应用程序代码，并让代码进行互操作，就像代码全部是用同一种语言编写的一样。 可以为面向 Windows 运行时库的解决方案（包括 [!INCLUDE[win8_appname_long](../../includes/win8-appname-long-md.md)] 应用）指定此选项。 有关详细信息，请参阅[用 C# 和 Visual Basic 创建 Windows 运行时组件](http://go.microsoft.com/fwlink/?LinkId=231895)。

> [!NOTE]
> Windows 运行时可以投影类型，使其在任何一种使用它们的语言中看起来都像本机对象一样。 例如，与 Windows 运行时交互的 JavaScript 应用程序将其用作一组 JavaScript 对象，而 C# 应用程序则将库用作一个 .NET 对象集合。 通过将项目输出打包为 WinMD 文件，可以充分利用 Windows 运行时所用的技术。

 有关“应用程序类型”  属性的详细信息，请参阅 [/target（C# 编译器选项）](https://msdn.microsoft.com/library/a18bbd8e-bbf7-49e7-992c-717d0eb1f76f)。 有关如何以编程方式访问此属性的信息，请参阅 <xref:VSLangProj.ProjectProperties.OutputType%2A>。

 **程序集信息**单击此按钮会显示[“程序集信息”对话框](../../ide/reference/assembly-information-dialog-box.md)。

 **启动对象**定义应用程序加载时要调用的入口点。 此选项通常设置为应用程序中的主窗体或当应用程序启动时应运行的 `Main` 过程。 类库没有入口点，因此它们为此属性提供的唯一选项是“(未设置)”  。

 默认情况下，在 WPF 浏览器应用程序项目中，此选项为“(未设置)”  。 另一个选项为 *Projectname*.App。 在此类项目中，必须将启动 URI 设置为当应用程序启动时加载 UI 资源。 若要执行此操作，请打开项目中的 Application.xaml 文件，并将 `StartupUri` 属性设置为项目中的 .xaml 文件，例如 Window1.xaml。 有关可接受的根元素的列表，请参阅 <xref:System.Windows.Application.StartupUri%2A>。 此外，还必须在项目的一个类中定义 `public static void Main()` 方法。 此类将在“启动对象”  列表中显示为 *ProjectName.ClassName*。 然后可以将该类选作启动对象。

 有关详细信息，请参阅 [/main（C# 编译器选项）](https://msdn.microsoft.com/library/975cf4d5-36ac-4530-826c-4aad0c7f2049)。 若要以编程方式访问此属性，请参阅 <xref:VSLangProj.ProjectProperties.StartupObject%2A>。

## <a name="resources"></a>资源
 以下选项用于配置应用程序的常规设置。

 **图标和清单**默认情况下，此单选按钮处于选中状态，“图标”和“清单”  选项处于启用状态  。 因此，你可以选择自己的图标，或选择不同的清单生成选项。 除非要为项目提供资源文件，否则请保留此单选按钮的选中状态。

 **图标**设置要用作程序图标的 .ico 文件。 单击省略号按钮浏览现有图形或键入所需文件的名称。 有关详细信息，请参阅 [/win32icon（C# 编译器选项）](https://msdn.microsoft.com/library/756d9b6d-ab07-41b7-ba58-5bd88f711138)。 若要以编程方式访问此属性，请参阅 <xref:VSLangProj.ProjectProperties.ApplicationIcon%2A>。

 **清单**当应用程序在 Windows Vista 上以用户帐户控制 (UAC) 模式运行时，选择一个清单生成选项。 此选项可以有下列值：

- **嵌入带默认设置的清单**。 支持 Visual Studio 在 Windows Vista 上的典型操作方式，即，将安全信息嵌入应用程序的可执行文件中，并指定 `requestedExecutionLevel` 为 `AsInvoker`。 这是默认选项。

- **创建不带清单的应用程序**。 此方法称为*虚拟化*。 若要与早期的应用程序兼容，则使用此选项。

- **Properties\app.manifest**。 此选项对通过 ClickOnce 或 Registration-Free COM 部署的应用程序而言是必需的。 如果通过使用 ClickOnce 部署发布应用程序，“清单”  会自动设置为此选项。

  **资源文件**若要为项目提供资源文件，则选中此单选按钮。 选择此选项会禁用“图标”  和“清单”  选项。

  输入路径名或使用“浏览”按钮 ( **...** )，以向项目添加 Win32 资源文件。

## <a name="see-also"></a>另请参阅
[管理应用程序属性](../../ide/application-properties.md) [在 Office 解决方案中编写代码](https://msdn.microsoft.com/library/2d4d8fd0-e881-4829-976f-0d1a9221dec0)
