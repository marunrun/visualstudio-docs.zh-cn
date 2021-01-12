---
title: 了解有关解决方案和项目的信息
description: 了解 Visual Studio 项目和解决方案、如何从模板创建新项目，以及如何在解决方案资源管理器中查看和管理项目。
ms.custom: SEO-VS-2020, contperf-fy21q2
ms.date: 12/31/2020
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
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 3b34d96f49370a71a63e986a79584caffbc00adf
ms.sourcegitcommit: d577818d3d8e365baa55c6108fa8159c46ed8b43
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2021
ms.locfileid: "97847053"
---
# <a name="solutions-and-projects-in-visual-studio"></a>Visual Studio 中的解决方案和项目

本页介绍了 Visual Studio 中的项目和解决方案的概念 。 它还简要介绍了“解决方案资源管理器”工具窗口以及如何创建新项目。

> [!NOTE]
> 本主题适用于 Visual Studio  Windows 版。 对于 Visual Studio for Mac，请参阅 [Visual Studio for Mac 中的项目和解决方案](/visualstudio/mac/projects-and-solutions)。

## <a name="projects"></a>项目

在 Visual Studio 中创建应用或网站时，请从项目开始。 从逻辑上讲，项目包含所有编译为可执行文件、库或网站的文件。 这些文件可以包括源代码、图标、图像、数据文件等。 项目还包含编译器设置以及程序将与之通信的各种服务或组件需要的其他配置文件。

### <a name="project-file"></a>项目文件

Visual Studio 使用 [MSBuild](../msbuild/msbuild.md) 生成解决方案中的每个项目，每个项目都包含一个 MSBuild 项目文件。 文件扩展名反映项目的类型（例如，C# 项目 (.csproj)、Visual Basic 项目 (.vbproj) 或数据库项目 (.dbproj)）。 项目文件是一个 XML 文档，其中包含 MSBuild 生成项目所需的所有信息和说明，包括内容、平台要求、版本控制信息、Web 服务器或数据库服务器设置以及要执行的任务。

项目文件基于 [MSBuild XML 架构](../msbuild/msbuild-project-file-schema-reference.md)。 要在 Visual Studio 中查看较新的 [SDK 样式项目文件](../msbuild/how-to-use-project-sdk.md)的内容，请在“解决方案资源管理器”中右键单击项目节点，然后选择“编辑 \<projectname\>”。 要查看该样式的 .NET Framework 和其他项目的内容，请先卸载该项目（右键单击“解决方案资源管理器”中的项目节点并选择“卸载项目” ）。 然后，右键单击该项目并选择“编辑 \<projectname\>”。

> [!NOTE]
> 无需在 Visual Studio 中使用解决方案或项目来编辑、生成和调试代码。 只需在 Visual Studio 中打开包含源文件的文件夹并开始编辑。 有关详细信息，请参阅[在 Visual Studio 中开发代码而无需创建项目或解决方案](../ide/develop-code-in-visual-studio-without-projects-or-solutions.md)。

### <a name="create-new-projects"></a>创建新项目

创建新项目的最简单方法是为所需的项目类型使用项目模板。 项目模板包含一组基本的预生成代码文件、配置文件、资产和设置。 使用“文件” > “新建” > “项目”，选择一个项目模板  。 有关详细信息，请参阅[创建新项目](create-new-project.md)。

你也可以创建自定义项目模板，可基于该模板创建新项目。 有关详细信息，请参阅[创建项目和项模板](../ide/creating-project-and-item-templates.md)。

创建新项目时，Visual Studio 会将其保存到默认位置 %USERPROFILE%\source\repos。 若要更改此位置，请转到“工具” > “选项” > “项目和解决方案” > “位置”   。 有关详细信息，请参阅[“选项”对话框：“项目和解决方案”>“位置”](./reference/projects-solutions-locations-options.md)。

## <a name="solutions"></a>解决方案

项目包含在解决方案中。 尽管其名称如此，但解决方案并不是“答案”。 解决方案只是一个容器，用于包含一个或多个相关项目，以及生成信息、Visual Studio 窗口设置和不与特定项目关联的任何杂项文件。

### <a name="solution-file"></a>解决方案文件

Visual Studio 采用两种文件类型（.sln 和 .suo）来存储解决方案设置 ：

|扩展名|“属性”|描述|
|---------------|----------|-----------------|
|.sln|Visual Studio 解决方案|将项目、项目项和解决方案项组织到解决方案中。|
|.suo|解决方案用户选项|存储用户级别设置和自定义项，如断点。|

> [!IMPORTANT]
> 解决方案由格式唯一的文本文件（扩展名 .sln）描述；不应对其进行手动编辑。 相反，.suo 文件是隐藏文件，在默认的文件资源管理器设置下不会显示。 若要显示隐藏文件，请在文件资源管理器的“查看”菜单上选中“隐藏项”复选框。

### <a name="solution-folder"></a>解决方案文件夹

“解决方案文件夹”是仅存在于“解决方案资源管理器”中的虚拟文件夹，你可以在其中使用它对解决方案中的项目进行分组。 如果要在计算机上查找解决方案文件，请转到“工具” > “选项” > “项目和解决方案” > “位置”。 有关详细信息，请参阅[“选项”对话框：“项目和解决方案”>“位置”](./reference/projects-solutions-locations-options.md)。

> [!TIP]
> 关于从头开始创建的项目和解决方案的示例，包括分步说明和示例代码，请参阅[项目和解决方案简介](../get-started/tutorial-projects-solutions.md)。

## <a name="solution-explorer"></a>“解决方案资源管理器”

创建新项目之后，可使用“解决方案资源管理器”查看和管理项目和解决方案及其关联项。 下图显示具有一个包含两个项目的 C# 解决方案的解决方案资源管理器：

::: moniker range="vs-2017"

![包含两个项目的解决方案资源管理器的屏幕截图。](../ide/media/vs2015_solution_explorer.png)

“解决方案资源管理器”顶部的工具栏具有用于从解决方案视图切换到文件夹视图、显示隐藏文件、折叠所有节点等的按钮。

::: moniker-end

::: moniker range="vs-2019"

![Visual Studio 2019 中包含两个项目的解决方案资源管理器的屏幕截图。](../ide/media/solution-explorer.png)

“解决方案资源管理器”顶部的工具栏上带有按钮，可用于从解决方案视图切换到文件夹视图、筛选挂起的更改、显示所有文件、折叠所有节点、查看[属性](managing-project-and-solution-properties.md)页、在[代码编辑器](writing-code-in-the-code-and-text-editor.md)中预览代码等。

::: moniker-end

可以从“解决方案资源管理器”中的各种项目上的右键单击上下文菜单中获取多个菜单命令。 这些命令包括生成项目、管理 NuGet 包、添加引用、重命名文件和运行测试，此处仅举几例。

> [!TIP]
> 如果已关闭解决方案资源管理器并且想要重新打开它，请在菜单栏中选择“窗口” > “重置窗口布局” 。

对于 ASP.NET Core 项目，你可以自定义如何将文件嵌套在“解决方案资源管理器”中。 有关详细信息，请参阅[在解决方案资源管理器中自定义文件嵌套](file-nesting-solution-explorer.md)

## <a name="see-also"></a>另请参阅

- [项目和解决方案简介](../get-started/tutorial-projects-solutions.md)
- [管理项目和解决方案属性](managing-project-and-solution-properties.md)
- [Visual Studio 中筛选的解决方案](filtered-solutions.md)
- [移植、迁移和升级项目](../porting/port-migrate-and-upgrade-visual-studio-projects.md)
- [用于排除 Visual Studio IDE 错误的资源](./reference/resources-for-troubleshooting-integrated-development-environment-errors.md)
- [项目和解决方案 (Visual Studio for Mac)](/visualstudio/mac/projects-and-solutions)