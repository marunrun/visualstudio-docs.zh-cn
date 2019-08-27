---
title: 使用 Git
description: 使用 Visual Studio for Mac 中的 Git。
author: jmatthiesen
ms.author: jomatthi
ms.date: 05/06/2018
ms.assetid: 852B6A9D-AEFA-4EF4-A5DD-94A506019D20
ms.custom: video
ms.openlocfilehash: b047222f67d75bbc092a731c8de1ca1ba6d94cf7
ms.sourcegitcommit: 7fbfb2a1d43ce72545096c635df2b04496b0be71
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/09/2019
ms.locfileid: "67692166"
---
# <a name="working-with-git"></a>使用 Git

Git 是分布式版本控制系统，使团队可以同时在同一文档上工作。 这意味着有一个中央服务器包含所有文件，但从此中央源中签出存储库时，整个存储库都会被克隆到本地计算机。

以下各部分将探索如何为 Visual Studio for Mac 中的版本控制使用 Git。

## <a name="git-version-control-menu"></a>Git 版本控制菜单

下图显示 Visual Studio for Mac 通过“版本控制”菜单项提供的选项：

![“版本控制”菜单项](media/version-control-gitVersionControlMenu.png)

## <a name="push-and-pull"></a>推送和拉取

推送和拉取是 Git 中最常用的两个操作。 若要同步其他人对远程存储库做的更改，必须从这里进行“拉取”  。 在 Visual Studio for Mac 中可通过选择“版本控制”>“更新解决方案”  完成。

更新、评审并提交文件后，必须将文件“推送”  到远程存储库，以便其他用户可以访问所做更改。 在 Visual Studio for Mac 中可通过选择“版本控制”>“推送更改”  完成。 这将显示“推送”对话框，可查看提交的更改，然后选择要推送到的分支：

![显示要提交到的分支的对话框](media/version-control-gitPush.png)

还可通过“提交”对话框同时“提交”和“推送”更改：

![显示如何同时提交和推送的选项。](media/version-control-commitPush.png)

## <a name="blame-log-and-merge"></a>责备、记录和合并

在窗口的底部显示了五个选项卡，如下所示：

![“版本控制”选项卡](media/version-control-gitTabs.png)

可以执行以下操作：

* **源** - 显示源代码文件。
* **更改** - 显示本地文件和基础文件之间的代码更改。 还可以比较不同哈希的文件的不同版本：

    ![“更改”选项卡](media/version-control-gitChange.png)

* **责备** - 显示和每个代码部分有关的用户名。
* **日志** - 显示所有提交、时间、日期、消息和对此文件负责的用户：

    ![“日志”选项卡](media/version-control-gitLog.png)

* **合并** - 可在提交工作出现合并冲突时使用。 显示更改的可视化表示形式，这些更改是你和其他开发者创建的，使你可以彻底合并代码的两个部分。

## <a name="switching-branches"></a>切换分支

默认情况下，存储库中创建的第一个分支称为主分支 ****  。 主分支和其他分支之间没有任何技术上的不同，但是主分支通常被认为是开发团队的“实时”或“生产”分支。

对主分支（或任何其他分支）再进行分支，可形成独立的开发思路。 这为某个时间点的主分支提供了新版本，允许独立于“实时”开发。 使用这种方式的分支通常用于软件开发功能

用户可为每个存储库创建任意数量的分支，但建议在完成使用分支后，删除分支以保持存储库结构。

可通过浏览到“版本控制”>“管理分支和远程...”  ，在 Visual Studio for Mac 中查看分支：

![分支视图](media/version-control-gitBranch2.png)

通过在列表中选中分支并按“切换到分支”  按钮可切换到另一个分支。

若要创建新分支，请选择 Git 存储库配置对话框中的“新建”  按钮。 输入新分支名称：

![创建新分支](media/version-control-gitBranch.png)

还可为“跟踪”  分支设置一个远程分支。 请参阅 [Git 文档](https://git-scm.com/book/en/v2/Git-Branching-Remote-Branches#Tracking-Branches)了解更多关于跟踪分支的详细信息。

在 Solution Pad 中查看当前分支（在项目名称旁）：

 ![Solution Pad 中显示的当前分支](media/version-control-gitBranchName.png)

## <a name="reviewing-and-committing"></a>评审并提交

若要查看文件的更改，请使用每个文件上的“更改”、“责备”、“记录”和“合并”选项卡，如前文所示。

可通过浏览到“版本控制”>“评审解决方案并提交”  菜单项，查看项目中的所有更改：

![查看代码视图](media/version-control-gitReviewCommit.png)

允许通过“还原”、“创建补丁”或“提交”选项查看项目每个文件中的所有更改。

要将文件提交到远程存储库，请按“提交”，输入提交消息，然后单击“提交”按钮确认  ：

![提交文件](media/version-control-gitCommit.png)

提交更改后，将其推送到远程存储库，以便其他用户查看。

## <a name="related-video"></a>相关视频

> [!Video https://channel9.msdn.com/Shows/Visual-Studio-Toolbox/Visual-Studio-for-Mac-Manage-Projects-with-Git/player]

## <a name="see-also"></a>请参阅

* [与 Visual Studio 2017 和 Azure Repos Git 共享代码](/azure/devops/repos/git/share-your-code-in-git-vs-2017)