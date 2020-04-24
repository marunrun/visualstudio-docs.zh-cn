---
title: 如何运行 C# 程序
description: 初学者指南介绍如何在 Visual Studio 中运行 C# 程序。
ms.custom: get-started
ms.date: 10/16/2019
ms.technology: vs-ide-general
ms.prod: visual-studio-windows
ms.topic: tutorial
ms.devlang: CSharp
author: ghogen
ms.author: ghogen
manager: jillfra
dev_langs:
- CSharp
ms.workload:
- dotnet
- dotnetcore
ms.openlocfilehash: ee28bde6de10006ccfdc5175cca629ad9d1590d0
ms.sourcegitcommit: ade07bd1cf69b8b494d171ae648cfdd54f7800d3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81649639"
---
# <a name="how-to-run-a-c-program-in-visual-studio"></a>如何：在 Visual Studio 中运行 C# 程序

运行程序所需执行的操作取决于从哪里启动，程序、应用或服务是什么类型，以及是否要在调试器下运行它。 在最简单的情况下，如果要在 Visual Studio 中打开项目，可按 Ctrl+F5（启动时不进行调试）或 F5（启动进行调试），或按下 Visual Studio 主工具栏上的绿色箭头（启动按钮）来生成并运行该项目       。

![此屏幕截图显示启动按钮](media/vs-start-button.png)

## <a name="starting-from-a-project"></a>从项目启动

如果你有一个 C# 项目（.csproj 文件），则可以运行它（如果它是可运行的程序）  。 如果项目包含带有 `Main` 方法的 C# 文件，并且其输出为可执行文件 (EXE)，则很可能会在项目成功生成后运行该项目。

如果 Visual Studio 某个项目中已有程序的代码，请打开该项目。 若要打开项目，请在“Windows 文件资源管理器”中双击或点击 .csproj，或在 Visual Studio 中，选择“打开项目”，浏览查找项目 (.csproj) 文件，然后选择项目文件    。

在 Visual Studio 中加载项目后，按 Ctrl+F5（启动时不进行调试）或 F5（启动时进行调试）或使用 Visual Studio 工具栏上的绿色“启动”按钮来运行程序     。  如果有多个项目，则必须将具有 `Main` 方法的项目设置为启动项目。 若要设置启动项目，请右键单击项目节点，然后选择“设为启动项目”  。

![设置启动项目](media/set-as-startup-project.png)

Visual Studio 会尝试生成并运行项目。  如果出现生成错误，则会在“输出”窗口中看到生成输出，在“错误列表”窗口中看到错误   。

如果生成成功，则应用会以适合项目类型的方式运行。 控制台应用在终端窗口中运行，Windows 桌面应用在新窗口中启动，Web 应用在浏览器中启动（由 IIS Express 托管），依此类推。

## <a name="starting-from-code"></a>从代码启动

如果是从代码列表、代码文件或少量文件启动，请首先确保要运行的代码来自受信任的源，并且是可运行的程序。 如果它具有 `Main` 方法，则很可能是一个可运行程序：可以使用控制台应用程序模板创建一个项目，在 Visual Studio 中使用该程序。

### <a name="code-listing-for-a-single-file"></a>单个文件的代码列表

启动 Visual Studio，打开一个空的 C# 控制台项目，选择项目中已存在的 .cs 文件中的所有代码，然后删除。 然后将代码的内容粘贴到 .cs 文件中。 粘贴代码时，请覆盖或删除以前存在的代码。 重命名该文件以匹配原始代码。

### <a name="code-listings-for-a-few-files"></a>一些文件的代码列表

启动 Visual Studio，打开一个空的 C# 控制台项目，选择项目中已存在的 .cs 文件中的所有代码，然后删除。 然后将第一个代码文件的内容粘贴到 .cs 文件中。 重命名该文件以匹配原始代码。 

对于第二个文件，请右键单击“解决方案资源管理器”中的项目节点，打开该项目的快捷菜单，然后选择“添加”>“现有项”（或使用组合键 Shift+Alt+A），并选择代码文件      。

### <a name="multiple-files-on-disk"></a>磁盘上的多个文件

1. 创建适当类型的新项目（如果不确定，请使用 C# 控制台应用  ）。

2. 右键单击项目节点，选择“添加” > “现有项”，然后选择文件并将其导入到项目中   。  

### <a name="starting-from-a-folder"></a>从文件夹启动

处理具有多个文件的文件夹时，首先查看是否存在项目或解决方案。  如果程序是使用 Visual Studio 创建的，则应查找项目文件或解决方案文件。 查找带有 .csproj 扩展名或 .sln 扩展名的文件，并在 Windows 文件资源管理器中双击其中一个文件，在 Visual Studio 中将其打开  。 请参阅[从 Visual Studio 解决方案或项目启动](#starting-from-a-project)。

如果没有项目文件（如代码是在其他开发环境中开发的），则使用 Visual Studio 中的“打开文件夹”方法打开顶级文件夹  。 请参阅[开发代码而无需创建项目或解决方案](../../ide/develop-code-in-visual-studio-without-projects-or-solutions.md)。

## <a name="starting-from-a-github-or-azure-devops-repo"></a>从 GitHub 或 Azure DevOps 存储库启动

如果要运行的代码位于 GitHub 或 Azure DevOps 存储库中，则可以使用 Visual Studio 直接从存储库打开项目。 请参阅[打开存储库中的项目](../tutorial-open-project-from-repo.md)。

## <a name="run-the-program"></a>运行程序

若要启动该程序，请按 Visual Studio 主工具栏上的绿色箭头（“启动”按钮），或按 F5 或 Ctrl+F5 以运行该程序     。 使用“启动”按钮时，它将在调试器下运行  。  Visual Studio 会尝试在你的项目中生成代码并运行它。  如果成功，那很好！ 但如果没有成功，请继续阅读有关如何使其成功生成的一些建议。

## <a name="troubleshooting"></a>疑难解答

你的代码可能有错误，但如果代码是正确的，且仅依赖于某些其他程序集或 NuGet 包，或是编写为面向其他版本的 .NET，那么有可能可以轻松解决。

### <a name="add-references"></a>添加引用

若要正确生成，代码必须正确，并正确设置了对库或其他依赖项的引用。 可以查看红色波浪线，并在“错误列表”中查看程序是否有任何错误，即使在编译和运行之前也可如此操作  。 如果看到与未解析名称相关的错误，则可能需要添加引用或 using 指令，或者同时添加两者。 如果代码引用了任何程序集或 NuGet 包，则需要在项目中添加这些引用。

Visual Studio 会尝试帮助你识别缺少的引用。 如果名称未解析，编辑器中会出现灯泡图标。 如果单击灯泡，可以看到有关如何解决此问题的一些建议。 解决方法可能是：

- 添加 using 指令
- 添加对程序集的引用，或
- 安装 NuGet 包。

#### <a name="missing-using-directive"></a>缺少 using 指令

例如，在下面的屏幕中，可以选择将 `using System;` 添加到代码文件的开头，对未解析名称 `Console` 进行解析：

![屏幕截图显示用于添加 using 指令的灯泡](media/name-does-not-exist2.png)

#### <a name="missing-assembly-reference"></a>缺少程序集引用

.NET 引用可以是程序集或 NuGet 包的形式。 通常情况下，如果找到源代码，发布者或作者将说明所需的程序集以及代码所依赖的包。 若要手动添加对项目的引用，请右键单击解决方案资源管理器中的“引用”节点，选择“添加引用”，然后找到所需的程序集    。

![“添加引用”菜单的屏幕截图](media/add-reference.png)

可以按照[使用引用管理器添加或删除引用](../../ide/how-to-add-or-remove-references-by-using-the-reference-manager.md)中的说明查找程序集并添加引用。

#### <a name="missing-nuget-package"></a>缺少 NuGet 包

如果 Visual Studio 检测到缺少 NuGet 包，则会出现一个灯泡，并提供安装的选项：

![屏幕截图显示用于安装包的灯泡](media/lightbulb-add-package.png)

如果这不能解决问题，并且 Visual Studio 找不到包，请尝试联机搜索。 请参阅[在 Visual Studio 中安装和使用 NuGet 包](/nuget/quickstart/install-and-use-a-package-in-visual-studio)。

## <a name="use-the-right-version-of-net"></a>使用正确版本的 .NET

由于 .NET Framework 的不同版本具有一定程度的向后兼容性，因此，较新的框架可能会运行为旧版框架编写的代码，而不进行任何修改。 但有时需要以特定的框架为目标。 可能需要安装 .NET Framework 或 .NET Core 的特定版本（如果尚未安装）。 请参阅[修改 Visual Studio](../../install/modify-visual-studio.md)。

若要更改目标框架，请参阅[更改目标框架](../../ide/visual-studio-multi-targeting-overview.md#select-a-target-framework-version)。 有关详细信息，请参阅 [.NET Framework 目标错误疑难解答](../../msbuild/troubleshooting-dotnet-framework-targeting-errors.md)。

## <a name="next-steps"></a>后续步骤

阅读[欢迎使用 Visual Studio IDE](../visual-studio-ide.md)，探索 Visual Studio 开发环境。

## <a name="see-also"></a>请参阅

[创建自己的第一个 C# 应用](tutorial-console.md)
