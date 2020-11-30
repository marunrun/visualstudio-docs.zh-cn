---
title: Visual Studio 中的 Git 体验
titleSuffix: ''
description: 了解 Visual Studio 2019 中新的集成 Git 体验如何帮助提高工作效率。
ms.date: 11/16/2020
ms.topic: conceptual
ms.author: tglee
author: TerryGLee
ms.manager: jillfra
monikerRange: vs-2019
ms.openlocfilehash: e640d19659861a03d0f97abc799344bebb14b936
ms.sourcegitcommit: f78960320798e2c6b33145cee77a2221f031603c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/18/2020
ms.locfileid: "94878304"
---
# <a name="git-experience-in-visual-studio"></a>Visual Studio 中的 Git 体验

Git 现在是 Visual Studio 2019 中的默认版本控制体验。 从[版本 16.6](/visualstudio/releases/2019/release-notes-v16.6) 开始，我们致力于构建功能集，并根据你的反馈对其进行迭代。 默认情况下，对于使用[版本 16.8](/visualstudio/releases/2019/release-notes/) 的所有用户，新 Git 体验处于开启状态。

> [!TIP]
> Git 是使用最广泛的新式版本控制系统，因此，无论你是专业的开发人员，还是正在学习编码的人员，Git 都非常有用。 如果不熟悉 Git，那么 https://git-scm.com/ 网站是一个不错的起点。 你可以从该网站找到速查表、畅销在线图书和 Git 基础知识视频。

## <a name="how-to-use-git-in-visual-studio"></a>如何在 Visual Studio 中使用 Git

我们将引导你逐步使用 Visual Studio 2019 中的新 Git 体验，但若要先进行快速导览，请观看以下视频： <br><br>*视频长度：* 5.27 分钟

> [!VIDEO https://www.youtube.com/embed/UHrAg3iKoe0]

可以通过三种方式开始结合使用 Git 与 Visual Studio 来提高工作效率：

- [打开现有 Git 存储库](#open-an-existing-local-repository)。 如果计算机上已有代码，则可以使用“文件” > “打开” > “项目/解决方案”（或“文件夹”）打开代码，Visual Studio 会自动检测其是否具有已初始化的 Git 存储库   。
- [创建新的 Git 存储库](#create-a-new-git-repository)。 如果你的代码未与 Git 关联，则可以创建一个新的 Git 存储库。
- [克隆现有 Git 存储库](#clone-an-existing-git-repository)。 如果要处理的代码不在计算机上，则可以克隆任何现有的远程存储库。

> [!NOTE]
> 也是自[版本 16.8](/visualstudio/releases/2019/release-notes/) 起，Visual Studio 2019 包含完全集成的 GitHub 帐户体验。 你现在可以将 GitHub 和 GitHub Enterprise 帐户都添加到密钥链中。 你可以添加并使用这些帐户，就像使用 Microsoft 帐户一样；也就是说，你将能够更轻松地跨 Visual Studio 访问 GitHub 资源。 有关详细信息，请参阅[在 Visual Studio 中使用 GitHub 帐户](work-with-github-accounts.md)页面。

## <a name="create-a-new-git-repository"></a>创建新的 Git 存储库

如果你的代码未与 Git 关联，则可以首先创建一个新的 Git 存储库。 为此，请从菜单栏中选择“Git” > “创建 Git 存储库” 。 然后，在“创建 Git 存储库”对话框中，输入你的信息。

:::image type="content" source="media/git-create-repository.png" alt-text="Visual Studio 中“创建 Git 存储库”对话框。":::

利用“创建 Git 存储库”对话框，可以轻松地将新存储库推送到 GitHub。 默认情况下，新存储库是专用的，这意味着只有你可以访问它。 如果取消选中此框，则该存储库将是公用的，这意味着 GitHub 上的任何人都可以查看它。

> [!TIP]
> 无论存储库是公用的还是专用的，即使你不与团队合作，也应将代码的远程备份安全地存储在 GitHub 上。 这也使得无论使用哪台计算机，你都可以使用你的代码。

可选择使用“仅限本地”选项，创建仅限本地的 Git 存储库。 也可使用“现有远程”选项，将存储库与任何其他 Git 提供程序上的任何现有空远程存储库关联。

## <a name="clone-an-existing-git-repository"></a>克隆现有 Git 存储库

Visual Studio 包含简单的克隆体验。 如果知道要克隆的存储库的 URL，则可以将该 URL 粘贴到“存储库位置”部分，然后选择要将 Visual Studio 克隆到的磁盘位置。

:::image type="content" source="media/git-clone-repository.png" alt-text="Visual Studio 中“克隆 Git 存储库”对话框。":::

如果不知道存储库 URL，则可以利用 Visual Studio 轻松浏览到现有的 GitHub 或 Azure DevOps 存储库，然后再进行克隆。

### <a name="open-an-existing-local-repository"></a>打开现有的本地存储库

克隆存储库或创建存储库之后，Visual Studio 将检测该 Git 存储库，并将其添加到 Git 菜单中的“本地存储库”列表。 在这里，你可以快速访问 Git 存储库并在其之间快速切换。

:::image type="content" source="media/git-local-repositories.png" alt-text="Visual Studio 中 Git 菜单上的“本地存储库”选项 ":::

## <a name="view-files-in-solution-explorer"></a>解决方案资源管理器中的的视图文件

克隆存储库或打开本地存储库时，Visual Studio 会通过保存并关闭先前打开的解决方案和项目，将你切换到该 Git 上下文。 解决方案资源管理器将在 Git 存储库的根目录中加载文件夹，并在目录树中扫描所有视图文件。 其中包括 CMakeLists.txt 等文件或具有 .sln 文件扩展名的文件。

Visual Studio 将根据你在解决方案资源管理器中加载的视图文件调整其视图：

- 如果克隆包含单个 .sln 文件的存储库，则解决方案资源管理器会直接为你加载该解决方案。
- 如果解决方案资源管理器在存储库中未检测到任何 .sln 文件，则默认情况下将加载文件夹视图。
- 如果存储库中有多个 .sln 文件，则解决方案资源管理器将显示可用视图的列表供你选择。

可以使用解决方案资源管理器工具栏中的“切换视图”按钮，在当前打开的视图和视图列表之间进行切换。

:::image type="content" source="media/git-solution-explorer-views.png" alt-text="Visual Studio 中选中“切换视图”按钮的解决方案资源管理器。":::

## <a name="git-changes-window"></a>Git 更改窗口

当你操作时，Git 会跟踪存储库中的文件更改，并将存储库中的文件分为三类。 这些更改等效于在命令行中输入 `git status` 命令时看到的内容：

- **未修改的文件**：自上次提交以来，这些文件未更改。
- **已修改的文件**：自上次提交以来，这些文件已更改，但尚未被暂存以用于下一次提交。
- **已暂存的文件**：这些文件已更改并将添加到下一次提交中。

当你执行操作时，Visual Studio 会在“Git 更改”窗口的“更改”部分中跟踪对项目的文件更改 。

:::image type="content" source="media/git-changes-window.png" alt-text="Visual Studio 中“Git 更改”窗口。":::

准备暂存更改时，请单击要暂存的每个文件上的“+”（加号）按钮，或右键单击文件，然后选择“暂存” 。 还可以使用“更改”部分顶部的暂存全部 +（加号）按钮，一键暂存所有已修改的文件 。

暂存更改时，Visual Studio 将创建“已暂存的更改”部分。 只有“已暂存的更改”部分的更改会添加到下一次提交中，可以通过选择“提交暂存内容”来执行此操作 。 还可以通过单击“–”（减号）按钮来取消暂存更改。 此操作的等效命令是 `git commit -m "Your commit message"`。

也可以通过跳过暂存区域来选择不暂存已修改的文件。 在这种情况下，Visual Studio 允许直接提交更改，而无需暂存更改。 只需输入提交消息，然后选择“全部提交”。 此操作的等效命令是 `git commit -a`。

还可通过 Visual Studio 的“全部提交并推送”和“全部提交并同步”快捷方式，轻松地一键提交和同步 。 双击“更改”和“已暂存的更改”部分中的任何文件时，可以看到与该文件的未修改版本的逐行比较 。

:::image type="content" source="media/git-file-version-compare.png" alt-text="Visual Studio 中文件版本的逐行比较 ":::

> [!TIP]
> 如果已连接到 Azure DevOps 存储库，可使用“#”字符将 Azure DevOps 工作项和提交相关联。 可通过“团队资源管理器” > “管理连接”连接 Azure DevOps 存储库。

### <a name="select-an-existing-branch"></a>选择一个现有分支

Visual Studio 会在“Git 更改”窗口顶部的选择器中显示当前分支。

:::image type="content" source="media/git-changes-current-branch-selector.png" alt-text="可以使用 Visual Studio 中“Git 更改”选择器顶部的选择器来查看的当前分支 ":::

当前分支也显示在 Visual Studio IDE 右下角的状态栏中。

:::image type="content" source="media/git-changes-current-branch-status-bar.png" alt-text="可以使用 Visual Studio IDE 右下角的状态栏来查看的当前分支 ":::

可以从这两个位置在现有分支之间进行切换。

### <a name="create-a-new-branch"></a>创建新分支

还可以创建一个新的分支。 此操作的等效命令是 `git checkout <branchname>`。

创建新分支非常简单，只需输入分支名称并将其基于现有分支。

:::image type="content" source="media/git-changes-create-new-branch.png" alt-text="Visual Studio 中“创建新分支”对话框 ":::

可以选择一个现有的本地或远程分支作为基础。 “签出分支”复选框会自动切换到新创建的分支。 此操作的等效命令是 `git checkout -b <new-branch><existing-branch>`。

## <a name="git-repository-window"></a>“Git 存储库”窗口

Visual Studio 有一个新的“Git 存储库”窗口，该窗口是存储库中所有详细信息的合并视图，包括所有分支、远程库和提交历史记录。 可以从菜单栏上的“Git”或“视图”，或从状态栏直接访问此窗口 。

### <a name="manage-branches"></a>管理分支

从 Git 菜单中选择“管理分支”时，你将在“Git 存储库”窗口中看到分支树状视图  。 在左侧窗格中，可以使用右键单击上下文菜单来签出分支、创建新的分支、合并、变基、挑拣等。 单击分支后，可以在右窗格中查看其提交历史记录的预览。

### <a name="incoming-and-outgoing-commits"></a>传入和传出提交

提取分支时，“Git 更改”窗口在分支下拉箭头下有一个指示器，其中显示了远程分支的未拉取提交数。 该指示器还显示未推送的本地提交数。

:::image type="content" source="media/git-repo-drop-down-indicator.png" alt-text="Visual Studio 中显示指示器下拉 UI 元素的“Git 更改”窗口 ":::

该指示器还可作为链接，将你带到“Git 存储库”窗口中该分支的提交历史记录。 历史记录的顶部现在会显示这些传入和传出提交的详细信息。 你还可以在这里决定拉取或推送提交。

:::image type="content" source="media/git-branch-commit-history.png" alt-text="Visual Studio 中显示分支提交历史记录的 Git 存储库窗口 ":::

#### <a name="commit-details"></a>提交详细信息

双击“提交”时，Visual Studio 会在单独的工具窗口中打开其详细信息。 在此处，你可以还原提交、重置提交、修改提交消息，或在提交上创建标记。 在提交中单击已更改的文件时，Visual Studio 将打开该提交及其父级的并排差异视图。

:::image type="content" source="media/git-branch-commit-details.png" alt-text="Visual Studio 中“提交详细信息”对话框 ":::

## <a name="handle-merge-conflicts"></a>处理合并冲突

如果两个开发人员在文件中修改了相同的行，并且 Git 无法自动识别哪个是正确的，则在合并期间可能会发生冲突。 Git 暂停合并，并通知你处于冲突状态。

使用 Visual Studio 可以轻松地识别和解决合并冲突。 首先，“Git 存储库”窗口会在窗口顶部显示一个金色的信息栏。

:::image type="content" source="media/git-merge-conflict-gold-bar.png" alt-text="Visual Studio 中“合并已完成，但存在冲突”消息 ":::

“Git 更改”窗口还会显示“合并正在进行，但存在冲突”消息，而未合并的文件位于其下方的单独部分中。

:::image type="content" source="media/git-merge-progress-conflicts-message.png" alt-text="Visual Studio 中“合并正在进行，但存在冲突”消息 ":::

但是，如果没有打开这些窗口，而是转到具有合并冲突的文件，则无需搜索以下文本：

```bash
    <<<<<<< HEAD
    =======
    >>>>>>> main
```

相反，Visual Studio 会在页面顶部显示金色的信息栏，指示打开的文件存在冲突。 然后，可以单击链接以打开“合并编辑器”。

:::image type="content" source="media/git-merge-conflict-gold-info-bar.png" alt-text="Visual Studio 中“文件包含合并冲突”消息的屏幕截图":::

### <a name="the-merge-editor"></a>合并编辑器

Visual Studio 中的合并编辑器是一种三向合并工具，用于显示传入的更改、当前的更改和合并的结果。 可以使用“合并编辑器”顶层的工具栏在文件中的冲突和自动合并的差异之间导航。

:::image type="content" source="media/git-merge-editor.png" alt-text="Visual Studio 中“合并编辑器” ":::

还可以使用切换来显示/隐藏差异、显示/隐藏单词差异，以及自定义布局。 每侧的顶部都有复选框，你可从任何一侧通过这些复选框来执行所有更改。 但若要进行单独的更改，可以单击任一侧的冲突行左侧的复选框。 最后，解决完冲突后，可以在合并编辑器中选择“接受合并”按钮。 然后，可以编写提交消息并提交更改以完成解决操作。

## <a name="personalize-your-git-settings"></a>个性化设置 Git 设置

若要在存储库级别和全局级别对 Git 设置进行个性化设置和自定义，请转到菜单栏上的“Git” > “设置”，或转到菜单栏上的“工具” > “选项” > “源代码管理”    。 然后选择所需的选项。

:::image type="content" source="media/git-options-settings.png" alt-text="Visual Studio IDE 中“选项”对话框，可以在该对话框中选择个性化设置和自定义设置 ":::

## <a name="how-to-use-the-legacy-team-explorer-experience-in-visual-studio"></a>如何在 Visual Studio 中使用旧的团队资源管理器体验

从[版本 16.8](/visualstudio/releases/2019/release-notes/) 开始，新的 Git 体验是 Visual Studio 2019 中的默认版本控制系统。 但是，可以在需要时将它关闭。 转到“工具” > “选项” > “环境” > “预览功能”，然后切换“新的 Git 用户体验”复选框    ，这会使你切换回旧的团队资源管理器体验。

:::image type="content" source="media/git-opt-new-user-experience.png" alt-text="Visual Studio 中“选项”对话框的“预览功能”部分 ":::

## <a name="whats-next"></a>后续步骤

虽然默认情况下，新 Git 体验目前在 Visual Studio 2019 [版本 16.8](/visualstudio/releases/2019/release-notes/) 中处于开启状态，不过我们会继续添加新功能以增强体验。 如果要在预览版本中查看对 Git 体验的新更新，可以从 [Visual Studio Preview](https://aka.ms/vspreview/) 页面下载并安装它。

> [!IMPORTANT]
> 如果你对我们有任何建议，请告诉我们！ 我们非常感激能够通过[开发人员社区](https://aka.ms/vs-suggest)门户与你交流设计决策。

## <a name="see-also"></a>另请参阅

- [宣布在 Visual Studio 中推出 Git 体验](https://devblogs.microsoft.com/visualstudio/announcing-the-release-of-the-git-experience-in-visual-studio/)博客文章
- YouTube 上的[启动新 Git 体验](https://www.youtube.com/watch?v=UHrAg3iKoe0&t)
- [Visual Studio 工具箱系列提供：新 Git 体验](https://channel9.msdn.com/Shows/Visual-Studio-Toolbox/The-New-Git-Experience)视频（在第 9 频道和 [YouTube](https://www.youtube.com/watch?v=ZiQ2LXtAJ6I&feature=youtu.be) 上）
- [Visual Studio 中针对 Git 体验的精彩新更新](https://devblogs.microsoft.com/visualstudio/exciting-new-updates-to-the-git-experience-in-visual-studio/)博客文章
- [Visual Studio 2019 中的 Git 新体验](https://devblogs.microsoft.com/visualstudio/improved-git-experience-in-visual-studio-2019/)博客文章
- [在 Visual Studio 中使用 GitHub 帐户](work-with-github-accounts.md)
- [Visual Studio 2019 发行说明](/visualstudio/releases/2019/release-notes)
