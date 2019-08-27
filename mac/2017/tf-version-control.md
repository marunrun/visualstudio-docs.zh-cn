---
title: Team Foundation 版本控制 (TFVC)
description: 使用 Team Foundation 版本控制 (TFVC) 从 Visual Studio for Mac 连接到 Team Foundation Server/Azure DevOps。
author: conceptdev
ms.author: crdun
ms.date: 06/25/2019
ms.topic: article
ms.technology: vs-ide-general
ms.assetid: 52D3D26A-4D01-4FD1-AAA1-AE7D7BD39746
ms.openlocfilehash: 52b40f8dbf24dd1e712bd0481e36f39cfcc1fc7d
ms.sourcegitcommit: 9d3529e40438ca45dcb0b31742c4cd5a89daa61e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/26/2019
ms.locfileid: "67398989"
---
# <a name="connecting-to-team-foundation-version-control"></a>连接到 Team Foundation 版本控制

> [!NOTE]
> 为了在 macOS 上获得最佳版本控制体验，建议使用 Git 而不是 Team Foundation 版本控制 (TFVC)。 Git 在 Visual Studio for Mac 中受支持，并且是托管在 Team Foundation Server (TFS)/Azure DevOps 中的存储库的默认选项。 要了解有关在 TFS/Azure DevOps 中使用 Git 的详细信息，请参阅[设置 Git 存储库](/visualstudio/mac/set-up-git-repository)一文。
>
> 如果您以前使用过 Visual Studio for Mac 的 TFVC 扩展的预览版本，则在升级到 Visual Studio 2019 for Mac 时，它不再受支持。

Azure Repos 提供了两种版本控制模型：[Git](/azure/devops/repos/git/?view=azure-devops)，它是分布式版本控制系统，以及 [Team Foundation 版本控制](/azure/devops/repos/tfvc/index?view=azure-devops) (TFVC)，它是集中式版本控制系统。

Visual Studio for Mac 提供了对 Git 存储库的全面支持，但需要一些解决方法才能使用 TFVC。 如果目前使用 TFVC 进行版本控制，可使用以下解决方案访问托管在 TFVC 中的源代码：

* [对于图形化 UI，请使用 Visual Studio Code 和 Azure Repos 扩展](#use-visual-studio-code-and-the-azure-repos-extension)
* [使用 Team Explorer Everywhere 命令行客户端 (TEE-CLC) 连接到存储库](#connecting-using-the-team-explorer-everywhere-command-line-client)
* [使用（不支持的）面向 Visual Studio for Mac 的 Team Foundation 版本控制扩展连接到 TFVC](#connect-to-tfvc-using-the-team-foundation-version-control-extension)

本文的其余部分将介绍上面列出的各个选项。

## <a name="requirements"></a>要求

* Visual Studio Community、Professional 或 Enterprise for Mac 7.8 和更高版本。
* Azure DevOps Services、Team Foundation Server 2013 及更高版本，或 Azure DevOps Server 2018 及更高版本。
* Azure DevOps Services 或 Team Foundation Server/Azure DevOps Server 中的项目，配置为使用 Team Foundation 版本控制。

## <a name="use-visual-studio-code-and-the-azure-repos-extension"></a>使用 Visual Studio Code 和 Azure Repos 扩展

如果要使用图形界面来管理版本控制中的文件，面向 Visual Studio Code 的 Azure Repos 扩展将提供来自 Microsoft 的支持的解决方案。 若要开始，请下载 [Visual Studio Code](https://code.visualstudio.com)，然后了解如何[配置 Azure Repos 扩展](https://marketplace.visualstudio.com/items?itemName=ms-vsts.team)。

## <a name="connecting-using-the-team-explorer-everywhere-command-line-client"></a>使用 Team Explorer Everywhere 命令行客户端进行连接

如果习惯使用 macOS 终端，Team Explorer Everywhere 命令行客户端 (TEE-CLC) 将提供一种受支持的方法，以连接到 TFVC 中的源。

可以按照以下步骤设置到 TFVC 的连接并提交更改。

### <a name="setting-up-the-tee-clc"></a>设置 TEE-CLC

有两种方法可以设置 TEE-CLC。

* 使用 Homebrew 安装客户端，或
* 下载并手动安装客户端

最简单的解决方案是使用 HomeBrew  ，它是适用于 macOS 的包管理器。 若要使用此方法进行安装：

1. 启动 macOS 终端应用程序。
1. 使用终端和 [Homebrew 主页](https://brew.sh/)上的说明安装 Homebrew。
1. 安装 Homebrew 后，从终端运行以下命令：`brew install tee-clc`

若要手动设置 TEE-CLC  ：

1. 从 Team Explorer Everywhere GitHub 存储库的版本页[下载 tee-clc 的最新版本](https://github.com/Microsoft/team-explorer-everywhere/releases)（例如撰写本文时的 tee-clc-14.134.0.zip）。
1. 将 .zip 的内容提取到磁盘上的一个文件夹中。
1. 打开 macOS 终端应用，使用 `cd` 命令切换到上一步骤中使用的文件夹。
1. 从文件夹中运行命令 `./tf` 来测试命令行客户端是否可以运行，可能会提示你安装 Java 或其他依赖项。

安装 TEE-CLC 后，可以运行命令 `tf eula` 来查看和接受客户端的许可协议。

最后，要在 TFS/Azure DevOps 环境中进行身份验证，需要在服务器上创建一个个人访问令牌。 详细了解如何[使用个人访问令牌进行身份验证](https://docs.microsoft.com/azure/devops/integrate/get-started/authentication/pats?view=azure-devops)。 当创建要与 TFVC 一起使用的个人访问令牌时，请确保在配置令牌时提供完全访问权限。

### <a name="using-the-tee-clc-to-connect-to-your-repo"></a>使用 TEE-CLC 连接到存储库

若要连接到源代码，首先需要使用 `tf workspace` 命令创建工作区。 例如，以下命令连接到 Azure DevOps Services 中名为“MyOrganization”的组织： 

```bash
export TF_AUTO_SAVE_CREDENTIALS=1
tf workspace -new MyWorkspace -collection:https://dev.azure.com/MyOrganization
```

`TF_AUTO_SAVE_CREDENTIALS` 环境设置用于保存凭据，因此不会提示你多次输入凭据。 当系统提示输入用户名称时，使用在上一节中创建的个人访问令牌，并使用空白密码。

要创建到本地文件夹的源文件的映射，请使用 `tf workfold` 命令。 下面的示例将从“MyRepository”TFVC 项目映射一个名为“WebApp.Services”的文件夹，并将其设置为复制到本地 ~/Projects/ 文件夹中（即当前用户的主文件夹中的“Projects”文件夹）。

```bash
tf workfold -map $/MyRepository/WebApp.Services -workspace:MyWorkspace ~/Projects/
```

最后，使用以下命令从服务器获取源文件并在本地复制：

```bash
tf get
```

### <a name="committing-changes-using-the-tee-clc"></a>使用 TEE-CLC 提交更改

在 Visual Studio for Mac 中对文件进行更改后，可以切换回终端以检查编辑。 `tf add` 命令用于将文件添加到待签入的挂起的更改列表中，`tf checkin` 命令执行对服务器的实际签入。 `checkin` 命令包含用于添加注释或关联相关工作项的参数。 在下面的代码片段中，`WebApp.Services` 文件夹中的所有文件都以递归方式添加到签入。 然后，用注释签入代码，并与 ID 为“42”的工作项关联。

```bash
cd WebApp.Services
tf add * /recursive
tf checkin -comment:"Replaced 'Northwand' typos with the correct word Northwind" -associate:42
```

若要详细了解有关此处提到的命令或其他命令，可在终端使用以下命令：

`tf help`

## <a name="connect-to-tfvc-using-the-team-foundation-version-control-extension"></a>使用 Team Foundation 版本控制扩展连接到 TFVC

> [!NOTE]
> 为了在 macOS 上获得最佳版本控制体验，建议使用 Git 而不是 Team Foundation 版本控制 (TFVC)。 Git 在 Visual Studio for Mac 中受支持，并且是托管在 Team Foundation Server (TFS)/Azure DevOps 中的存储库的默认选项。 要了解有关在 TFS/Azure DevOps 中使用 Git 的详细信息，请参阅[设置 Git 存储库](/visualstudio/mac/set-up-git-repository)一文。
>
> 如果您以前使用过 Visual Studio for Mac 的 TFVC 扩展的预览版本，则在升级到 Visual Studio 2019 for Mac 时，它不再受支持。

在 Visual Studio for Mac 扩展库中，有一个 Team Foundation 版本控制扩展，它提供对连接到 TFVC 的有限支持。 该扩展不受支持，并且存在几个已知问题，因此在使用它时，体验可能会有所不同。

要安装扩展，请启动 Visual Studio for Mac 并选择“Visual Studio”>“扩展”  菜单。 在“库”  选项卡中，选择“版本控制”>“适用于 TFS 和 Azure DevOps 的 Team Foundation 版本控制”  ，然后单击“安装...”  ：

![扩展管理器](media/tfvc-install.png)

按照提示安装扩展。 安装后，重启 IDE。

### <a name="updating-the-extension"></a>更新扩展

TFVC 扩展定期更新。 若要访问更新，请从菜单中选择“Visual Studio”>“扩展...”，然后选择“更新”选项卡   。从列表中选择扩展，然后选择“更新”按钮  ：

选择下一对话框中的“安装”来卸载旧包并安装新包  。

### <a name="using-the-extension"></a>使用扩展

安装扩展后，选择“版本控制”>“TFS/Azure DevOps”>“从远程存储库打开...”  菜单项。

![用于打开扩展的菜单项](media/tfvc-source-control-explorer-devops.png)

选择 VSTS 或 Team Foundation Server 以开始使用，然后选择“继续”  ：

![与服务器连接](media/tfvc-choose-server-type-devops.png)

#### <a name="azure-repos-authentication"></a>Azure Repos 身份验证

选择在 Azure Repos 上托管的项目时，系统会提示输入 Microsoft 帐户详细信息：

![与 Azure Repos 连接](media/tfvc-vsts-login.png)

#### <a name="tfs-authentication"></a>TFS 身份验证

若要连接到 TFS，请输入服务器详细信息和帐户凭据。 若要使用 NTLM 身份验证，请输入域；若要使用基本身份验证，则留空。 选择“添加服务器”  ：

![登录 TFS 服务器](media/tfvc-login.png)

### <a name="selecting-a-project"></a>选择项目

成功通过身份验证后，可在“在源代码管理中打开”对话框中看到与帐户关联的存储库的列表  ：

![显示项目的“在源代码管理中打开”对话框](media/tfvc-vsts-projects.png)

此对话框分为以下节点：

- Azure DevOps 组织或集合 - 这显示连接到所登录 Microsoft 帐户的所有组织。
- 项目 - 在每个组织或集合中，可以拥有许多项目。 项目中托管源代码、工作项和自动生成。

现在可按项目或组织的名称进行搜索和筛选。

#### <a name="adding-a-new-server"></a>添加新服务器

若要将新服务器添加到列表，请在“在源代码管理中打开”对话框中选择“添加主机”按钮   ：

![突出显示的添加按钮，用于将新服务器添加到列表](media/tfvc-add-new-server.png)

从列表中选择提供程序并输入凭据：

![显示源代码管理提供程序的选项的对话框](media/tfvc-add-new-creds-devops.png)

### <a name="creating-a-new-workspace"></a>创建一个新工作区

若要开始使用项目，则需具备“工作区”  。 如果还没有工作区，可通过“在源代码管理中打开”对话框中的“工作区”组合框进行创建   ：

![创建新工作区组合框选项](media/tfvc-create-new-workspace.png)

设置新工作区的名称和本地路径，并选择“创建工作区”  :

![输入新工作区的名称和本地路径](media/tfvc-local-workspace.png)

### <a name="using-the-source-code-explorer"></a>使用源代码资源管理器

创建工作区并映射项目后，则可开始使用“源代码资源管理器”  。

若要打开源代码资源管理器，请选择“版本控制”>“TFS/Azure DevOps”>“源代码管理器”菜单项  。

利用源代码资源管理器可以浏览所有映射的项目及其文件和文件夹。 还可以执行所有基本源代码管理操作，例如：

- 获取最新版本
- 获取特定版本
- 签入和签出文件
- 锁定和解锁文件
- 添加、删除和重命名文件
- 查看历史记录
- 比较更改。

许多这些操作都可以通过项目的上下文操作实现：

![项目的上下文菜单操作](media/tfvc-sourcecode-actions.png)

### <a name="managing-workspaces"></a>管理工作区

如果尚未创建工作区（如[创建工作区](#creating-a-new-workspace)部分所述），则会发现源代码资源管理器是空的：

![空源代码资源管理器](media/tfvc-setup-empty-sce.png)

若要使用本地工作区设置远程项目，请执行以下步骤：

1. 从组合框中选择“服务器”  。
1. 请注意，此时显示“无工作区”，并且本地路径为“未映射”。 选择“未映射”链接，以显示“创建新工作区”对话框   。
1. 为工作区提供一个名称，然后单击“添加工作文件夹”，将项目映射到计算机上的本地文件夹  ：

    ![显示默认选项的“创建新工作区”对话框](media/tfvc-workspace1.png)

1. 选择“$”文件夹，将服务器上的所有项目映射到同一工作区；或选择单个项目，然后单击“确定”  ：

    ![显示所有项目的“浏览文件夹”对话框](media/tfvc-workspace2.png)

1. 在本地计算机上选择希望将项目映射到的位置，然后单击“选择文件夹”  。
1. 选择“确定”，确认新工作区的详细信息后 

    ![添加了工作文件夹的“创建新工作区”对话框](media/tfvc-workspace3.png)

设置工作区后，可通过单击源代码资源管理器中的“管理工作区”按钮来进行更改或将其删除  。

![管理工作区](media/tfvc-workspace4.png)

## <a name="troubleshooting-and-known-issues"></a>疑难解答和已知问题

#### <a name="problems-using-basic-authentication"></a>使用基本身份验证的问题

可使用以下选项对服务器进行身份验证：

- Oauth
- Basic
- Ntlm

若要使用基本身份验证，需要在 Azure DevOps Services 中启用“其他身份验证凭据”，具体步骤如下  ：

1. 以所有者身份登录到 Azure DevOps 组织 (https:\//dev.azure.com/{organization}/{project})。

2. 在组织工具栏中，选择齿轮图标，然后选择“策略”  ：

    ![选中的策略设置选项](media/tfvc-auth2.png)

3. 查看应用程序连接设置。 根据安全策略更改这些设置：

    ![选中的策略设置选项](media/tfvc-auth.png)

#### <a name="i-do-not-see-anything-in-tfvc"></a>我在 TFVC 中没有看到任何内容

若要在开发计算机上设置 Team Foundation 版本控制 (TFVC)，必须按照[管理工作区](#managing-workspaces)部分所述创建工作区  。

在源代码管理器中，按“管理工作区”按钮  。 按照步骤将项目映射到开发计算机上的文件夹。

#### <a name="i-do-not-see-any--all-of-my-projects"></a>我没有看到任何/所有项目

身份验证后，应该可以看到项目列表。 默认情况下，只显示 TFS 项目。 要查看其他类型的项目，请选中“查看所有项目”框。

请记住，只有权限正确，才会显示服务器上的项目。

##### <a name="i-am-getting-the-error-cannot-create-the-workspace-please-try-again"></a>我收到“无法创建工作区， 请重试”错误

尝试[创建新工作区](#creating-a-new-workspace)时，应确保满足以下条件：

- 工作区名称中不可使用无效字符。
- 名称必须少于 64 个字符。
- 任何其他工作区都不能使用本地路径。

### <a name="see-also"></a>请参阅

- [使用 Visual Studio 开发和共享 TFVC 中的代码 (Windows)](/azure/devops/repos/tfvc/share-your-code-in-tfvc-vs)