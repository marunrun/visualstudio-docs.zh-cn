---
title: Visual Studio 2017 中 Live Unit Testing 的新增功能
titleSuffix: ''
ms.date: 10/11/2017
ms.topic: conceptual
helpviewer_keywords:
- Live Unit Testing
- Live Unit Testing What's New
author: mikejo5000
ms.author: mikejo
ms.workload:
- dotnet
monikerRange: vs-2017
ms.openlocfilehash: 7f7ab0c257bfed4521e95d9da12eaa0b9e25a71e
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "76114269"
---
# <a name="whats-new-in-live-unit-testing-for-visual-studio-2017"></a>Visual Studio 2017 的 Live Unit Testing 的新增功能

本主题列出从 Visual Studio 2017 版本 15.3 开始，每个 Visual Studio 版本中的 Live Unit Testing 添加的新功能。 如需大致了解如何使用 Live Unit Testing，请参阅[使用 Visual Studio 执行 Live Unit Testing](live-unit-testing.md)。

## <a name="version-154"></a>版本 15.4

从 Visual Studio 2017 版本 15.4 开始，Live Unit Testing 包含以下领域的改进和增强功能：

- **改进的可发现性**。 对于不知道 Live Unit Testing 功能存在的用户，只要用户打开包含单元测试但未启用 Live Unit Testing 的解决方案，Visual Studio IDE 就显示一个提及 Live Unit Testing 的黄色条框。 用户可借助黄色条框中提供的信息详细了解 Live Unit Testing 并启用该功能。 如果未满足 Live Unit Testing 的先决条件，也会显示金色条框。 其中包括：

  - 缺少测试适配器。
  - 存在较旧版本的测试适配器。
  - 需要提供解决方案引用的 NuGet 包的还原文件。

- **与任务中心通知集成**。 Visual Studio IDE 现在在任务中心显示 Live Unit Testing 后台处理通知，以便用户可以轻松地了解启用 Live Unit Testing 后发生的情况。 这解决了在大型解决方案中启动 Live Unit Testing 的关键问题。 之前，在覆盖率图标显示前的数分钟，用户无法确定 Live Unit Testing 是否实际已被启用以及它是否在正常运行。 现在不会这样了！

- **MSTest 框架版本 1 支持**：Live Unit Testing 已经可与三个常用单元测试框架配合使用：xUnit、NUnit 以及 MSTest。 之前，Live Unit Testing 仅在 MSTest 单元测试项目使用 MS Test 版本 2 时有效。 从 Visual Studio 2017 版本 15.4 开始，它现在还支持 MSTest 版本 1。

- **可靠性和性能**：Live Unit Testing 现在可确保系统能够更好地检测出项目尚未完全完成加载的情况，并可避免 Live Unit Testing 出现崩溃。 生成性能改进还可在系统知道项目文件未进行任何更改时避免重新计算 MSBuild 项目。

- **其他用户界面优化**：右键单击手势中令人费解的“实时测试集 - 包括/排除”  选项已更名为“Live Unit Testing 包括/排除”  。 “测试” **“Live Unit Testing”菜单的“重置清理”选项已被删除**   >   。 现可通过依次选择“工具” **“选项”** “Live Unit Testing”，然后选择“删除持久化数据”访问该选项 >    >    。

## <a name="version-153"></a>版本 15.3

从 Visual Studio 2017 版本 15.3 开始，Live Unit Testing 在两大领域推出了改进和增强功能：

- .NET Core 和 .NET Standard 支持。 可在使用 C# 或 Visual Basic 编写的 .NET Core 和 .NET Standard 解决方案中使用 Live Unit Testing。

- 性能得到了改进。 可以发现，在“Live Unit Testing”下首次完整生成并运行测试后，性能大大提升。 同时还会发现，对于同一解决方案，在后续启动 Live Unit Testing 时的性能也有显著提升。 我们现在可以保留 Live Unit Testing 生成的数据，并在检查结果是最新的情况下尽可能重用这些数据。

除这些主要解决方案外，Live Unit Testing 还包括以下增强功能：

- 当前使用了全新的烧杯图标来区分测试方法和常规方法。 空烧杯图标表示 Live Unit Testing 中没有特定测试。

- 从 Live Unit Testing 覆盖图标的弹出 UI 窗口单击测试方法时，可通过 UI 窗口中的上下文直接调试测试，而无需离开代码编辑器。 这在查看未通过测试时特别有用。

- “工具/选项/Live Unit Testing/常规”中额外添加了一些可配置的选项。 可设置用于 Live Unit Testing 的内存上限。 还可以为未结解决方案指定 Live Unit Testing 永久性数据的文件路径。

- “测试/Live Unit Testing”的菜单栏下额外添加了一些菜单项。 “重置清理”  可以删除永久性数据，并能重新生成这些数据。 “选项”  跳转到“工具/选项/Live Unit Testing/常规”。

- 现在可以使用以下属性，在源代码中指定要从 Live Unit Testing 中排除的目标测试方法：

  - 对于 xUnit：`[Trait("Category", "SkipWhenLiveUnitTesting")]`
  - 对于 NUnit：`[Category("SkipWhenLiveUnitTesting")]`
  - 对于 MSTest：`[TestCategory("SkipWhenLiveUnitTesting")]`

## <a name="see-also"></a>另请参阅

- [Live Unit Testing 简介](live-unit-testing-intro.md)
- [使用 Visual Studio 进行实时单元测试](live-unit-testing.md)
