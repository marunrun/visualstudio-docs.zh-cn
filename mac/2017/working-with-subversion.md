---
title: 使用 Subversion
description: 使用 Visual Studio for Mac 中的 Subversion。
author: heiligerdankgesang
ms.author: dominicn
ms.date: 05/06/2018
ms.assetid: 2400ED9C-6236-4C0A-A3AB-9D7CBE1F0CF4
ms.openlocfilehash: e5a9dd8120dd312bfc3e1c8905a725a58cca0e92
ms.sourcegitcommit: 370cc7fd2e11ede6d8215c8d81963a8307614550
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2019
ms.locfileid: "74983521"
---
# <a name="working-with-subversion"></a>使用 Subversion

Subversion 是集中式版本控制系统，可让用户签出集中式数据的一个主控副本。 与 Git 不同，签出 Subversion 存储库不会克隆整个存储库，它仅拍摄该时间点的快照。

Subversion 使用复制-修改-合并模型，支持多位用户同时使用同一存储库。 这意味着每个用户创建集中式数据的一个本地副本或工作副本，然后独立使用该副本。 对用户工作副本的更改按时间顺序合并。

例如，假设用户 A 和用户 B 都从远程存储库中签出一个副本，并且都修改了文件。 用户 A 完成修改并远程提交。 在用户 B 提交工作之前，需要使用远程提交的更改更新其工作副本，从而合并用户 A 的更改。

以下各部分介绍如何使用 Subversion 在 Visual Studio for Mac 中实现版本控制。

下图显示 Visual Studio for Mac 通过“版本控制”菜单项提供的选项：

![“版本控制”菜单项](media/version-control-svnVersionControlMenu.png)

## <a name="checkout"></a>签出...

在开始使用远程 Subversion 存储库前，先签出该存储库，在本地计算机上创建该目录的一个工作副本。

要了解如何使用 Visual Studio for Mac 中的“签出”  功能，请按照[设置 Subversion 存储库](set-up-subversion-repository.md)部分中的步骤进行操作。

## <a name="update-solution"></a>更新解决方案

使用远程存储库时，请务必记住其他用户可能正在修改文件，而这会让你的工作副本过时。 考虑到这一冲突，通常建议在开始工作前和提交前，将任何更改从存储库拉取到解决方案中。 要进行拉取变更，请选择“版本控制”>“更新解决方案”  菜单项。

## <a name="review-solution-and-commit"></a>查看解决方案并提交

要查看文件的更改，请使用每个文件上的“更改”、“责备”、“记录”和“合并”选项卡，如下图所示：

![“版本控制”选项卡](media/version-control-vcTabs.png)

通过浏览到“版本控制”>“评审解决方案并提交”  菜单项，查看项目中的所有更改：

![评审解决方案](media/version-control-vcStatus.png)

支持通过“还原”、“创建补丁”或“提交”选项查看项目每个文件中的所有更改。

要将文件提交到远程存储库，请按“提交...”，输入提交消息，然后单击“提交”按钮确认：

![提交文件](media/version-control-svnCommit.png)

将更改发送到创建所有修改的新修订版本的存储库。

## <a name="see-also"></a>请参阅

- [设置 Subversion 存储库](set-up-subversion-repository.md)
