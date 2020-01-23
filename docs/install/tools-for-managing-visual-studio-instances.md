---
title: 用于检测和管理 Visual Studio 实例的工具
titleSuffix: ''
description: 了解可用于在客户端计算机上检测和管理 Visual Studio 安装的工具。
ms.date: 08/14/2017
ms.custom: seodec18
ms.topic: conceptual
helpviewer_keywords:
- '{{PLACEHOLDER}}'
- '{{PLACEHOLDER}}'
ms.assetid: 85686707-14C0-4860-9B7A-66485D43D241
author: ornellaalt
ms.author: ornella
manager: jillfra
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: d6e46c95584cb3732d6339a02f6098976f2bab85
ms.sourcegitcommit: f3f668ecaf11b4c2738ebc91923c6b5e38e74670
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/16/2020
ms.locfileid: "76115045"
---
# <a name="tools-for-detecting-and-managing-visual-studio-instances"></a>用于检测和管理 Visual Studio 实例的工具

有几种工具可用于在客户端计算机上检测和管理 Visual Studio 安装。

## <a name="detecting-existing-visual-studio-instances"></a>检测现有 Visual Studio 实例

我们提供了几种工具来帮助你检测和管理在客户端计算机上安装的 Visual Studio 实例：

* [vswhere](https://github.com/microsoft/vswhere)：一个可执行文件，内置于 Visual Studio 或可单独分发，可帮助查找特定计算机上所有 Visual Studio 实例的位置。
* [VSSetup.PowerShell](https://github.com/microsoft/vssetup.powershell)：使用安装程序配置 API 来标识已安装的 Visual Studio 实例的 PowerShell 脚本。
* [VS-Setup-Samples](https://github.com/microsoft/vs-setup-samples)：展示了如何使用安装程序配置 API 来查询现有安装的 C# 和 C++ 示例。

此外，[安装程序配置 API](<xref:Microsoft.VisualStudio.Setup.Configuration>) 提供了接口，方便开发者生成自己的实用工具来询问 Visual Studio 实例。

## <a name="using-vswhereexe"></a>使用 vswhere.exe

`vswhere.exe` 自动包含在 Visual Studio 中（从 Visual Studio 2017 15.2 及更高版本开始），也可以从 [vswhere 版本页面](https://github.com/Microsoft/vswhere/releases)下载它。 使用 `vswhere -?` 获取有关该工具的帮助信息。 作为示例，此命令显示了 Visual Studio 的所有版本（包括产品的早期版本和预发行版本），并输出 JSON 格式的结果：

```cmd
C:\Program Files (x86)\Microsoft Visual Studio\Installer> vswhere.exe -legacy -prerelease -format json
```

::: moniker range="vs-2017"

> [!TIP]
> 有关 Visual Studio 2017 安装的详细信息，请参阅 [Visual Studio 安装程序存档](https://devblogs.microsoft.com/setup/tag/vs2017/)。

::: moniker-end

## <a name="editing-the-registry-for-a-visual-studio-instance"></a>编辑 Visual Studio 实例的注册表

在 Visual Studio 中，注册表设置存储在专用位置中，这样可以在同一计算机上安装相同版本 Visual Studio 的多个并行实例。

由于这些条目并非存储在全局注册表中，因此需要遵循有关使用注册表编辑器更改注册表设置的特殊说明：

1. 如果有打开的 Visual Studio 实例，请将其关闭。

1. 启动 `regedit.exe`。

1. 选择“`HKEY_LOCAL_MACHINE`”节点。

1. 在 Regedit 主菜单中，依次选择“文件” > “加载配置单元...”，然后选择专用注册表文件（存储在“AppData\Local”文件夹中）    。 例如：

   ```
   %localappdata%\Microsoft\VisualStudio\<config>\privateregistry.bin
   ```

   > [!NOTE]
   > `<config>` 对应于要浏览的 Visual Studio 实例。

系统会提示你输入配置单元名称，这将成为你的独立配置单元的名称。 执行此操作后，应该能够在所创建的独立配置单元下浏览注册表。

> [!IMPORTANT]
> 必须先卸载已创建的独立配置单元，然后才能再次启动 Visual Studio。 为此，请在 Regedit 主菜单中，依次选择“文件” > “卸载配置单元”   。 （如果不这样做，文件会一直处于锁定状态，且 Visual Studio 无法启动。）

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>请参阅

* [Visual Studio 管理员指南](visual-studio-administrator-guide.md)
