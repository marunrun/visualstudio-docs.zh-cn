---
title: 开发代码而无需创建项目或解决方案
ms.date: 02/21/2018
ms.topic: conceptual
helpviewer_keywords:
- open folder [Visual Studio]
- anycode [Visual Studio]
- projects and solutions, develop code without
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d7a9459868d569a7466dccf92e4b548c0500bf80
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "75596289"
---
# <a name="develop-code-in-visual-studio-without-projects-or-solutions"></a>在 Visual Studio 中开发代码而无需创建项目或解决方案

你可以在 Visual Studio 中打开几乎任何类型的基于目录的项目的代码，而无需创建解决方案或者项目文件。 这意味着，例如，可以在 GitHub 上克隆一个存储库，然后在 Visual Studio 中直接打开并开始开发，而无需创建解决方案或项目。 如果需要，可以指定自定义生成任务并通过简单的 JSON 文件启动参数。

在 Visual Studio 中打开代码文件之后，“解决方案资源管理器”会显示文件夹中的所有文件  。 可以单击任何文件开始编辑。 在后台，Visual Studio 开始对文件编制索引，以启用 IntelliSense、导航和重构功能。 在编辑、创建、移动或删除文件时，Visual Studio 会自动跟踪更改，并不断更新其 IntelliSense 索引。 代码带有语法着色，许多情况下还含有基本的 IntelliSense 语句完成。

## <a name="open-any-code"></a>打开任何代码

可以通过以下任何方式，在 Visual Studio 中打开代码：

- 在 Visual Studio 菜单栏上，依次选择“文件”   > “打开”   > “文件夹”  ，然后浏览到代码位置。

- 在包含该代码的文件夹的上下文（右键单击）菜单上，选择“在 Visual Studio 中打开”  命令。

::: moniker range="vs-2017"
- 选择 Visual Studio“开始”页上的“打开文件夹”链接   。
::: moniker-end

::: moniker range=">=vs-2019"
- 在“启动”窗口中选择“打开文件夹”链接  。
::: moniker-end

- 如果是键盘用户，则在 Visual Studio 中按 Ctrl  +Shift  +Alt  +O  。

- 打开克隆的 GitHub 存储库中的代码。

### <a name="to-open-code-from-a-cloned-github-repo"></a>打开克隆的 GitHub 存储库中的代码

以下示例演示如何克隆 GitHub 存储库，并在 Visual Studio 中打开其代码。 若要执行此过程，必须具有 GitHub 帐户，并且已经在系统上安装了适用于 Windows 的 Git。 请参阅[注册新的 GitHub 帐户](https://help.github.com/articles/signing-up-for-a-new-github-account/)和[适用于 Windows 的 Git](https://git-for-windows.github.io/) 了解详细信息。

1. 转到要在 GitHub 上克隆的存储库。

1. 选择“克隆或下载”按钮，然后在下拉菜单中选择“复制到剪贴板”按钮，以便复制 GitHub 存储库的安全 URL   。

   ![GitHub 克隆按钮](./media/VSIDE_Code_Clone.png)

1. 在 Visual Studio 中，选择“团队资源管理器”选项卡，打开“团队资源管理器”   。 如果未看到选项卡，则从“视图”   > “团队资源管理器”  中将其打开。

1. 在团队资源管理器的“本地 Git 存储库”  部分中，选择“克隆”  命令，然后将 GitHub 页的 URL 粘贴到文本框。

   ![克隆项目](./media/VSIDE_Code_Clone2.png)

1. 选择“克隆”  按钮，将项目的文件克隆到本地 Git 存储库。 此过程可能需要几分钟的时间，具体取决于存储库的大小。

1. 将存储库克隆到系统后，在“团队资源管理器”中，在新克隆存储库的上下文（右键单击）菜单上，选择“打开”命令   。

   ![已克隆的存储库](./media/VSIDE_Code_Clone3.png)

1. 选择“显示文件夹视图”命令，查看“解决方案资源管理器”中的文件   。

   ![显示文件夹视图](./media/VSIDE_Code_Clone3_show.png)

   此时，可以浏览克隆存储库中的文件夹和文件，并在具有语法着色和其他功能的 Visual Studio 代码编辑器中查看和搜索代码。

## <a name="run-and-debug-your-code"></a>运行和调试代码

不通过项目或解决方案即可在 Visual Studio 中调试代码！ 对某些语言进行调试时，可能需要在代码库中指定一个有效的启动文件  ，例如脚本、可执行文件或项目。 工具栏上“开始”  按钮旁的下拉列表框中列出了 Visual Studio 检测到的所有启动项，以及你在文件夹中专门指定的项。 调试代码时，Visual Studio 会首先运行此代码。

配置代码以在 Visual Studio 中运行因代码类型和生成工具而异。

### <a name="codebases-that-use-msbuild"></a>使用 MSBuild 的代码库

基于 MSBuild 的代码库拥有多个生成配置，它们在“开始”  按钮的下拉列表中显示。 选择要作为启动项使用的文件，然后选择“开始”  按钮开始调试。

> [!NOTE]
> 对于 C# 和 Visual Basic 代码库，必须安装 .NET 桌面开发  工作负载。 对于 C++ 代码库，必须安装使用 C++ 的桌面开发  工作负载。

### <a name="codebases-that-use-custom-build-tools"></a>使用自定义生成工具的代码库

如果代码库使用自定义生成工具，则必须告知 Visual Studio 如何使用 .json  文件中定义的生成任务  来生成代码。 有关详细信息，请参阅[自定义生成和调试任务](../ide/customize-build-and-debug-tasks-in-visual-studio.md)。

### <a name="codebases-that-contain-python-or-javascript-code"></a>包含 Python 或 JavaScript 代码的代码库

如果代码库包含 Python 或 JavaScript 代码，则无需配置任何 .json  文件，但必须安装相应的工作负载。 还必须配置启动脚本：

1. 通过选择“工具”[“获取工具和功能”](https://visualstudio.microsoft.com/vs/node-js/)[，或者通过关闭 Visual Studio 并运行 Visual Studio 安装程序来安装 ](https://visualstudio.microsoft.com/vs/python/)Node.js 开发**或** Python 开发 > 工作负载  。

   ![Node.js 和 Python 开发工作负载](media/python_nodejs_workloads.png)

1. 在“解决方案资源管理器”  中，右键单击 JavaScript 或 Python 文件的上下文菜单上，选择“设置为启动项”  命令。

1. 选择“开始”  按钮开始调试。

### <a name="codebases-that-contain-c-code"></a>包含 C++ 代码的代码库

有关在 Visual Studio 中打开 C++ 代码而无需创建解决方案或项目的信息，请参阅 [C++ 的打开文件夹项目](/cpp/build/open-folder-projects-cpp)。

### <a name="codebases-that-contain-a-visual-studio-project"></a>包含 Visual Studio 项目的代码库

如果代码文件夹包含 Visual Studio 项目，则可以将项目指定为启动项。

![将项目设为启动项](media/customize-set-project-as-startup-item.png)

“开始”  按钮的文本将更改，以反映项目为启动项。

![“开始”按钮上的项目](media/customize-start-button-project.png)

## <a name="see-also"></a>另请参阅

- [自定义生成和调试任务](../ide/customize-build-and-debug-tasks-in-visual-studio.md)
- [C++ 的打开文件夹项目](/cpp/build/open-folder-projects-cpp)
- [C++ 中的 CMake 项目](/cpp/build/cmake-projects-in-visual-studio)
- [在代码和文本编辑器中编写代码](../ide/writing-code-in-the-code-and-text-editor.md)
