---
title: 演练：构建应用程序
ms.date: 09/25/2017
ms.technology: vs-ide-compile
ms.topic: conceptual
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 8964fc81b8323b6720d7c6d960449c7a9134658b
ms.sourcegitcommit: 59e5758036223ee866f3de5e3c0ab2b6dbae97b6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/23/2019
ms.locfileid: "68416898"
---
# <a name="walkthrough-build-an-application"></a>演练：构建应用程序

完成本演练后，你会更熟悉使用 Visual Studio 生成应用程序时可配置的多个选项。 将为示例应用程序创建自定义生成配置、隐藏特定警告消息以及增加生成输出信息。

## <a name="install-the-sample-application"></a>安装示例应用程序

下载 [Introduction to building WPF applications](https://code.msdn.microsoft.com/Introduction-to-Building-b8d16419)（生成 WPF 应用程序简介）示例。 选择 C# 或 Visual Basic。 下载 .zip 文件后，将它解压缩并使用 Visual Studio 打开 ExpenseItIntro.sln 文件   。

## <a name="create-a-custom-build-configuration"></a>创建自定义生成配置

创建解决方案时，调试和发布生成配置，并为解决方案自动定义它们的默认平台目标。 然后，可以自定义这些配置，或创建自己的配置。 生成配置指定生成类型。 生成平台指定应用程序为该配置定向的操作系统。 有关详细信息，请参阅[了解生成配置](../ide/understanding-build-configurations.md)、[了解生成平台](../ide/understanding-build-platforms.md)，以及[如何：设置调试和发布配置](../debugger/how-to-set-debug-and-release-configurations.md)。

可以使用“配置管理器”  对话框更改或创建配置和平台设置。 在此过程中将创建用于测试的生成配置。

### <a name="create-a-build-configuration"></a>创建生成配置

1. 打开“配置管理器”  对话框。

   ![“生成”菜单-&gt;“配置管理器”命令](../ide/media/buildwalk_configurationmanagerdialogbox.png)

1. 在“活动解决方案配置”  列表中，选择“\<新建...\>”  。

1. 在“新建解决方案配置”对话框中，命名新配置 `Test`，复制现有“调试”配置中的设置，然后选择“确定”按钮    。

   ![“新建解决方案配置”对话框](../ide/media/buildwalk_newsolutionconfigdlgbox.png)

1. 在“活动解决方案平台”  列表中，选择“\<新建...\>”  。

1. 在“新建解决方案平台”对话框中，选择“x64”，且不要复制 x86 平台中的设置   。

   ![“新建解决方案平台”对话框](../ide/media/buildwalk_newsolutionplatform.png)

1. 选择“确定”  按钮。

   “活动解决方案配置”已更改为“测试”，且“活动解决方案平台”设置为“x64”  。

   ![具有测试配置的配置管理器](../ide/media/buildwalk_configmanagertestconfig.png)

1. 选择“关闭”  。

使用“标准”  工具栏上的“解决方案配置”  列表，可快速验证或更改“活动解决方案配置”。

![解决方案配置选项标准工具栏](../ide/media/buildwalk_standardtoolbarsolutioncongfig.png)

## <a name="build-the-application"></a>生成应用程序

接下来将生成具有自定义生成配置的解决方案。

### <a name="build-the-solution"></a>生成解决方案

- 在菜单栏上，依次选择“生成” > “生成解决方案”   。

    “输出”  窗口将显示生成的结果。 成功生成。

## <a name="hide-compiler-warnings"></a>隐藏编译器警告

接下来将介绍一些会导致编译器生成警告的代码。

1. 在 C# 项目中，打开 ExpenseReportPage.xaml.cs  文件。 在 ExpenseReportPage  方法中，添加以下代码：`int i;`。

    或

    在 Visual Basic 项目中，打开 ExpenseReportPage.xaml.vb  文件。 在自定义的构造函数“Public Sub New...”  中，添加以下代码：`Dim i`。

1. 生成解决方案。

“输出”  窗口将显示生成的结果。 成功生成，但生成了警告：

![输出窗口 Visual Basic](../ide/media/buildwalk_vbbuildoutputwnd.png)

![输出窗口 Visual C#](../ide/media/buildwalk_csharpbuildoutputwnd.png)

可在生成期间暂时隐藏某些警告消息，而不是使其扰乱生成输出。

### <a name="hide-a-specific-c-warning"></a>隐藏特定的 C# 警告

1. 在“解决方案资源管理器”  中，选择顶级项目节点。

1. 在菜单栏上，依次选择“查看”   > “属性页”  。

     将打开“项目设计器”  。

1. 选择“生成”  页，然后在“禁止显示警告”  框中，指定警告编号“0168”  。

     ![“生成”页，“项目设计器”](../ide/media/buildwalk_csharpsuppresswarnings.png)

     有关详细信息，请参阅 [“项目设计器”->“生成”页 (C#)](../ide/reference/build-page-project-designer-csharp.md)。

1. 生成解决方案。

     “输出”  窗口仅显示生成的摘要信息。

     ![输出窗口 Visual C# 生成警告](../ide/media/buildwalk_visualcsharpbuildwarnings.png)

### <a name="suppress-all-visual-basic-build-warnings"></a>禁止显示所有 Visual Basic 生成警告

1. 在“解决方案资源管理器”  中，选择顶级项目节点。

2. 在菜单栏上，依次选择“查看”   > “属性页”  。

     将打开“项目设计器”  。

3. 在“编译”  页上，选择“禁用所有警告”  复选框。

     ![“编译”页，“项目设计器”](../ide/media/buildwalk_vbsuppresswarnings.png)

     有关详细信息，请参阅[在 Visual Basic 中配置警告](../ide/configuring-warnings-in-visual-basic.md)。

4. 生成解决方案。

   “输出”  窗口仅显示生成的摘要信息。

   ![输出窗口 Visual Basic 生成警告](../ide/media/buildwalk_visualbasicbuildwarnings.png)

   有关详细信息，请参阅[如何：取消编译器警告](../ide/how-to-suppress-compiler-warnings.md)。

## <a name="display-additional-build-details-in-the-output-window"></a>在“输出”窗口中显示其他生成详细信息

你可以更改“输出”  窗口中显示的关于生成过程的信息量。 生成详细程度通常设置为“最小”，这意味着，“输出”窗口仅显示生成过程的摘要以及任何高优先级的警告或错误   。 使用[“选项”对话框->“项目和解决方案”->“生成和运行”](../ide/reference/options-dialog-box-projects-and-solutions-build-and-run.md)，可显示有关生成的详细信息。

> [!IMPORTANT]
> 如果显示详细信息，生成将花费更长时间才能完成。

### <a name="change-the-amount-of-information-in-the-output-window"></a>更改“输出”窗口中的信息量

1. 打开“选项”  对话框。

     ![“工具”菜单上的“选项”命令](../ide/media/exploreide-toolsoptionsmenu.png)

1. 选择“项目和解决方案”  类别，然后选择“生成和运行”  页。

1. 在“MSBuild 项目生成输出详细信息”  列表中，选择“常规”  ，然后选择“确定”  按钮。

1. 在菜单栏上，依次选择“生成” > “清理解决方案”   。

1. 生成解决方案，然后查看“输出”  窗口中的信息。

     生成信息包括生成开始的时间（位于开头）和处理文件的顺序。 此信息还包括生成期间 Visual Studio 运行的实际的编译器语法。

     例如，在 C# 生成中，[/nowarn](/dotnet/visual-basic/reference/command-line-compiler/nowarn) 选项列出了本主题前面部分随其他三个警告一起指定的警告代码 1762  。

     在 Visual Basic 生成中，[/nowarn](/dotnet/visual-basic/reference/command-line-compiler/nowarn) 不包括要排除的特定警告，因此不会出现任何警告。

    > [!TIP]
    > 如果通过选择 Ctrl+F 键，显示“查找”对话框，则可以搜索“输出”窗口的内容     。

有关详细信息，请参阅[如何：查看、保存和配置生成日志文件](../ide/how-to-view-save-and-configure-build-log-files.md)。

## <a name="create-a-release-build"></a>创建版本生成

可以生成针对交付进行了优化的示例应用程序版本。 对于版本生成，需指定在启动生成前，将可执行文件复制到网络共享。

有关详细信息，请参阅[如何：更改生成输出目录](../ide/how-to-change-the-build-output-directory.md)和[在 Visual Studio 中生成和清理项目和解决方案](../ide/building-and-cleaning-projects-and-solutions-in-visual-studio.md)。

### <a name="specify-a-release-build-for-visual-basic"></a>指定 Visual Basic 的版本生成

1. 打开“项目设计器”  。

     ![“视图”菜单，“属性页”命令](../ide/media/buildwalk_viewpropertypages.png)

1. 选择“编译”  页。

1. 在“配置”  列表中，选择“版本”  。

1. 在“平台”  列表中，选择“x86”  。

1. 在“生成输出路径”  框中，指定网络路径。

     例如，你可以指定 `\\myserver\builds`。

    > [!IMPORTANT]
    > 可能会出现一个消息框，警告指定的网络共享位置可能不受信任。 如果信任指定的位置，请在消息框中选择“确定”按钮  。

1. 生成应用程序。

     ![“生成”菜单上的“生成解决方案”命令](../ide/media/exploreide-buildsolution.png)

### <a name="specify-a-release-build-for-c"></a>指定 C\# 的版本生成

1. 打开“项目设计器”  。

     ![“视图”菜单，“属性页”命令](../ide/media/buildwalk_viewpropertypages.png)

1. 选择“生成”页。 

1. 在“配置”  列表中，选择“版本”  。

1. 在“平台”  列表中，选择“x86”  。

1. 在“输出路径”  框中，指定网络路径。

     例如，可指定 `\\myserver\builds`。

    > [!IMPORTANT]
    > 可能会出现一个消息框，警告指定的网络共享位置可能不受信任。 如果信任指定的位置，请在消息框中选择“确定”按钮  。

1. 在“标准工具栏”  上，将解决方案配置设置为“发布”  ，将解决方案平台设置为“x86”  。

1. 生成应用程序。

     ![“生成”菜单上的“生成解决方案”命令](../ide/media/exploreide-buildsolution.png)

   可执行文件已复制到指定的网络路径。 其路径将为 `\\myserver\builds\\FileName.exe`。

祝贺你！ 已成功完成此演练。

## <a name="see-also"></a>请参阅

- [演练：生成项目 (C++)](/cpp/ide/walkthrough-building-a-project-cpp)
- [ASP.NET Web 应用程序项目预编译概述](/previous-versions/aspnet/aa983464\(v\=vs.110\))
- [演练：使用 MSBuild](../msbuild/walkthrough-using-msbuild.md)