---
title: 创建新项目
ms.date: 03/19/2019
ms.topic: conceptual
f1_keywords:
- vs.newproject
helpviewer_keywords:
- projects [Visual Studio], creating
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 9f5d48ee97e1e0d92237fe5836c8bd9c1888c3a4
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62818814"
---
# <a name="create-a-new-project-in-visual-studio"></a>在 Visual Studio 中创建新项目

::: moniker range="vs-2017"

## <a name="open-the-new-project-dialog"></a>打开“新建项目”对话框

可通过多种方式在 Visual Studio 2017 中创建新项目。 在起始页上，可在“搜索项目模板”框中键入项目模板的名称，或选择“创建新项目”链接打开“新建项目”对话框。 除了通过起始页，也可以选择菜单栏上的“文件” > “新建” > “项目”，或单击工具栏上的“新建项目”按钮。

![起始页和“文件”>“新建”>“项目”](./media/vside-newproject1.png)

## <a name="select-a-template-type"></a>选择一个模板类型

在“新建项目”对话框中的“模板”类别下，可用项目模板以列表形式列出。 模板按编程语言和项目类型（如 Visual C#、JavaScript 和 Azure Data Lake）归类。

![“新建项目”对话框](./media/vside-newproject-templates-list.png)

> [!NOTE]
> 显示的可用语言和项目模板列表取决于正在运行的 Visual Studio 版本和安装的工作负载。 要了解如何安装附加工作负载，请参阅[通过添加或删除工作负载和组件修改 Visual Studio](../install/modify-visual-studio.md)。

通过单击语言名称旁边的三角形，然后选择项目类别（如 Windows 桌面），显示要使用的编程语言的模板列表。

下图显示可用于 Visual C# .NET Core 项目的项目模板：

![项目模板](./media/new-project-dialog-net-core.png)

## <a name="configure-your-project"></a>配置项目

在“名称”框中输入新项目的名称。 可将项目保存在计算机上的默认位置，或单击“浏览”按钮查找其他位置。 还可以选择解决方案名称，或将新项目添加到 Git 存储库（方法是选择“添加到源代码管理”）。

单击“确定”创建解决方案和项目。

::: moniker-end

::: moniker range=">=vs-2019"

## <a name="open-the-create-a-new-project-page"></a>打开“创建新项目”页

可通过多种方式在 Visual Studio 2019 中创建新项目。 首次打开 Visual Studio 时，将显示“启动”窗口，通过此窗口可选择“创建新项目”。

![从 VS 2019 的“启动”窗口创建新项目](media/vs-2019/start-window-create-new-project.png)

如果已打开 Visual Studio 开发环境，在菜单栏上选择“文件”>“新建”>“项目”，或者单击工具栏上的“新建项目”按钮即可创建新项目。

![Visual Studio 2019 中的“新建项目”按钮](media/vs-2019/new-project-button.png)

## <a name="select-a-template-type"></a>选择一个模板类型

在“创建新项目”页上，最近选择的模板列表显示在左侧。 模板按“最近使用”排序。

如果没有从最近使用的模板中进行选择，则可以按“语言”（如 C#或 C++）、“平台”（如 Windows 或 Azure）和“项目类型”（如桌面或 Web）筛选所有可用的项目模板。 还可在搜索框中输入搜索文本（如 asp.net）以进一步筛选模板，例如 asp.net。

![Visual Studio 2019 中的项目模板筛选器](media/vs-2019/create-new-project-filters.png)

每个模板下方显示的标记对应于三个下拉筛选器（语言、平台和项目类型）。

> [!TIP]
> 如果没有看到要查找的模板，则可能是丢失了 Visual Studio 的工作负载。 要安装其他工作负载（如 Azure 开发或使用 .NET 的移动开发），请单击“安装更多工具和功能”链接以打开 Visual Studio 安装程序。 从中选择要安装的工作负载，然后选择“修改”。 之后，便可选择其他项目模板。
>
> ![VS 2019 中的“安装更多工具和功能”链接](media/vs-2019/install-more-tools-features.png)

选择一个模板，然后单击“下一步”。

## <a name="configure-your-project"></a>配置项目

“配置新项目”页中提供有关对项目（和解决方案）命名、选择磁盘位置和选择框架版本（如果适用于所选模板）的选项。

![VS 2019 中的“配置新项目”页](media/vs-2019/configure-new-project.png)

> [!NOTE]
> 如果在 Visual Studio 中存在已打开的项目或解决方案时创建新项目，则可以使用额外的配置选项。 可选择创建新解决方案或将新项目添加到已打开的解决方案中。
>
> ![创建新解决方案或添加到 VS 2019 中的现有解决方案](media/vs-2019/configure-new-project-solution.png)

单击“创建”以创建新项目。

::: moniker-end

## <a name="add-additional-projects-to-a-solution"></a>向解决方案添加其他项目

若要向解决方案添加其他项目，请右键单击“解决方案资源管理器”中的解决方案节点，然后选择“添加” > “新建项目”。

## <a name="see-also"></a>请参阅

- [创建解决方案和项目](creating-solutions-and-projects.md)
