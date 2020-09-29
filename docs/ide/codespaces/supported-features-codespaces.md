---
title: 受支持的 Visual Studio 功能（预览）
description: 了解使用 GitHub Codespaces 时可用的 Visual Studio IDE 功能。
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
ms.openlocfilehash: c86fc99fe6bd2ae17b6ce222b04549db07d7687e
ms.sourcegitcommit: 062615c058d2ff44751e8d0c704ccfa3c5543469
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/22/2020
ms.locfileid: "90862325"
---
# <a name="supported-visual-studio-features-preview"></a>受支持的 Visual Studio 功能（预览）

连接到 codespace 后，Visual Studio 可提供丰富的开发体验。 你可以使用熟悉的 Visual Studio 内部循环工具，来编辑、调试、测试和版本化源代码，还可以使用诸如项目模板、丰富的代码导航和 IntelliSense 之类的生产力功能。

在当前的 GitHub Codespaces [public beta 版本](https://github.com/features/codespaces)中，某些 Visual Studio 功能可能并不完全支持，或在最初可能有缺失。 以下各节概述了 Visual Studio 和 GitHub Codespaces beta 版本中值得期待的内容，以及将来可以展望的内容。 

这并不是一个详尽的列表，只是介绍了 Visual Studio 在连接到 codespace 时的一般功能。

> [!NOTE]
> 如果在 Visual Studio 中使用 codespace 时缺少某个功能，请在 https://developercommunity.visualstudio.com/ 上创建问题，告知我们。 这有助于我们优先考虑最需要的功能。

> [!NOTE]
> 下述功能适用于 Visual Studio，而不适用于其他两个 GitHub Codespaces 客户端：Visual Studio Code 和浏览器内部编辑器。

## <a name="edit-and-navigation"></a>编辑和导航

你应注意到，在 codespace 中编辑源代码的方式与获取智能语言功能（如 IntelliSense、代码导航、诊断和建议）的方式几乎没有什么区别。

* IntelliSense*
* 代码导航*
* 通过格式化文档进行代码格式化
* 语法突出显示
* 快速信息*
* HTML、CSS、Razor 编辑器* - 部分支持。
* JavaScript 编辑器* - 部分支持。

以下内容尚不可用：

* IntelliSense* - 某些自动完成/成员列表筛选器不可用。 监视窗口中未导入类型和 IntelliSense 的补全尚不可用。
* 代码导航* - 支持大多数命令，但尚不支持路径说明中的“转到基本”和“在文件中查找”。
* 快速信息* - 不支持快速信息中的着色。
* HTML、CSS、Razor 编辑器* - 诊断、Intellisense 补全、快速信息、智能缩进。 当前不支持语义着色、导航命令等。
* JavaScript 编辑器* - 尚不支持脚本块（例如 HTML 和 CSHTML 文件中的 JavaScript 内容）和语义突出显示。 带有灯泡特征和 Lint 分析的已知问题。
* CMake 目标视图
* CMake 项目设置编辑器
* Ctrl+F7（编译文件）
* CodeLens
* 代码片段
* IntelliCode

## <a name="application-types-and-configuration"></a>应用程序类型和配置

支持大多数应用程序类型和项目配置，但是你需要不借助可视化设计器直接编辑项目代码。 有关更多配置指南，请参阅[如何自定义 codespace](customize-codespaces.md)。

* 项目和项模板
* .NET Core 和 ASP.NET Core 项目
* C++ 控制台应用 - 支持 CMake 和 vcxproj
* 面向 Linux 的 C++ 应用 - 大部分都支持非 GUI。 能够安装和预配 WSL、特定于平台的 Intellisense 和内部版本。
* 项目文件编辑 - 大部分都支持。 缺少某些补全、语法突出显示和高级编辑功能。
* GitHub 帐户 - 可用于创建和连接到 Codespaces，并访问 GitHub 上该帐户可用的资源。
* Azure CLI - 不共享已登录的 Visual Studio 标识或密钥链帐户。 不支持基于浏览器的登录，但可以使用 `az login --use-device-code` 在集成终端内进行身份验证。

以下内容尚不可用：

* UI 设计器 - WinForms 和 WPF 设计器
* Visual Basic 和 F# 项目
* 目标是 .NET Framework 的项目
* Docker Compose 项目
* 项目属性页
* ASP.NET Core 模板中的身份验证选项
* 需要安装 GUI 的应用 - 支持可以在终端上安装的所有程序（包括 chocolatey 安装程序），但实际的 GUI 不会立即可用。 当前的缓解措施是启用全屏 Live Share 以访问 GUI。 管理控制台不可访问。 不支持需要重启才能安装的应用。
* Visual Studio 中 Azure 资源的托管标识
* Intranet 资源（专用网络）- 目前，codespace 无法连接到需要 VPN 的任何资源。
* 扩展 - 将 Codespaces 用于 Visual Studio 时，不支持任何扩展。

## <a name="debugging"></a>调试

支持必要的内部循环调试，包括设置断点、基本单步执行代码、检查变量以及局部变量、自动和监视窗口。 不支持某些其他窗口、自定义项和可视化工具。

* 断点*
* 基本单步执行
* 局部变量、自动、监视窗口* - 部分支持。
* 部分支持符号服务器、源服务器以及导入/导出数据提示。

以下内容尚不可用：

* 断点* - “反汇编”窗口中的“断点标签”、“数据断点”和“设置断点”正在开发中。 部分支持导入和导出断点。
* 局部变量、自动、监视窗口* - 一些功能，例如搜索框中的语句完成和搜索框导航。
* UI 自定义 - 不支持可固定属性和隐藏模板参数。
* 可视化工具 - 部分支持 C++ natvis。 不支持“反汇编”窗口、XAML 视觉诊断、自定义 .NET 可视化工具和数据集可视化工具。
* 其他调试器窗口 - 部分支持“进程”窗口。 “并行堆栈”窗口 - 不支持“任务视图”、“诊断中心”和“查找源/符号”对话框。
* 某些调试器工作流 - 不支持“附加到进程”、实时 (JIT) 调试器、转储调试、分析和 IntelliTrace。 部分支持 C++“仅我的代码”单步执行。
* 编辑并继续 - 不支持托管代码和本机代码。
* 线程功能 - 不支持“冻结/解冻”线程、“重命名”线程和“在源中显示线程”。
* 其他单步执行功能 - 不支持“自动单步跳过”属性和运算符 (.NET Core) 和“单步执行特定项”。 

## <a name="features"></a>功能

使用连接到 codespace 的 Visual Studio 时，可以获取与在本地使用时相同的辅助功能。

* 源代码管理 - 通过新的 [Git 窗口](https://devblogs.microsoft.com/visualstudio/improved-git-experience-in-visual-studio-2019/)完全支持 Git。
* 辅助功能 - 辅助技术存在一个已知问题，即无法访问已调试应用的应用广播。 除此限制外，我们认为本地 Visual Studio 体验中还会存在其他兼容性问题。 如果你发现了 bug，请在[开发者社区](https://developercommunity.visualstudio.com/)上提交问题以告知我们。
* 发布 - 支持通过 GitHub 操作发布到 Azure。
* 连接服务 - 部分支持应用见解、KeyVault、存储、SQL、Redis、Cosmos、openAPI 和 gRPC。
* 测试资源管理器* - 大部分都支持。

以下内容尚不可用：

* 测试资源管理器* - 诸如默认的体系结构选择、并行运行测试、播放列表等功能。调试单元测试、运行设置和一些其他企业功能的已知问题。 不支持分析单元测试。
* NuGet 包管理器 UI - 支持 NuGet 命令行。
* 企业测试功能 - 不支持 Live Unit Testing、Microsoft Fakes、代码覆盖率和 IntelliTest。
* 高级发布方案 - 选择性发布、FTP 发布、预览更改、快速发布工具栏等。

## <a name="see-also"></a>另请参阅

* [什么是 GitHub Codespaces？](codespaces-overview.md)
* [如何将 Visual Studio 用于 codespace](use-visual-studio-with-codespaces.md)
* [如何自定义 codespace](customize-codespaces.md)
