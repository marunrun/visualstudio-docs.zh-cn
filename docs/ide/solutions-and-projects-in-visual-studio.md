---
title: 解决方案和项目
ms.date: 10/05/2017
ms.topic: conceptual
f1_keywords:
- vs.addnewitem
- vs.addnewsolutionitem
- vs.openproject
- vs.addexistingitem
- vs.addexistingsolutionitem
- vs.environment.projects
- vs.environment.solutions
- VS.SolutionExplorer
- VS.SolutionExplorer.Solutions
helpviewer_keywords:
- solutions [Visual Studio]
- projects [Visual Studio]
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 42a8dbc2fd9a6fc89b0be62271b048f8275a82b2
ms.sourcegitcommit: ba5e072c9fedeff625a1332f22dcf3644d019f51
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/31/2019
ms.locfileid: "66432210"
---
# <a name="solutions-and-projects-in-visual-studio"></a>Visual Studio 中的解决方案和项目

本文介绍了 Visual Studio 中的项目和解决方案的概念   。 它还简要介绍了如何创建新项目以及“解决方案资源管理器”工具窗口  。

> [!NOTE]
> 本主题适用于 Visual Studio  Windows 版。 对于 Visual Studio for Mac，请参阅 [Visual Studio for Mac 中的项目和解决方案](/visualstudio/mac/projects-and-solutions)。

## <a name="projects"></a>项目

在 Visual Studio 中创建应用、网站、插件等时，会从项目开始  。 在逻辑意义上，项目包含所有将编译到可执行文件、库或网站中的源代码文件、图标、图像、数据文件等。 项目还包含编译器设置以及程序将与之通信的各种服务或组件需要的其他配置文件。

> [!NOTE]
> 无需在 Visual Studio 中使用解决方案或项目来编辑、生成和调试代码。 只需在 Visual Studio 中打开包含源文件的文件夹并开始编辑。 有关详细信息，请参阅[在 Visual Studio 中开发代码而无需创建项目或解决方案](../ide/develop-code-in-visual-studio-without-projects-or-solutions.md)。

项目在扩展名为 .vbproj、.csproj 或 .vcxproj 等的 XML 文件中进行定义    。 此文件包含虚拟文件夹层次结构以及项目中所有项的路径。 它还包含生成设置。

> [!TIP]
> 若要在 Visual Studio 中查看项目文件的内容，请先卸载项目，方法是在“解决方案资源管理器”中选择项目名称，然后在上下文菜单（或右键单击菜单）中选择“卸载项目”   。 然后，再次打开上下文菜单，依次选择“编辑”、“项目名称” **\<\>** 。

在 Visual Studio 中，“解决方案资源管理器”使用项目文件来显示项目内容和设置  。 编译项目时，MSBuild 引擎会使用项目文件创建可执行文件。 还可以自定义项目以生成其他类型的输出。

## <a name="solutions"></a>解决方案

项目包含在解决方案中  。 尽管其名称如此，但解决方案并不是“答案”。 解决方案只是一个容器，用于包含一个或多个相关项目，以及生成信息、Visual Studio 窗口设置和不与特定项目关联的任何杂项文件。 解决方案由格式唯一的文本文件（扩展名 .sln）描述；不应对其进行手动编辑  。

Visual Studio 采用两种文件类型（.sln 和 .suo）来存储解决方案设置   ：

|扩展名|name|说明|
|---------------|----------|-----------------|
|.sln|Visual Studio 解决方案|将项目、项目项和解决方案项组织到解决方案中。|
|.suo|解决方案用户选项|存储用户级别设置和自定义项，如断点。|

## <a name="create-new-projects"></a>创建新项目

创建新项目最简单的方法是从特定类型的应用程序或网站的项目模板开始。 项目模板包含一组基本的预生成代码文件、配置文件、资产和设置。 可以在创建新项目的对话框中（“文件” > “新建” > “项目”）使用这些模板    。 有关详细信息，请参阅[在 Visual Studio 中创建新项目](create-new-project.md)和[创建解决方案和项目](../ide/creating-solutions-and-projects.md)。

如果你经常以某种方式自定义项目，则可以创建可用于从中创建新项目的自定义项目模板。 有关详细信息，请参阅[创建项目和项模板](../ide/creating-project-and-item-templates.md)。

创建新项目时，默认情况下会将其保存在 %USERPROFILE%\source\repos 中  。 可以在“工具” > “选项” > “项目和解决方案” > “位置”下的“项目位置”设置中更改此位置      。 有关详细信息，请参阅[项目和解决方案页的“选项”对话框](../ide/reference/projects-and-solutions-options-dialog-box.md)。

## <a name="solution-explorer"></a>“解决方案资源管理器”

创建新项目之后，可使用“解决方案资源管理器”  查看和管理项目和解决方案及其关联项。 下图显示具有一个包含两个项目的 C# 解决方案的解决方案资源管理器  ：

![“解决方案资源管理器”](../ide/media/vs2015_solution_explorer.png)

可以从“解决方案资源管理器”中的各种项目上的右键单击菜单中获取多个菜单命令  。 这些命令包括生成项目、管理 NuGet 包、添加引用、重命名文件和运行测试，此处仅举几例。 “解决方案资源管理器”顶部的工具栏具有用于从解决方案视图切换到文件夹视图、显示隐藏文件、折叠所有节点等的按钮  。

对于 ASP.NET Core 项目，你可以自定义如何将文件嵌套在“解决方案资源管理器”中  。 有关详细信息，请参阅[在解决方案资源管理器中自定义文件嵌套](file-nesting-solution-explorer.md)

## <a name="see-also"></a>请参阅

- [Visual Studio IDE](../get-started/visual-studio-ide.md)
- [项目和解决方案 (Visual Studio for Mac)](/visualstudio/mac/projects-and-solutions)
- [添加和删除项目项 (Visual Studio for Mac)](/visualstudio/mac/add-and-remove-project-items)
