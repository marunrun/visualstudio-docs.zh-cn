---
title: 自定义 codespace（预览）
description: 了解有关如何自定义 codespace 的详细信息。
ms.topic: how-to
ms.date: 09/21/2020
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
ms.workload:
- multiple
monikerRange: vs-2019
ms.openlocfilehash: f63dc4989a59256a0a3ad59491b2290912ffd2f8
ms.sourcegitcommit: 062615c058d2ff44751e8d0c704ccfa3c5543469
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/22/2020
ms.locfileid: "90862296"
---
# <a name="how-to-customize-a-codespace-preview"></a>如何自定义 codespace（预览）

GitHub Codespaces 在云中提供完整的开发环境。 对于使用 Visual Studio 2019 的基于 Windows 的开发，GitHub Codespaces 默认实例提供了一个很好的起点，但你也可以为特定项目自定义环境。

## <a name="installed-software"></a>安装的软件

Windows codespace 附带了许多已安装的框架和工具，因此你可以立即开始。 下表列出了所有 Windows codespace 环境中可用的应用程序和功能。

| 应用                                         | 路径别名 | 版本            |
|---------------------------------------------|------------|--------------------|
| .NET                                        | 空值        | 4.8                |
| .NET Core 运行时                           | dotnet     | 2.1, 3.1           |
| .NET Core SDK                               | dotnet     | 2.1, 3.1.3, 3.1.4  |
| Azure CLI                                   | az         | 2.5                |
| Chocolatey                                  | choco      | 0.10.15            |
| CMake                                       | cmake      | 3.17               |
| Git                                         | git        | 2.26               |
| Microsoft build                             | msbuild    | 16.7               |
| Microsoft SQL Server Express Edition 2019   | 空值        | 15.0               |
| Ninja                                       | ninja      | 1.8.2              |
| Node.js                                     | 节点       | 12.16              |
| NPM                                         | npm        | 6.14               |
| Python                                      | Python     | 3.7                |
| VC 包管理器                          | vcpkg      | 2020.02            |
| Windows SDK                                 | 空值        | 10.0.18362         |

上面的列表并不详尽，未包括 Visual Studio 安装的许多工具（例如 IISExpress）。 组件还可能具有与上述版本不同的次要版本或补丁版本。

以下[已安装软件的详细说明](#installed-software-specifics)部分提供了有关预安装的框架和工具的特定详细信息。

## <a name="modifications-to-a-codespace"></a>对 codespace 的修改
 
创建 codespace 后，对该特定 codespace 所做的任何更改都将保留，而该 codespace 实例在 GitHub Codespaces 上可用。 你可以克隆其他存储库、安装工具和应用程序生成器，还可以添加其他开发资产，这些修改将保留，即使 codespace 暂停后也是如此。 但是，如果删除 codespace，则任何修改都将丢失。

> [!NOTE]
> 如果删除 codespace，则在 codespace 中对本地存储库的任何更改（挂起或提交）都将丢失。 删除 codespace 之前，请务必将存储库更改推送到远程位置。

使用 Visual Studio 连接 codespace 时，可以使用 Visual Studio 终端运行命令行工具。 可以使用 PowerShell 或 Windows 命令提示符，二者都在本地管理员帐户下进行了提升。 若要了解有关 Visual Studio 终端的详细信息，请参阅 [Visual Studio 终端公告博客](https://devblogs.microsoft.com/visualstudio/say-hello-to-the-new-visual-studio-terminal/)。

## <a name="customize-a-codespace"></a>自定义 codespace

GitHub Codespaces 的真正价值在于，你可以在云中创建独特的、可重复的开发环境，该环境专为你自己的工作以及团队的工作量身定制。 通过在默认的 GitHub Codespaces 实例上构建，你可以自定义在创建新的 codespace 时要安装和配置的内容。

下一部分将介绍使用 .devcontainer.json 和 .devinit.json 文件的两种 codespace 配置方法 。 通过这些文件，你可以为 codespace 配置安装框架和工具，并且在将其添加到存储库后，任何基于你的存储库创建 codespace 的人都将具有相同的远程开发环境。

## <a name="customize-with-devcontainerjson"></a>自定义 devcontainer.json

创建 codespace 后，GitHub Codespaces 将在存储库的根目录中查找 [devcontainers.json](https://code.visualstudio.com/docs/remote/devcontainerjson-reference) 文件，并使用其中的设置来自定义 codespace 或与其连接的客户端实例（基于浏览器的编辑器、Visual Studio 或 Visual Studio Code）。 大多数 devcontainer.json 设置都适用于基于 Linux 的 codespace 或其他两个客户端，但某些设置适用于 Windows codespace 和 Visual Studio。

devcontainer.json 文件可置于存储库中的以下两个位置之一：

1. {repository-root}/.devcontainer.json
2. {repository-root}/.devcontainer/devcontainer.json

GitHub Codespaces 支持以下 devcontainer.json 属性。 如果希望通过 Visual Studio 之外的其他客户端连接到 codespace，建议设置 Visual Studio Code 特定的属性。 

* `extensions` - 应安装的一组 [Visual Studio Code Marketplace](https://marketplace.visualstudio.com/vscode) 扩展。
* `settings` - 要应用的一组 [Visual Studio Code 设置](https://code.visualstudio.com/docs/getstarted/settings)。
* `forwardPorts` - 运行 codespace 时应在本地自动转发的端口。
* `postCreateCommand` - 创建 codespace 后要运行的命令字符串或命令参数列表。

> [!NOTE]
> devcontainer.json 文件还用于支持 Visual Studio Code [远程开发](https://code.visualstudio.com/docs/remote/remote-overview)，并具有本文档未涵盖的其他属性。 可以放心将这些其他属性添加到文件中，但 Codespaces 将忽略这些属性。 有关详细信息，请参阅 code.visualstudio.com 上的 [devcontainer.json 参考](https://code.visualstudio.com/docs/remote/devcontainerjson-reference)。

## <a name="customize-with-devinit"></a>使用 devinit 进行自定义

[devinit](../../devinit/getting-started-with-devinit.md) 是 Windows codespace 中包含的命令行工具，可用于在环境中安装框架和工具。 可以从命令提示符 (`devinit -t require-dotnetcoresdk`) 手动运行该工具，但该工具真正强大之处在于，可用于创建自定义 [.devinit.json](../../devinit/devinit-json.md) 文件，以便在每次创建 codespace 时统一进行配置。

`devinit` 包括一组用于安装特定项的工具（例如 SQL Server 和 Azure CLI），以及用于运行常规包管理器的工具（例如 chocolatey、npm 和 vcpkg）。 可以在[可用工具](../../devinit/devinit-tool-list.md)文档中找到 `devinit` 工具的完整列表。

### <a name="devinitjson"></a>devinit.json

尽管可以直接运行 `devinit` 命令行，但建议创建 [devinit.json](../../devinit/devinit-json.md) 配置文件，用于描述要运行的一组 `devinit` 工具。 

例如，若要安装 [.NET Core SDK](https://docs.microsoft.com/dotnet/core/sdk)，则 .devinit.json 应如下所示：

```json
{
    "run": [
        {
            "comments": "We need the .NET Core SDK."
            "tool": "require-dotnetcoresdk"
        }
    ]
}
```

在项目的根目录中创作 .devinit.json 文件时，将在运行 `devinit init` 时使用该文件。 默认情况下，`devinit.exe` 在以下位置查找该文件：

1. *{current-directory}\\.devinit.json*
2. *{current-directory}\\.devinit\devinit.json*

### <a name="running-devinit-when-creating-a-codespace"></a>创建 codespace 时运行 devinit

使用 devcontainers.json 文件中的 `postCreateCommand` 属性创建 codespace 后，可以指示 GitHub Codespaces 运行 `devinit`。 如上所述，GitHub Codespaces 将在克隆的存储库中查找 devcontainer.json 文件，以便自定义 codespace 或客户端实例，它还将运行 `postCreateCommand` 属性中所述的任何命令。

通过指定 `devinit init`，`devinit` 将使用 devinit.json 配置运行。

```json
{
  "postCreateCommand": "devinit init"
}
```

### <a name="an-example"></a>示例

下面是有关安装 .NET Core Entity Framework 命令行工具 `dotnet-ef` 的简单示例。

**devcontainer.json**

存储库根中的 .devcontainer.json 文件的内容。 

```json
{
  "postCreateCommand": "devinit init"
}
```

**devinit.json**

.devinit.json 文件的内容。 该文件需要与 .devcontainer.json 位于相同的文件夹中。

```json
{
    "run": [
        {
            "comments": "Install the Entity Framework tools",
            "tool": "dotnet-toolinstall",
            "input": "dotnet-ef",
        }
     ]
}
```

可在 `devinit` [示例列表](../../devinit/sample-readme.md)中找到更多 `devinit` 示例。

## <a name="port-forwarding"></a>端口转发

GitHub Codespaces 通过端口转发提供对在远程环境中运行的应用程序和服务的访问。 默认情况下，出于安全考虑，不会转发任何端口。 不过，你可以指定要在 codespace 中打开的某些端口。

### <a name="configure-port-forwarding"></a>配置端口转发

如果默认情况下存在应为给定存储库转发的一个或多个端口，则可以在 devcontainer.json 中使用 `forwardPorts` 属性进行配置。

* `forwardPorts` - 运行环境时应在本地自动转发的端口。

## <a name="installed-software-specifics"></a>已安装的软件的详细信息

### <a name="microsoft-sql-server"></a>Microsoft SQL Server

Microsoft SQL Server 2019 Express Edition 可用，并在 Windows Codespace 环境中作为本地服务 (localdb) 运行。 当前用户（应用和 Visual Studio 终端运行时的身份）对 SQL Server 具有 SQL 管理员权限。 若要管理服务器，将需要使用 Visual Studio 终端或其他命令行工具（如 `dotnet-ef`）中的 PowerShell。 SQL Server Management Studio 和其他远程管理工具当前不可用。

#### <a name="example-connection-string"></a>连接字符串示例

下面是连接到本地 MS SQL Server 的连接字符串示例。

```csharp
"Server=(LocalDB);Integrated Security=true;"
```

### <a name="azure-cli"></a>Azure CLI

Azure CLI 安装在所有 Windows Codespace 环境中，并在路径中以 `az` 的形式提供。

#### <a name="using-azure-resources"></a>使用 Azure 资源

如果使用 Azure Active Directory 标识对 Azure 资源的应用程序进行身份验证，则需要先从 Visual Studio 终端登录到 Azure。 登录时，请使用带有设备登录流的 Azure CLI `login` 命令（如以下示例中所示）。 登录后，应用程序和终端会话应能够使用该标识。

```powershell
> az login --use-device-code
```

有关详细信息，请参阅 Azure CLI [文档](/cli/azure/reference-index#az_login)中的 `az login` 命令。

## <a name="see-also"></a>另请参阅

- [什么是 GitHub Codespaces？](codespaces-overview.md)
- [如何将 Visual Studio 用于 codespace](use-visual-studio-with-codespaces.md)