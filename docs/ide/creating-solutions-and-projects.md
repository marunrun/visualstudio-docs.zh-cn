---
title: 创建解决方案和项目
ms.date: 02/06/2018
ms.topic: conceptual
f1_keywords:
- vs.openprojectfromweb
- VS.ToolsOptionsPages.Projects.General
- SolutionItemsProject
helpviewer_keywords:
- solutions [Visual Studio], creating
- projects [Visual Studio], creating
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: abe2cbd18e87c7045d44e597e3a5bb93a64a1c35
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72747968"
---
# <a name="create-solutions-and-projects"></a>创建解决方案和项目

“项目”用于保存在 Visual Studio 中生成应用时所需的项，比如源代码文件、位图、图标以及组件和服务引用  。 创建新项目时，Visual Studio 会创建一个解决方案  来包含该项目。 然后可以根据需要向解决方案添加其他新项目或现有项目。 解决方案还可以包含未连接到任何特定项目的文件。

![解决方案/项目层次结构](./media/vside-proj-soln.png)

> [!NOTE]
> 本主题适用于 Visual Studio  Windows 版。 对于 Visual Studio for Mac，请参阅[在 Visual Studio for Mac 中创建项目](/visualstudio/mac/create-new-projects)。

可在名为“解决方案资源管理器”  的工具窗口中查看解决方案和项目。 以下屏幕截图显示“解决方案资源管理器”中的一个示例解决方案 (BikeSharing.Xamarin-UWP)，该解决方案 包含两个项目：BikeSharing.Clients.Core 和 BikeSharing.Clients.Windows     。 每个项目均包含多个文件、文件夹和引用。 粗体形式的项目名称是*启动项目*；即，运行应用时启动的项目。 可以指定将哪个项目作为启动项目。

![包含项目的解决方案资源管理器](./media/vside-solution-explorer-projects.png)

用户可以通过向项目添加必要文件来自行构造项目，与此同时，Visual Studio 也提供了一组精选的项目模板，让用户能够拥有一个好的开端。 从模板新建的项目将具有该项目类型的必需元素，用户可在必要时重命名文件，或向项目添加新代码或现有代码以及其他资源。

也就是说，在 Visual Studio 中开发应用时不需要解决方案和项目。 用户也可以直接打开从 Git 克隆或从其他地方下载的代码。 有关详细信息，请参阅[在 Visual Studio 中开发代码而无需创建项目或解决方案](../ide/develop-code-in-visual-studio-without-projects-or-solutions.md)。

## <a name="create-a-project-from-a-project-template"></a>根据项目模板创建项目

有关根据模板创建新项目的信息，请参阅[在 Visual Studio 中创建新项目](create-new-project.md)。

## <a name="create-a-project-from-existing-code-files"></a>从现有代码文件创建项目

如果有一组代码源文件，可以轻松地将它们添加到项目。

1. 在菜单上，依次选择“文件”   > “新建”   > “从现有代码创建项目”  。

1. 在“从现有代码文件创建项目”  向导的“要创建什么类型的项目?”  下拉列表框中，选择所需的项目类型，然后选择“下一步”  按钮。

1. 在向导中，浏览到文件位置，然后在“名称”  框中输入新项目的名称。 完成后，选择“完成”  按钮。

> [!NOTE]
> 此选项最适合相对简单的文件集合。 目前仅支持 C++、Apache Cordova、Visual Basic 和 C# 项目类型。

## <a name="add-files-to-a-solution"></a>将文件添加到解决方案

如果有一个适用于多个项目的文件，比如解决方案的自述文件，或其他逻辑上属于解决方案级别而不是位于特定项目下的文件，则可以将它们添加到解决方案自身。 若要将某项添加到解决方案，请在“解决方案资源管理器”  中解决方案节点的上下文（右击）菜单上，依次选择“添加”   > “新项”  ，或依次选择“添加”   > “现有项”  。

## <a name="create-a-net-project-that-targets-a-specific-version-of-the-net-framework"></a>创建面向 .NET Framework 特定版本的 .NET 项目

创建 .NET Framework 项目时，可指定想要项目使用的特定 .NET Framework 版本。 （创建 .NET Core 项目时，不指定框架版本。）

::: moniker range="vs-2017"

要指定 .NET Framework 版本，请选择“新建项目”对话框中的“框架”下拉菜单   。

![“新建项目”对话框中的“框架”下拉列表](./media/vside-newproject-framework.png)

> [!NOTE]
> 必须在系统上安装 .NET Framework 3.5 才能访问 .NET Framework 4 以前的 .NET Framework 版本。

::: moniker-end

::: moniker range=">=vs-2019"

要指定 .NET Framework 版本，请选择“创建新项目”页中的“框架”下拉菜单   。

![配置新项目中的框架选择器](media/vs-2019/configure-new-project-framework.png)

::: moniker-end

## <a name="create-empty-solutions"></a>创建空的解决方案

还可以创建不包含任何项目的空解决方案。 这可能更适合想从头开始构造解决方案和项目的情况。

### <a name="to-create-an-empty-solution"></a>创建空解决方案

1. 在菜单栏上，依次选择“文件”   > “新建”   > “项目”  。

::: moniker range="vs-2017"

2. 在左侧（“模板”）窗格中，依次选择展开列表中的“其他项目类型”>“Visual Studio 解决方案”    。

3. 在中间窗格中，选择“空白解决方案”  。

4. 输入解决方案的“名称”和“位置”值，然后选择“确定”    。

::: moniker-end

::: moniker range=">=vs-2019"

2. 在“创建新项目”页上，在搜索框中键入“解决方案”   。

3. 选择“空白解决方案”模板，然后单击“下一步”   。

4. 输入解决方案的“名称”和“位置”值，然后选择“创建”    。

::: moniker-end

创建空白解决方案后，可以选择“项目”  菜单上的“添加新项”  或“添加现有项”  ，将新的或现有的项目或项添加到解决方案中。

如前文所述，还可以打开代码文件而无需创建项目或解决方案。 若要了解如何按照此方法开发代码，请参阅[在 Visual Studio 中开发代码而无需创建项目或解决方案](../ide/develop-code-in-visual-studio-without-projects-or-solutions.md)。

::: moniker range="vs-2017"

## <a name="create-a-temporary-project"></a>创建临时项目

（仅限 C# 和 Visual Basic）

如果创建基于 .NET 的项目时不指定磁盘位置，它就是一个临时项目。 临时项目可用于试验 .NET 项目。 使用临时项目时，可以随时选择保存或放弃它。

若要创建临时项目，请先转到“工具”   > “选项”   > “项目和解决方案”   > “常规”  ，取消选中“创建时保存新项目”  复选框。 然后照常打开“新建项目”  对话框。

::: moniker-end

## <a name="delete-a-solution-project-or-item"></a>删除解决方案、项目或项

可以永久删除解决方案及其内容，但不能通过 Visual Studio IDE 执行。 在 Visual Studio 中删除项只会将它们从当前解决方案或项目中移除。 若要从系统中永久删除解决方案或其他组件，请使用文件资源管理器删除包含 .sln 和 .suo 解决方案文件的文件夹   。 但是，在永久删除解决方案之前，建议备份好所有项目或文件，以防再次需要它们。

> [!NOTE]
> .suo 文件是隐藏文件，在默认的文件资源管理器设置下不会显示  。 若要显示隐藏文件，请在文件资源管理器的“查看”  菜单上选中“隐藏项”  复选框。

### <a name="permanently-delete-a-solution"></a>永久删除解决方案

1. 在“解决方案资源管理器”  中，在要删除的解决方案的右键单击菜单（关联菜单）中，选择“在文件资源管理器中打开文件夹”  。

1. 在文件资源管理器中，导航到上一级。

1. 选择包含解决方案的文件夹，然后按 Delete 键  。

## <a name="see-also"></a>请参阅

- [解决方案和项目](../ide/solutions-and-projects-in-visual-studio.md)
- [GitHub 上的 Microsoft 开放源代码存储库](https://github.com/Microsoft)
- [开发者代码示例](https://code.msdn.microsoft.com/)
- [创建项目 (Visual Studio for Mac)](/visualstudio/mac/create-new-projects)