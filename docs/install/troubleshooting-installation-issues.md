---
title: 安装或升级问题疑难解答
description: 有时也会遇到问题。 如果 Visual Studio 安装或升级失败，可在此页寻求帮助。
ms.date: 09/13/2019
ms.custom: seodec18
ms.topic: troubleshooting
helpviewer_keywords:
- '{{PLACEHOLDER}}'
- '{{PLACEHOLDER}}'
ms.assetid: 556EDD3F-E365-43EE-B3DD-03AA4353F75B
author: ornellaalt
ms.author: ornella
manager: jillfra
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: 9dfdf504378dafd7d71288cae1927dd8d6bb9e56
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "76114994"
---
# <a name="troubleshoot-visual-studio-installation-and-upgrade-issues"></a>Visual Studio 安装和升级问题疑难解答

> [!IMPORTANT]
> 安装时遇到问题？ 我们可以为你提供帮助。 我们提供[**实时聊天**](https://visualstudio.microsoft.com/vs/support/#talktous)（仅英语）支持选项。

本疑难解答指南包含可解决大多数安装问题的分步说明。

## <a name="online-installations"></a>联机安装

以下步骤针对典型的联机安装进行了优化。 有关影响脱机安装的问题，请参阅[如何解决脱机安装问题](#offline-installations)。

### <a name="step-1---check-whether-this-problem-is-a-known-issue"></a>第 1 步 - 检查此问题是否是已知问题

::: moniker range="vs-2017"

Visual Studio 安装程序存在一些已知问题，Microsoft 正在努力修复中。 若要确定你遇到的问题是否有解决办法，请参阅[发行说明的“已知问题”部分](/visualstudio/releasenotes/vs2017-relnotes#-known-issues)。

::: moniker-end

::: moniker range="vs-2019"

Visual Studio 安装程序存在一些已知问题，Microsoft 正在努力修复中。 若要确定你遇到的问题是否有解决办法，请参阅[发行说明的“已知问题”部分](/visualstudio/releases/2019/release-notes#-known-issues)。

::: moniker-end

### <a name="step-2---check-with-the-developer-community"></a>第 2 步 - 通过开发者社区获取帮助

在 [Visual Studio 开发人员社区](https://developercommunity.visualstudio.com/spaces/8/index.html)中搜索错误消息。 社区的其他成员可能已记录下你遇到的问题的解决方案。

### <a name="step-3---delete-the-visual-studio-installer-directory-to-fix-upgrade-problems"></a>第 3 步 - 删除 Visual Studio 安装程序目录以修复升级问题

Visual Studio 安装程序引导程序是最轻型的可执行文件，用于安装 Visual Studio 安装程序的剩余部分。 删除 Visual Studio 安装程序文件，然后重新运行引导程序，可能会修复一些更新故障。

> [!NOTE]
> 执行以下操作将重新安装 Visual Studio 安装程序文件并重置安装元数据。

::: moniker range="vs-2017"

1. 关闭 Visual Studio 安装程序。
2. 删除 Visual Studio 安装程序目录。 通常，该目录是 `C:\Program Files (x86)\Microsoft Visual Studio\Installer`。
3. 运行 Visual Studio 安装程序引导程序。 引导程序位于“下载”文件夹中，文件名格式为 `vs_[Visual Studio edition]__*.exe`。 如果找不到此应用程序，可以转到 [Visual Studio 下载](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download)页，然后单击你的 Visual Studio 版本所对应的“下载”  ，便可下载引导程序。 然后，运行此可执行文件，重置安装元数据。
4. 尝试重新安装或更新 Visual Studio。 如果安装程序仍无法安装，请转到下一步。

::: moniker-end

::: moniker range="vs-2019"

1. 关闭 Visual Studio 安装程序。
2. 删除 Visual Studio 安装程序目录。 通常，该目录是 `C:\Program Files (x86)\Microsoft Visual Studio\Installer`。
3. 运行 Visual Studio 安装程序引导程序。 引导程序位于“下载”文件夹中，文件名格式为 `vs_[Visual Studio edition]__*.exe`。 如果找不到此应用程序，可以转到 [Visual Studio 下载](https://visualstudio.microsoft.com/downloads)页，然后单击你的 Visual Studio 版本所对应的“下载”  ，便可下载引导程序。 然后，运行此可执行文件，重置安装元数据。
4. 尝试重新安装或更新 Visual Studio。 如果安装程序仍无法安装，请转到下一步。

::: moniker-end

### <a name="step-4---report-a-problem"></a>第 4 步 - 报告问题

在某些情况下（如出现与文件损坏相关的问题时），可能需要逐个调查每个问题。 为便于我们为你提供帮助，请执行以下操作：

::: moniker range="vs-2017"

1. 收集安装日志。 有关详细信息，请参阅[如何获取 Visual Studio 安装日志](#installation-logs)。
2. 打开 Visual Studio 安装程序，然后单击“报告问题”  ，打开 Visual Studio 反馈工具。
![可以使用 Tab 键定位到“提供反馈”按钮，从而打开反馈工具](media/report-a-problem.png)
3. 为问题报告命名一个标题，然后输入相关详细信息。 单击“下一步”  ，转到“附件”  部分，然后附加生成的日志文件（此文件通常位于 `%TEMP%\vslogs.zip`）。
4. 单击“下一步”  ，检查问题报告，然后单击“提交”  。

::: moniker-end

::: moniker range="vs-2019"

1. 收集安装日志。 有关详细信息，请参阅[如何获取 Visual Studio 安装日志](#installation-logs)。
2. 打开 Visual Studio 安装程序，然后单击“报告问题”  ，打开 Visual Studio 反馈工具。
![可以使用 Tab 键定位到“提供反馈”按钮，从而打开反馈工具](media/vs-2019/vs-installer-report-problem.png)
3. 为问题报告命名一个标题，然后输入相关详细信息。 单击“下一步”  ，转到“附件”  部分，然后附加生成的日志文件（此文件通常位于 `%TEMP%\vslogs.zip`）。
4. 单击“下一步”  ，检查问题报告，然后单击“提交”  。

::: moniker-end

### <a name="step-5---run-installcleanupexe-to-remove-installation-files"></a>第 5 步 - 运行 InstallCleanup.exe 以删除安装文件

作为最后一种方法，可以[删除 Visual Studio](remove-visual-studio.md) 以删除所有安装文件和产品信息。

1. 按照[删除 Visual Studio](remove-visual-studio.md) 中的说明执行。
2. 按照[第 3 步 - 删除 Visual Studio 安装程序目录以修复升级问题](#step-3---delete-the-visual-studio-installer-directory-to-fix-upgrade-problems)中的说明操作，重新运行引导程序。
3. 尝试重新安装或更新 Visual Studio。

### <a name="step-6---contact-us-optional"></a>第 6 步 - 与我们联系（可选）

如果上述步骤均未帮助你成功安装或升级 Visual Studio，请使用我们的[实时聊天  ](https://visualstudio.microsoft.com/vs/support/#talktous)支持选项（仅英语）与我们联系，以获取进一步的帮助。

## <a name="offline-installations"></a>脱机安装

下面的表格列出了创建[脱机安装](create-an-offline-installation-of-visual-studio.md)和通过本地布局进行安装时的已知问题和可能会对你有所帮助的解决办法。

| 问题       | 项                   | 解决方案 |
| ----------- | ---------------------- | -------- |
| 用户没有访问文件的权限。 | 权限 (ACL) | 请确保调整权限 (ACL)，以便他们在共享脱机安装前  先向其他用户授予“读取”权限。 |
| 无法安装新的工作负载、组件或语言。  | `--layout`  | 若要通过部分布局进行安装，并选择之前未在此部分布局中下载过的工作负载、组件或语言，请确保可连接到 Internet。 |

有关如何解决[网络安装](create-a-network-installation-of-visual-studio.md)问题的详细信息，请参阅[安装或使用 Visual Studio 时与网络相关错误的疑难解答](troubleshooting-network-related-errors-in-visual-studio.md)。

## <a name="installation-logs"></a>安装日志

若要排查大部分的安装问题，需要有安装日志。 使用 Visual Studio 安装程序中的[报告问题](../ide/how-to-report-a-problem-with-visual-studio.md)提交问题时，这些日志会自动添加到报告中。

如果联系 Microsoft 支持部门，可能需要使用 [Microsoft Visual Studio 和 .NET Framework 日志收集工具](https://www.microsoft.com/download/details.aspx?id=12493)来提供这些安装日志。 日志收集工具从 Visual Studio 安装的所有组件（包括 .NET Framework、Windows SDK 和 SQL Server）收集安装日志。 它还会收集计算机信息、Windows Installer 清单，以及 Visual Studio 安装程序、Windows Installer 和系统还原的 Windows 事件日志信息。

收集日志的具体步骤：

1. [下载工具](https://www.microsoft.com/download/details.aspx?id=12493)。
2. 打开管理命令提示符。
3. 从工具保存目录运行 `Collect.exe`。
4. 在 `vslogs.zip` 目录中查找生成的 `%TEMP%` 文件，例如，`C:\Users\YourName\AppData\Local\Temp\vslogs.zip`。

> [!NOTE]
> 工具必须在安装失败时使用的同一用户帐户下运行。 若要从其他用户帐户运行工具，请设置 `–user:<name>` 选项，以指定安装失败时使用的用户帐户。 有关其他选项和使用情况信息，请通过管理员命令提示符运行 `Collect.exe -?` 获取。

## <a name="live-help"></a>实时帮助

如果本疑难解答指南中列出的解决方案无法帮助你成功安装或升级 Visual Studio，请使用我们的[**实时聊天**](https://visualstudio.microsoft.com/vs/support/#talktous)支持选项（仅英语）以获取进一步的帮助。

## <a name="see-also"></a>另请参阅

* [删除 Visual Studio](remove-visual-studio.md)
* [在防火墙或代理服务器后面安装和使用 Visual Studio 和 Azure 服务](install-and-use-visual-studio-behind-a-firewall-or-proxy-server.md)
* [用于检测和管理 Visual Studio 实例的工具](tools-for-managing-visual-studio-instances.md)
* [Visual Studio 管理员指南](visual-studio-administrator-guide.md)
