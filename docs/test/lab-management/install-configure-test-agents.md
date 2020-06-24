---
title: 安装测试代理和测试控制器
ms.date: 04/17/2019
ms.topic: how-to
helpviewer_keywords:
- configure test agents, test lab
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 3c374951b4d4875e4e754035ac52afb7f8fc5a2e
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/23/2020
ms.locfileid: "85286890"
---
# <a name="install-test-agents-and-test-controllers"></a>安装测试代理和测试控制器

对于使用 Visual Studio 和 Azure Test Plans 或 Team Foundation Server (TFS) 的测试方案，无需测试控制器。 Visual Studio 的代理通过与 Azure Test Plans 或 TFS 通信来处理业务流程。 一种情况可能是你在 Azure Test Plans 或 TFS 中运行用于生成和发布工作流的连续测试。

还可考虑[改为使用 Build Management 或 Release Management ](use-build-or-rm-instead-of-lab-management.md)来替代实验室管理是否会更好。

## <a name="system-requirements"></a>系统要求

下表显示了为 Visual Studio 安装测试代理或测试控制器的系统要求：

| 项 | 要求 |
| ---- | ------------ |
| **代理** | Windows 10<br />Windows 8、Windows 8.1<br />Windows 7 Service Pack 1<br />Windows Server 2016 Standard 和 Datacenter<br />Windows Server 2012 R2 |
| **控制器** | Windows 10<br />Windows 8、Windows 8.1<br />Windows 7 Service Pack 1<br />Windows Server 2016 Standard 和 Datacenter<br />Windows Server 2012 R2 |
| **.NET Framework** | .NET Framework 4.5 |

## <a name="install-the-test-controller-and-test-agents"></a>安装测试控制器和测试代理

可从 [visualstudio.microsoft.com](https://visualstudio.microsoft.com/downloads/?q=agents) 中下载 Visual Studio 的代理。 查找 Visual Studio 2019 的代理，选择“代理”或“控制器”，然后选择“下载”     。 运行已下载的可执行文件，以安装测试代理或控制器。

可以从[早期版本下载](https://visualstudio.microsoft.com/vs/older-downloads/)页中下载 Visual Studio 2017、Visual Studio 2015 和 Visual Studio 2013 的代理。

这些安装程序可用作 ISO 文件，便于在虚拟机上安装。

::: moniker range="vs-2017"
## <a name="compatible-versions-of-tfs-microsoft-test-manager-the-test-controller-and-test-agent"></a>TFS、Microsoft 测试管理器、测试控制器和测试代理的兼容版本

可以根据下表混合使用不同版本的 TFS、Microsoft 测试管理器、测试控制器和测试代理：

| TFS | 带实验中心的 Microsoft 测试管理器 | 控制器 | 代理 |
| --- | -------------------------------------- | ---------- | ----- |
| 2017：从 2015 升级或全新安装 | 2017 | 2017 | 2017 |
| 2017：从 2015 升级或全新安装 | 2017 | 2013 Update 5 | 2013 Update 5 |
| 2017：从 2015 升级或全新安装 | 2015 | 2013 Update 5 | 2013 Update 5 |
| 2015：从 2013 升级 | 2013 | 2013 |2013 |
| 2015：全新安装 | 2013 | 2013 | 2013 |
| 2015：从 2013 升级或全新安装 | 2015 | 2013 | 2013 |
| 2013 | 2015 | 2013 | 2013 |
::: moniker-end

::: moniker range=">=vs-2019"
## <a name="compatible-versions-of-tfs-the-test-controller-and-test-agent"></a>TFS、测试控制器和测试代理的兼容版本

可以根据下表混合使用不同版本的 TFS、测试控制器和测试代理：

| TFS | 控制器 | 代理 |
| --- | -------------------------------------- | ---------- | ----- |
| 2017：从 2015 升级或全新安装 | 2017 | 2017 |
| 2017：从 2015 升级或全新安装 | 2013 Update 5 | 2013 Update 5 |
| 2017：从 2015 升级或全新安装 | 2013 Update 5 | 2013 Update 5 |
| 2015：从 2013 升级 | 2013 |2013 |
| 2015：全新安装 | 2013 | 2013 |
| 2015：从 2013 升级或全新安装 | 2013 | 2013 |
| 2013 | 2013 | 2013 |
::: moniker-end

> [!NOTE]
> TFS 2018 和 Azure DevOps Services 中的实验室管理方案已弃用。 有关详细信息，请参阅 [TFS 2018 发行说明](/visualstudio/releasenotes/tfs2018-relnotes#--removing-support-for-lab-center-and-automated-testing-flows-in-microsoft-test-manager)。

## <a name="upgrade-from-visual-studio-2013-test-agents"></a>从 Visual Studio 2013 测试代理升级

建议在所有新的自动测试方案中都使用 Visual Studio 的代理。 可以在生成管道中使用“部署测试代理”  任务在计算机上下载和安装测试代理。

下表显示了 Agents for Visual Studio 2013 支持的方案，以及 Team Foundation Server (TFS) 2015 和 Azure Test Plans 的替代方案：

| Agents for Visual Studio 2013 支持的方案 | TFS 和 Azure Test Plans 中的替代方案 |
| - | - |
| Visual Studio 中的“生成-部署-测试工”作流 | 用户可以在 TFS 中使用[生成管道](/azure/devops/pipelines/index?view=vsts)（而不是 XAML 生成）生成、部署和测试方案。 |
| 使用本地远程计算机进行负载测试（性能测试） | 使用 Test Controller 和 Test Agents 2013 Update 5 在本地运行负载测试。 |
| 使用实验室环境从 Microsoft 测试管理器（在 Visual Studio 2017 中已弃用）远程执行自动测试 | 目前此方案没有替代方案。 建议在生成和发布定义（而不是 XAML 生成）中使用“运行功能测试”任务来远程执行测试。 |
| 开发人员在 Visual Studio 中执行远程测试 | 不再支持。 |
