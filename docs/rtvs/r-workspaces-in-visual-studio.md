---
title: R 工作区
description: 如何通过使用 Visual Studio 中的工作区控制 R 代码的运行位置。
ms.date: 01/24/2018
ms.topic: conceptual
author: kraigb
ms.author: kraigb
manager: jillfra
ms.workload:
- data-science
ms.openlocfilehash: 97ce4f226c39a20ad41c5977f800aa178450c69c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89314935"
---
# <a name="control-where-r-code-runs-with-workspaces"></a>控制 R 代码在工作区中的运行位置

在针对 Visual Studio 的 R 工具 (RTVS) 中的工作区可以配置 R 会话运行的位置，既可以在本地计算机运行，也可以在远程计算机运。 其目的是让你在工作时获得不相上下的用户体验，同时能够利用潜在的、更强大的基于云的计算机。

要打开“工作区”窗口，请使用“R 工具” > “Windows” > “工作区”命令，或按 Ctrl+9。

![针对 Visual Studio (VS2017) 的 R 工具中的工作区](media/workspaces-window.png)

在此窗口中，绿色选中标记表示 RTVS 绑定的活动工作区。 选择蓝色箭头来设置活动工作区。 通过每个工作区右侧的设置（齿轮）图标可更改工作区的名称、位置和命令行参数。 使用红色 X 可删除手动添加的工作区。

## <a name="save-and-reset-a-workspace"></a>保存和重置工作区

默认情况下，在关闭和重新打开项目时，RTVS 将不会保存工作区状态。 但是，可以通过[工作区选项](options-for-r-tools-in-visual-studio.md#workspace)更改此行为。

也可随时使用“R 工具” > “会话” > “重置”命令以及交互窗口中的重置工具栏按钮重置工作区状态。 对于远程工作区，重置会删除首次连接到远程服务器时所创建的用户配置文件，从而有效地删除那里积累的所有文件。

## <a name="local-workspaces"></a>本地工作区

本地工作区列表显示所有安装在计算机上的 R 解释器。

启动时，Visual Studio 会尝试浏览 HKEY_LOCAL_MACHINE\Software\R-Core\\ 注册表项，以自动检测已安装的所有 R 版本。 由于仅在启动时执行此检查，因此安装新的 R 解释器时需要重启 Visual Studio。

RTVS 可能无法检测以非标准方式（例如，仅仅将文件复制到文件夹，而不是运行安装程序）安装的 R 解释器。 在这种情况下，请按下列步骤手动创建新的本地 R 工作区：

1. 在“工作区”窗口，选择“添加”  按钮。
1. 输入新工作区的名称。
1. 输入 R 根文件夹的路径（包含带解释器的 bin 文件夹），同时输入 RTVS 启动它时要传递给解释器的所有可选命令行参数  。
1. 完成操作后，选择“保存”  。

![添加一个新工作区](media/workspaces-add-new.png)

## <a name="remote-workspaces"></a>远程工作区

通过远程工作区可连接到远程计算机上的 R 会话。 （要如何配置计算机以实现此目的，请参阅[设置远程工作区](setting-up-remote-r-workspaces.md)。）

Visual Studio 不会自动检测远程工作区，因此必须使用“工作区”窗口中的“添加”按钮手动添加远程工作区（如上一节中所述）  。 在这种情况下，请输入远程计算机的 URI 而非本地路径。

> [!Important]
> 远程工作区必须由使用 HTTPS 协议的 URI 标识，以保证与远程计算机之间通信的隐私和完整性。  Visual Studio 无法连接到不支持 HTTPS 的远程计算机。

> [!Note]
> 远程工作区在预览中有效。 我们正在努力解决文件同步问题，希望在未来版本中实现优化，欢迎提供想法和反馈。

## <a name="remote-workspace-logon"></a>远程工作区登录

必须使用用户名和密码才能登录到远程工作区。

### <a name="logon-to-windows-workspace"></a>登录到 Windows 工作区

如果远程计算机设置为使用域帐户，则可以使用域登录名访问远程工作区。 如果不是，则必须使用远程计算机上的计算机帐户以 `machine-name\username` 格式登录。

### <a name="logon-to-linux-workspace"></a>登录到 Linux 工作区

若要登录到 Linux 帐户，请使用 `<<unix>>\username` 格式。 例如，如果帐户名称为 `ruser`，则应以 `<<unix>>\ruser` 的形式键入用户名。

## <a name="switch-between-workspaces"></a>在工作区间进行切换

RTVS 一次仅绑定到一个工作区中。 绑定的工作区通过“工作区”窗口中的绿色小复选标记来指示。 RTVS 默认会绑定到在上个会话中最近打开的本地工作区。

要更改活动工作区，请选择所需工作区旁的蓝色箭头。 执行此操作后，系统会提示保存会话，终止当前工作区，然后切换到新的工作区。

> [!Tip]
> 要禁用保存提示，请选择“R 工具” > “选项”命令，然后将[在切换工作区前显示“确认”对话框]选项设置为 `No`。 请参阅[工作区选项](options-for-r-tools-in-visual-studio.md#workspace)。

如果尝试切换到已卸载的本地工作区或不可用的远程工作区，则 RTVS 有可能不会绑定到任何工作区。 结果，在交互窗口输入代码时，或尝试运行其他代码时，会出现错误：

![工作区未绑定到 RTVS 时出错](media/workspaces-disconnected-interactive-window.png)

要更正此问题，请在“工作区”窗口中切换到其他工作区。 如果所有工作区都不可用，则需安装 R 解释器。 在 Visual Studio 运行期间，如果已安装解释器，还可以尝试重启 Visual Studio。

### <a name="switch-to-a-remote-workspace"></a>切换到远程工作区

首次连接远程工作区时，RTVS 将提示输入凭据，并为后面的会话缓存这些凭据（使用安全 Windows 凭据保险箱）。 然后就可以通过 HTTPS（必需）与远程服务器安全通信。

根据服务器的配置，在连接时有可能遇到证书警告，内容如下“远程 R 服务提供的安全证书阻止我们证明你确实正连接到计算机（名称）。”

![连接到远程工作区时的自签名证书警告](media/workspaces-remote-self-signed-certificate-warning.png)

证书是一个文档，由正在尝试连接到的计算机呈现给 RTVS。 证书包含用于标识该计算机 URI 的字段。 RTVS 检测到证书中 URI 和连接计算机所用 URI 不匹配时，系统将发出警告，指示服务器的安全性可能已遭破坏。

但是如果已使用自签名证书在远程计算机上启用 HTTPS，而不是使用来自受信任提供程序的证书，也会出现此警告  。 有关详细信息，请参阅[设置远程工作区](setting-up-remote-r-workspaces.md)。

## <a name="directories-on-local-and-remote-computers"></a>本地和远程计算机上的目录

在本地工作区启动新的 R 解释器时，当前的工作目录默认为 %userprofile%\Documents  。 可通过以下方式随时更改目录：使用“R 工具” > “工作目录”命令，或者在 Visual Studio 解决方案资源管理器中右键单击项目，然后选择“在此设置工作目录”之类的命令。

首次连接到远程计算机时，RTVS 会自动基于凭据创建用户配置文件，这会将工作目录设置为该配置文件下的“文档”文件夹  。 所有使用相同凭据的后续远程会话都会用到此文件夹。

因此，对于本地和远程工作区而言，运行代码的确切位置可以有所不同。 然后在代码中始终使用数据文件的相对路径，这样，代码便可在工作区间移植。

另请注意，对于远程工作区，工作目录中的所有文件在相同用户配置文件的会话中仍保持在原来位置。 如前文所述，在使用远程工作区时，可通过“R 工具” > “会话” > “重置”命令（或交互窗口中的重置按钮）删除这些文件。 此命令会再次从服务器删除重新连接时重新创建的用户配置文件。

## <a name="copy-project-files-to-remote-workspaces"></a>将项目文件复制到远程工作区

在 Visual Studio 中处理 R 项目时，即使正使用远程工作区，本地计算机也会拥有最新项目文件。 即，在 Visual Studio 中打开项目时（这通常意味着打开一个包含该项目的解决方案），RTVS 会假定项目内容完全驻留在本地计算机上。 实际上，远程工作区仅是项目文件的临时主机，以及任何来自代码的输出。 这意味着，例如要在交互窗口中使用 `source` 加载文件，则该文件必须已经在所提供路径的远程计算机上，或者，必须在远程 R 解释器的当前工作目录（使用 `setwd()` 函数设置）。

将文件复制到远程服务器，如下所示：

- 要通过交互窗口远程处理文件，必须先在解决方案资源管理器中右键单击这些文件（或项目），然后选择“寻源所选文件”进行手动复制  。 对于单独的文件，在服务器上将其复制到工作目录；在复制项目时，RTVS 会为项目创建文件夹。

- 还可以在解决方案资源管理器中选择文件进行复制，然后选择“寻源所选文”  。 此操作会将这些文件加载到交互窗口并在其中运行。 如果会话连接到远程计算机，则首先在那里复制文件。

- RTVS 绑定到远程工作区时，如果按 F5、选择“调试” > “启动调试”或按其他方式开始运行代码，则 RTVS 默认将项目文件自动复制到远程工作区（要了解如何控制此行为，请参阅下文）。

- 服务器上任何现有的文件都会被覆盖。

> [!Note]
> 由于 RTVS 无法可靠地截获所有 R 函数调用，因此在交互窗口中调用 `source()` 或 `runApp()`（适用于 Shiny 应用程序）等函数时，不会向远程工作区复制文件  。

[项目属性](r-projects-in-visual-studio.md#project-properties)决定 RTVS 是否在项目运行时复制文件以及究竟复制哪些文件。 要打开此页，请选择“项目” > “(名称)属性”菜单命令，或在解决方案资源管理器中右键单击项目并选择“属性”。

![包含文件传输设置的项目属性运行选项卡](media/workspaces-remote-file-transfer-filter-settings.png)

在此处，“运行时传输文件”属性决定 RTVS 是否自动复制项目文件  。 然后，“要传输的文件”  值将准确筛选出传输的文件。 默认仅复制 .R、.Rmd、.sql、.md 和 .cpp 文件      。 此行为可避免在每次运行时不慎将大型数据文件复制到服务器。

## <a name="copy-files-from-a-remote-workspace"></a>从远程工作区复制文件

如果 R 脚本在服务器中生成了文件，可使用 `rtvs::fetch_file` 函数将它们复制回客户端。 此函数至少会接受要复制到计算机的文件的远程路径，并选择性接受计算机上的目标路径。 如果不指定路径，则文件将复制到 %userprofile%\Downloads 文件夹  。
