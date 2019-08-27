---
title: 安装 R 工具
description: 如何在 Visual Studio 2017 和 Visual Studio 2015 中安装 R 工具，包括脱机安装。
ms.date: 01/24/2018
ms.topic: conceptual
author: kraigb
ms.author: kraigb
manager: jillfra
ms.workload:
- data-science
monikerRange: vs-2017
ms.openlocfilehash: 4b505b1a8669c0eff14e7afcdb88275cd1502f95
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62581233"
---
# <a name="how-to-install-r-tools-for-visual-studio"></a>如何安装针对 Visual Studio 的 R 工具

本文内容：

- [支持的 Visual Studio 版本](#supported-versions-of-visual-studio)
- [在 Visual Studio 2017 中安装 RTVS](#install-rtvs-in-visual-studio-2017)
- [在 Visual Studio 2015 中安装 RTVS](#install-rtvs-in-visual-studio-2015)
- [脱机安装](#offline-installation-of-visual-studio-and-rtvs)

> [!Note]
> 安装 R 工具后，可能需要配置 Visual Studio，以获得经过优化的数据科学家布局，如[选项](options-for-r-tools-in-visual-studio.md)一文中所述。

## <a name="supported-versions-of-visual-studio"></a>支持的 Visual Studio 版本

装有 [Visual Studio 2017](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download) 和 [Visual Studio 2015 Update 3（或更高版本）](http://go.microsoft.com/fwlink/?LinkId=691129)的社区版（免费）、专业版和企业版的 Windows 均支持针对 Visual Studio 的 R 工具 (RTVS)。

Visual Studio for Mac 目前尚不支持 RTVS。

如果只有 Visual Studio Test Professional 和 SQL Server Management Studio 等产品随附的 Visual Studio Shell，则不会安装 RTVS。 Visual Studio Shell 缺少 RTVS 的必需组件。

## <a name="install-rtvs-in-visual-studio-2017"></a>在 Visual Studio 2017 中安装 RTVS

1. 运行 Visual Studio 安装程序并选择“修改”选项（有关详细信息，请参阅[修改 Visual Studio](../install/modify-visual-studio.md)）。 如果还没有安装 Visual Studio，请参阅[安装 Visual Studio](../install/install-visual-studio.md)。 在 Windows 7 上，请确保安装程序已更新，显示 Visual Studio 2017 版本 15.2 内部版本 26430.12 或更高版本。

1. 选择“数据科学和分析应用程序”工作负载：

    ![VS 2017 中的数据科学和分析应用程序工作负载](media/installation-data-science-workload.png)

1. 在同一工作负载名称下的右侧设置任何其他选项。 此工作负载默认包含 F# 和 Python 支持。 对于 R，最低要求是“R 语言支持”、“R 开发运行时支持”以及“Microsoft R Client”。

RTVS 的安装位置：%ProgramFiles(x86)%\Microsoft Visual Studio\<version>\<edition>Common7\IDE\Extensions\Microsoft\R Tools for Visual Studio，其中 \<version> 通常为 `2017`，\<edition> 为 `Community`、`Professional` 或 `Enterprise`。

## <a name="install-rtvs-in-visual-studio-2015"></a>在 Visual Studio 2015 中安装 RTVS

安装 Visual Studio 2015 后，需要单独安装 R 解释器和 R 工具。

### <a name="install-an-r-interpreter"></a>安装 R 解释器

RTVS 需要从以下一个或多个来源安装 64 位的 R 3.2.1 或更高版本：

- [Microsoft R Open](https://mran.microsoft.com/download/)
- [Microsoft R Client](/machine-learning-server/r-client/what-is-microsoft-r-client)
- [CRAN R](https://cran.r-project.org/bin/windows/base/)

Microsoft R Open 和 CRAN R 均允许多个并行版本。 但是，Microsoft R Client 只支持一个版本，并始终使用安装的最新版本。

### <a name="install-the-r-tools"></a>安装 R 工具

从 [https://aka.ms/rtvs-current](https://aka.ms/rtvs-current) 下载适用于 Visual Studio 2015 的最新 RTVS。 如果尚未安装，RTVS 会检查是否有适合的 Visual Studio 版本，并帮助安装 R 解释器。

> [!Note]
> 独立 RTVS 安装程序仅适用于 Visual Studio 2015；在 Visual Studio 2017 中，可通过[数据科学和分析应用程序工作负载](#install-rtvs-in-visual-studio-2017)安装 R 支持（如前面所述）。

RTVS for Visual Studio 2015 安装在以下位置：`%ProgramFiles(x86)%\Microsoft Visual Studio 14\Common7\IDE\Extensions\Microsoft\R Tools for Visual Studio`

## <a name="offline-installation-of-visual-studio-and-rtvs"></a>Visual Studio 和 RTVS 的脱机安装

脱机安装适用于未连接到 Internet 的计算机：

1. 转到[创建 Visual Studio 2017 的脱机安装](../install/create-an-offline-installation-of-visual-studio.md)。

1. 如果使用 Visual Studio 2015，请在目录上方的选择器中选择“2015”。

1. 请遵循在网页中创建脱机安装的说明。

1. 对于 Visual Studio 2015，从 [https://aka.ms/rtvs-current-zip](https://aka.ms/rtvs-current-zip) 和 [https://aka.ms/rtvs-remote-zip](https://aka.ms/rtvs-remote-zip) 下载脱机 RTVS 安装程序。

1. 从脱机安装程序安装 Visual Studio 和 RTVS。

## <a name="see-also"></a>请参阅

- [R 入门](getting-started-with-r.md)
- [R 工具示例项目](getting-started-samples.md)
- [R 工具中的帮助](getting-started-help.md)
- [R 工具选项](options-for-r-tools-in-visual-studio.md)
- [Microsoft Machine Learning Server（以前称为 R Server）](/machine-learning-server/)