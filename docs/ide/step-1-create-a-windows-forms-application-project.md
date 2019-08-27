---
title: 步骤 1：创建 Windows 窗体应用程序项目
ms.date: 06/01/2019
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
ms.topic: conceptual
ms.assetid: 16ac2422-e720-4e3a-b511-bc2a54201a86
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 1b28b69f2a5f2b02c483c5d6813943297b13f173
ms.sourcegitcommit: aeb1a1135dd789551e15aa5124099a5fe3f0f32b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/04/2019
ms.locfileid: "66501059"
---
# <a name="step-1-create-a-windows-forms-application-project"></a>步骤 1：创建 Windows 窗体应用程序项目

创建图片查看器时，第一步是创建 Windows 窗体应用程序项目。

 > [!TIP]
 > ![视频链接](../data-tools/media/playvideo.gif)有关此主题的视频版本，请参阅[教程 1：在 Visual Basic 中创建图片查看器 - 视频 1](http://go.microsoft.com/fwlink/?LinkId=205209) 或[教程 1：在 C# 中创建图片查看器 - 视频 1](http://go.microsoft.com/fwlink/?LinkId=205199)。 这些视频使用 Visual Studio 的早期版本，因此在一些菜单命令和其他用户界面元素上略有差异。 但是，概念和过程与当前版本的 Visual Studio 大同小异。

::: moniker range="vs-2017"

## <a name="open-visual-studio-2017"></a>打开 Visual Studio 2017

1. 在菜单栏上，依次选择“文件”   > “新建”   > “项目”  。 对话框应如以下屏幕快照所示。

     ![“新建项目”对话框](../ide/media/newprojectdialogcallouts.png)<br/>“新建项目”对话框 

2. 在“新建项目”  对话框的左侧，选择 Visual C#  或 Visual Basic  ，然后选择“Windows 桌面”  。

3. 在模板列表中，选择“Windows 窗体应用(.NET Framework)”  。 将新窗体命名为“PictureViewer”，然后选择“确定”按钮。  

    >[!NOTE]
    >如果没有看到“Windows 窗体应用(.NET Framework)”模板，请使用 Visual Studio 安装程序安装“.NET 桌面开发”工作负载   。<br/><br/>![Visual Studio 安装程序中的 .NET 桌面开发工作负载](../ide/media/dot-net-desktop-dev-workload.png)<br/><br/> 有关详细信息，请参阅[安装 Visual Studio](../install/install-visual-studio.md) 页面。

::: moniker-end

::: moniker range="vs-2019"

## <a name="open-visual-studio-2019"></a>打开 Visual Studio 2019

1. 在“开始”窗口上，选择“创建新项目”  。

   ![查看“创建新项目”窗口](../get-started/media/vs-2019/create-new-project-dark-theme.png)

1. 在“创建新项目”  窗口的搜索框中输入或键入“Windows 窗体”  。 接下来，从“语言”列表中选择 Visual Basic，然后从“平台”列表中选择“Windows”   。

   应用语言和平台筛选器之后，选择“Windows 窗体应用(.NET Framework)”  模板，然后选择“下一步”  。

   ![为“Windows 窗体应用(.NET Framework)”选择 Visual Basic 模板](../get-started/visual-basic/media/vs-2019/vb-create-new-project-search-winforms-filtered.png)

   > [!NOTE]
   > 如果未看到“Windows 窗体应用(.NET Framework)”  模板，则可以通过“创建新项目”  窗口安装该模板。 在“找不到所需内容?”消息中，选择“安装更多工具和功能”链接   。
   >
   > ![“创建新项目”窗口内“找不到所需内容”消息中的“安装更多工具和功能”链接](../get-started/media/vs-2019/not-finding-what-looking-for.png)
   >
   > 接下来，在 Visual Studio 安装程序中，选择“.NET 桌面开发”  工作负载。
   >
   > ![Visual Studio 安装程序中的 .NET Core 开发工作负载](../ide/media/install-dot-net-desktop-env.png)
   >
   > 之后，在 Visual Studio 安装程序中选择“修改”按钮  。 系统可能会提示你保存所有内容；如果出现提示，请按照指示进行操作。 接下来，选择“继续”，以安装工作负载  。

1. 在“配置新项目”  窗口中，在“项目名称”  框中键入或输入“PictureViewer”  。 然后，选择“创建”  。

::: moniker-end

Visual Studio 将为您的程序创建解决方案。 解决方案充当程序所需全部项目和文件的容器。 本教程后面部分将详细解释这些术语。

## <a name="about-the-windows-forms-application-project"></a>Windows 窗体应用程序项目简介

1. 开发环境包含三个窗口：主窗口、“解决方案资源管理器”和“属性”窗口   。

     如果缺少其中任何一个窗口，请在菜单栏中选择“窗口”   > “重置窗口布局”  来还原默认的窗口布局。 您还可以通过使用菜单命令来显示各个窗口。 在菜单栏上，依次选择“视图”   > “属性窗口”  或“解决方案资源管理器”  。 如果任何其他窗口处于打开状态，请选择窗口右上角的“关闭”(x) 按钮将其关闭。 

    ::: moniker range="vs-2017"

    - **主窗口** 在此窗口中，可以完成大部分工作，如使用窗体和编辑代码。 窗口显示了“表单编辑器”中的一个表单  。 在窗口的顶部，显示有“起始页”选项卡和“Form1.cs [设计]”选项卡。   （在 Visual Basic 中，选项卡名称以 .vb  而非 .cs  结尾。）

    ::: moniker-end

    ::: moniker range=">=vs-2019"

    - **主窗口** 在此窗口中，可以完成大部分工作，如使用窗体和编辑代码。 窗口显示了“表单编辑器”中的一个表单  。

    ::: moniker-end

    - “解决方案资源管理器”窗口  在此窗口中，可以查看并导航到解决方案中的所有项。 选择某个文件时，“属性”窗口中的内容将发生更改。  如果打开某个代码文件（在 Visual C# 中以 .cs  结尾，在 Visual Basic 中以 .vb  结尾），则将显示该代码文件或用于该代码文件的设计器。 设计器是一种可视化图面，您可在上面添加按钮和列表等控件。 对于 Visual Studio 窗体，设计器称为“Windows 窗体设计器”  。

    - “属性”窗口  在此窗口中，可更改在其他窗口中选择的项的属性。 例如，如果选择 Form1，则可以通过设置“Text”属性更改其标题，还可以通过设置“Backcolor”属性更改背景色。  

    > [!NOTE]
    > **解决方案资源管理器**的顶行显示**解决方案 PictureViewer（1 个项目）** ，这意味着 Visual Studio 已为你创建一个解决方案。 一个解决方案可以包含多个项目，但现在，您将使用只包含一个项目的解决方案。

1. 在菜单栏上，依次选择“文件”   > “全部保存”  。

     或者，在工具栏上选择“全部保存”按钮，如下图所示。 

     ![“全部保存”工具栏按钮](../ide/media/express_iconsaveall.png)<br/>
     “全部保存”工具栏按钮  

     Visual Studio 将自动填充文件夹名称和项目名称，并将项目保存在项目文件夹中。

## <a name="to-continue-or-review"></a>继续或查看

- 要转到下一个教程步骤，请参阅[步骤 2：运行程序](../ide/step-2-run-your-program.md)。

- 要返回概述主题，请参阅[教程 1：创建图片查看器](../ide/tutorial-1-create-a-picture-viewer.md)。

## <a name="see-also"></a>请参阅

- [创建新的 Windows 窗体](/dotnet/framework/winforms/creating-a-new-windows-form/)
