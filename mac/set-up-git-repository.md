---
title: 设置 Git 存储库
description: 使用 Visual Studio for Mac 中的 Git 和 Subversion。
author: jmatthiesen
ms.author: jomatthi
ms.date: 02/15/2019
ms.assetid: E992FA1D-B2AD-4A28-ADC6-47E4FC471060
ms.openlocfilehash: 9b21ed322d2b22be619a71e474a3b5078607bbe5
ms.sourcegitcommit: 2975d722a6d6e45f7887b05e9b526e91cffb0bcf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/20/2020
ms.locfileid: "70107894"
---
# <a name="set-up-a-git-repository"></a>设置 Git 存储库

Git 是分布式版本控制系统，使团队可以同时在同一文档上工作。 这意味着有一个单一服务器包含所有文件，但从此中央源中签出存储库时，整个存储库都会被克隆到本地计算机。

虽然许多远程主机允许使用 Git 进行版本控制，但最常用的主机是 GitHub。 虽然下面的示例使用 GitHub 主机，但可使用任何 Git 主机在 Visual Studio for Mac 中进行版本控制。

若要使用 GitHub，请确保先创建并配置一个帐户，然后再执行本文中的步骤。

## <a name="creating-a-remote-repo-on-github"></a>在 GitHub 上创建远程存储库

虽然下面的示例使用 GitHub 主机，但可使用任何 Git 主机在 Visual Studio for Mac 中进行版本控制。

要设置 Git 存储库，请执行以下步骤：

1. 在 github.com 上创建新 Git 存储库：

    ![创建新 Git 存储库](media/version-control-git1-sml.png)

2. 设置存储库名称、说明和隐私。 请勿初始化存储库  。 将 .gitignore 和许可证设置为“无”：

    ![设置 Git 存储库的详细信息](media/version-control-git2.png)

3. 下页提供一个选项，用于显示 HTTPS 或 SSH 地址，并将其复制到已创建的存储库：

    ![查看和复制地址](media/version-control-git3.png)

   要将 Visual Studio for Mac 指向此存储库，需要 HTTPS 地址。

## <a name="publishing-an-existing-project"></a>发布现有项目

如果现有的一个项目_不_在版本控制中，请使用以下步骤在 Git 中设置该项目：

1. 从 Visual Studio for Mac 的 Solution Pad 中选择解决方案名称。

2. 在菜单栏中，选择“版本控制”>“在版本控制中发布”以显示“选择存储库”对话框   ：

    ![开始在 Visual Studio for Mac 中签出](media/version-control-git4-sml.png)

    如果此菜单项在菜单中变灰，请确保已选择解决方案名称。

3. 选择“已注册存储库”选项卡，然后按“添加”按钮   ：

    ![](media/version-control-git5.png)

4. 输入要在本地显示的存储库名称，然后粘贴步骤 #3 中的 URL。 “存储库配置”对话框应如下所示。 按“确定”：

    ![输入 Git 详细信息对话框](media/version-control-git6.png)

    此外也可使用 SSH 连接到 Git。

5. 要尝试将应用发布到 Git，请选择存储库，并确保“模块名称”和“信息”文本字段都已完成   ：

    ![尝试将应用发布到 Git](media/version-control-git7.png)

6. 单击“好的”，然后从警报对话框中单击“发布”   。

7. 在“Git 凭据”窗口中，输入你的 GitHub 用户名和密码  。 

> [!NOTE]
> 如果帐户已启用双因素身份验证 (2FA)，则需要创建一个访问令牌以用于替代密码。 如果尚未创建访问令牌，请按照 Git [访问令牌](https://help.github.com/articles/creating-an-access-token-for-command-line-use/)文档中的步骤进行操作。

8. 输入用户名和个人访问令牌，然后按“好的”  ：

    ![输入 Git 用户名和密码](media/version-control-git9-sml.png)

9. 几秒钟后，会发布初次提交的解决方案。 可通过浏览“版本控制”菜单项确认已将其发布，该菜单中应已填充了许多选项：

    ![“版本控制”菜单](media/version-control-git10.png)

10. 开始进行其他更改时，请选择“推送更改”  将更改推送到“远程”  存储库。 这可让所有相应的用户在 github.com 上进行查看：

    ![将更改推送到远程存储库](media/version-control-git11.png)

## <a name="publishing-a-new-project"></a>发布新项目

“新建项目”对话框可用于创建具有本地 git 存储库的新项目。 要启用该对话框，请选中“使用 git 进行版本控制”复选框，如以下屏幕截图所示  。 这将初始化存储库，并添加一个可选 .gitignore 文件：

![借助 git 支持创建新项目](media/version-control-git-publish-new1.png)

按照以下步骤将新的本地存储库推送到新的 GitHub 存储库中：

> [!NOTE]
> 如果尚未创建 GitHub 存储库，请参阅[在 GitHub 上创建远程存储库](#creating-a-remote-repo-on-github)部分。

1. 通过转到菜单栏中的“版本控制”>“查看解决方案并提交”，创建第一次提交  。

2. 在“状态”选项卡中，选择左上角的“提交”  。

3. 编写提交消息，例如“第一次提交”，然后单击“提交”  ：

    ![向 git 存储库提交初始更改](media/version-control-git-publish-new2.png)

4. 下一步，在“菜单栏”中，转到“版本控制”>“管理分支和远程”  。

5. 转到“远程源”选项卡，然后单击“添加”   。

6. 在“远程源”窗口中，添加先前创建的 GitHub 存储库的详细信息，然后单击“确定”   ：

    ![为 git 存储库配置远程源](media/version-control-git-publish-new3.png)

7. 关闭“Git 存储库配置”窗口，然后在“菜单栏”上转到“版本控制”>“推送更改”   。

8. 在“推送到存储库”窗口中，单击“推送更改”按钮   ：

    ![将更改推送到远程存储库](media/version-control-git-publish-new4.png)

9. 系统出现提示时，请输入 GitHub 用户名和密码。

> [!NOTE]
> 如果帐户已启用双因素身份验证 (2FA)，则需要创建一个访问令牌以用于替代密码。 如果尚未创建访问令牌，请按照 Git [访问令牌](https://help.github.com/articles/creating-an-access-token-for-command-line-use/)文档中的步骤进行操作。

Visual Studio for Mac 现在将更改推送到远程 GitHub 存储库中：

![推送操作成功完成确认](media/version-control-git11.png)

## <a name="check-out-an-existing-repository"></a>签出现有存储库

用户要使用的 GitHub 存储库很有可能仅存在于远程计算机上，而不在本地计算机上。 Visual Studio for Mac 允许快速签出此存储库。 请按以下步骤将其克隆到计算机上：

1. 在菜单栏中，选择“版本控制”>“签出”  ：

2. 随即显示“连接到存储库”  选项卡：

    ![输入了详细信息的“连接到存储库”选项卡](media/version-control-git13.png)

3. 在远程存储库的 GitHub 页上，按“克隆或下载”  按钮，然后复制提供的 URL：

    ![显示 github url](media/version-control-git14.png)

4. 在“连接到存储库”  选项卡中替换掉 **URL** 输入字段中的所有文本。这将为用户填充此选项卡中的其他大多数字段，如步骤 2 中的图像所示。

5. 输入要将存储库克隆到的目录并按“签出”  。

> [!NOTE]
> 如果存储库大小超过 4 GB，可能会遇到问题。

## <a name="troubleshooting"></a>疑难解答

如果在使用空的远程存储库初始化项目时遇到问题，可尝试执行以下步骤：

1. 转到解决方案文件夹。
1. 按 Command+Shift+.  以显示隐藏的文件和文件夹。
1. 若有 **.git** 文件夹，请删除它。
1. 若有 **gitignore** 文件，请删除它。
1. 按 Command+Shift+.  以隐藏文件和文件夹。
1. 在 VS for Mac 中打开解决方案。
1. 在 Solution Pad 上选择解决方案节点。
1. 浏览到“版本控制”菜单，并选择“在版本控制中发布”  。
1. 执行上述教程中的步骤 6 及之后的步骤。

## <a name="see-also"></a>请参阅

- [Visual Studio 中的版本控制 (Windows)](/visualstudio/version-control/)
