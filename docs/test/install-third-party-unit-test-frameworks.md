---
title: 安装第三方单元测试框架
ms.date: 04/01/2019
ms.topic: conceptual
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
author: gewarren
ms.openlocfilehash: 9f61b52f72474a8ecd8fac4c30265dcd7cf36a5e
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62978640"
---
# <a name="install-unit-test-frameworks"></a>安装单元测试框架

Visual Studio 测试资源管理器可从任何针对该资源管理器开发了适配器接口的单元测试框架中运行测试。 安装框架会复制二进制文件，并为支持的语言添加 Visual Studio 项目模板。 使用模板创建项目时，框架会向测试资源管理器注册。

Visual Studio 解决方案可以包含使用不同框架和面向不同语言的单元测试项目。

[MSTest](getting-started-with-unit-testing.md) 是 Visual Studio 提供的测试框架并默认安装。

## <a name="acquire-frameworks"></a>获取框架

使用“NuGet 包管理器”安装第三方单元测试框架。

1. 右键单击将包含测试代码的项目，然后选择“管理 NuGet 包”。

2. 在“NuGet 包管理器”中，搜索要安装的测试框架，然后单击“安装”。

   ![Visual Studio 中的 NuGet 包管理器](media/vs-2019/nuget-package-manager.png)

## <a name="update-to-the-latest-test-adapters"></a>更新到最新版本的测试适配器

更新到最新版本的稳定测试适配器，以体验更好的测试发现和执行。 有关更新到 MSTest、NUnit 和 xUnit 测试适配器的详细信息，请参阅 [Visual Studio 博客](https://devblogs.microsoft.com/visualstudio/test-experience-improvements/)。

### <a name="to-update-to-the-latest-stable-test-adapter-version"></a>更新到最新版本的稳定测试适配器

1. 导航到“工具” > “NuGet 包管理器” > “管理解决方案的 NuGet 包”，打开解决方案的 Nuget 包管理器。

2. 单击“更新”选项卡，并搜索已安装的 MSTest、NUnit 或 xUnit 测试适配器。

3. 选择每个测试适配器，然后选择下拉菜单中的最新稳定版本。

4. 选择“安装”按钮。

   ![升级测试适配器](media/install-adapter-upgrade.png)

## <a name="see-also"></a>请参阅

- [单元测试代码](../test/unit-test-your-code.md)
