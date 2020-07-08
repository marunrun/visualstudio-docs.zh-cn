---
title: Team Foundation 版本控制 (TFVC)
description: 有关 TFVC 和 macOS 的疑难解答指南。
author: jmatthiesen
ms.author: jomatthi
ms.date: 09/02/2019
ms.technology: vs-ide-general
ms.assetid: 52D3D26A-4D01-4FD1-AAA1-AE7D7BD39746
ms.topic: troubleshooting
ms.openlocfilehash: c51f3cd50598cd0c33b019c09f95554cc5f9058b
ms.sourcegitcommit: 5335a9864d5747bc917ed28d4ebeade3076b10e7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2020
ms.locfileid: "85950494"
---
# <a name="does-visual-studio-for-mac-support-team-foundation-version-control"></a>Visual Studio for Mac 是否支持 Team Foundation 版本控制？

> [!CAUTION]
> Visual Studio for Mac 的 TFVC 扩展的预览版本在 Visual Studio 2019 for Mac 中已不再受支持。


## <a name="alternative-version-control-options-in-visual-studio-for-mac"></a>Visual Studio for Mac 中的备用版本控制选项

为了在 macOS 上获得最佳版本控制体验，建议使用 Git 而不是 Team Foundation 版本控制 (TFVC)。 

Git 在 Visual Studio for Mac 中受支持，并且是托管在 Team Foundation Server (TFS)/Azure DevOps 中的存储库的默认选项。 要了解有关在 TFS/Azure DevOps 中使用 Git 的详细信息，请参阅[设置 Git 存储库](/visualstudio/mac/set-up-git-repository)指南。

## <a name="unsupported-workarounds-for-tfvc"></a>TFVC 不受支持的解决方法

虽然 Visual Studio for Mac 并未正式支持 TFVC，但本指南的其余部分提供了一些在 macOS 上使用 TFVC 的解决方法。 如果目前使用 TFVC 进行版本控制，可使用以下解决方案访问托管在 TFVC 中的源代码：

* 选项 1. [对于图形化 UI，请使用 Visual Studio Code 和 Azure Repos 扩展](#use-visual-studio-code-and-the-azure-repos-extension)
* 选项 2. [使用 Team Explorer Everywhere 命令行客户端 (TEE-CLC) 连接到存储库](#connecting-using-the-team-explorer-everywhere-command-line-client)

### <a name="option-1--use-visual-studio-code-and-the-azure-repos-extension"></a>选项 1. <a id="use-visual-studio-code-and-the-azure-repos-extension"></a> 使用 Visual Studio Code 和 Azure Repos 扩展

如果要使用图形界面来管理版本控制中的文件，面向 Visual Studio Code 的 Azure Repos 扩展将提供来自 Microsoft 的支持的解决方案。 若要开始，请下载 [Visual Studio Code](https://code.visualstudio.com)，然后了解如何[配置 Azure Repos 扩展](https://marketplace.visualstudio.com/items?itemName=ms-vsts.team)。

### <a name="option-2--connecting-using-the-team-explorer-everywhere-command-line-client"></a>选项 2. <a id="connecting-using-the-team-explorer-everywhere-command-line-client"></a> 使用 Team Explorer Everywhere 命令行客户端进行连接

> [!IMPORTANT]
> 根据 Team Explorer Everywhere README 的说明，此项目[不再维护](https://github.com/microsoft/team-explorer-everywhere)。

如果习惯使用 macOS 终端，Team Explorer Everywhere 命令行客户端 (TEE-CLC) 将提供一种受支持的方法，以连接到 TFVC 中的源。

可以按照以下步骤设置到 TFVC 的连接并提交更改。

#### <a name="setting-up-the-tee-clc"></a>设置 TEE-CLC

有两种方法可以设置 TEE-CLC。

* 使用 Homebrew 安装客户端，或
* 下载并手动安装客户端

最简单的解决方案是使用 HomeBrew，它是适用于 macOS 的包管理器。 若要使用此方法进行安装：

1. 启动 macOS 终端应用程序。
1. 使用终端和 [Homebrew 主页](https://brew.sh/)上的说明安装 Homebrew。
1. 安装 Homebrew 后，从终端运行以下命令：`brew install tee-clc`

若要手动设置 TEE-CLC：

1. 从 Team Explorer Everywhere GitHub 存储库的版本页[下载 tee-clc 的最新版本](https://github.com/Microsoft/team-explorer-everywhere/releases)（例如撰写本文时的 tee-clc-14.134.0.zip）。
1. 将 .zip 的内容提取到磁盘上的一个文件夹中。
1. 打开 macOS 终端应用，使用 `cd` 命令切换到上一步骤中使用的文件夹。
1. 从文件夹中运行命令 `./tf` 来测试命令行客户端是否可以运行，可能会提示你安装 Java 或其他依赖项。

安装 TEE-CLC 后，可以运行命令 `tf eula` 来查看和接受客户端的许可协议。

最后，要在 TFS/Azure DevOps 环境中进行身份验证，需要在服务器上创建一个个人访问令牌。 详细了解如何[使用个人访问令牌进行身份验证](/azure/devops/integrate/get-started/authentication/pats?view=azure-devops)。 当创建要与 TFVC 一起使用的个人访问令牌时，请确保在配置令牌时提供完全访问权限。

#### <a name="using-the-tee-clc-to-connect-to-your-repo"></a>使用 TEE-CLC 连接到存储库

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

#### <a name="committing-changes-using-the-tee-clc"></a>使用 TEE-CLC 提交更改

在 Visual Studio for Mac 中对文件进行更改后，可以切换回终端以检查编辑。 `tf add` 命令用于将文件添加到待签入的挂起的更改列表中，`tf checkin` 命令执行对服务器的实际签入。 `checkin` 命令包含用于添加注释或关联相关工作项的参数。 在下面的代码片段中，`WebApp.Services` 文件夹中的所有文件都以递归方式添加到签入。 然后，用注释签入代码，并与 ID 为“42”的工作项关联。

```bash
cd WebApp.Services
tf add * /recursive
tf checkin -comment:"Replaced 'Northwand' typos with the correct word Northwind" -associate:42
```

若要详细了解有关此处提到的命令或其他命令，可在终端使用以下命令：

`tf help`

## <a name="see-also"></a>请参阅

- [使用 Visual Studio 开发和共享 TFVC 中的代码 (Windows)](/azure/devops/repos/tfvc/share-your-code-in-tfvc-vs)