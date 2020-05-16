---
title: 创建 Web 性能和负载测试项目
ms.date: 03/14/2018
ms.topic: quickstart
helpviewer_keywords:
- load testing, quickstart
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 4f186e8c10d894b98e789480046d43fc957edd8a
ms.sourcegitcommit: 2975d722a6d6e45f7887b05e9b526e91cffb0bcf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/20/2020
ms.locfileid: "75566405"
---
# <a name="quickstart-create-a-load-test-project"></a>快速入门：创建负载测试项目

在此 10 分钟的快速入门教程中，将学习如何在 Visual Studio 中创建和运行 Web 性能和负载测试项目。 负载测试执行 Web 性能或单元测试，以模拟同时访问服务器的多个用户。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## <a name="software-requirements"></a>软件要求

Web 性能和负载测试项目仅在 Visual Studio Enterprise Edition 中可用  。

## <a name="install-the-load-testing-component"></a>安装负载测试组件

如果尚未安装 Web 性能和负载测试工具组件，则需通过 Visual Studio 安装程序进行安装。

1. 从 Windows 的“开始”菜单打开“Visual Studio 安装程序”   。 在 Visual Studio 中，也可从“新建项目”对话框访问它，或从菜单栏中选择“工具” > “获取工具和功能”访问   。

1. 在“Visual Studio 安装程序”中，选择“单个组件”选项卡，然后向下滚动到“调试和测试”部分    。 选择“Web 性能和负载测试工具”  。

   ![Web 性能和负载测试工具组件](media/web-perf-load-testing-tools-component.png)

1. 选择“修改”按钮  。

   已安装 Web 性能和负载测试工具组件。

## <a name="create-a-load-test-project"></a>创建负载测试项目

本节将创建一个 C# 负载测试项目。 如果愿意，还可创建 Visual Basic 负载测试项目。

::: moniker range="vs-2017"

1. 打开 Visual Studio。

2. 从菜单栏中依次选择“文件”  >“新建”  >“项目”  。

   **“新建项目”** 对话框随即打开。

3. 在“新建项目”对话框中，依次展开“已安装”、“Visual C#”，然后选择“测试”类别     。 选择“Web 性能和负载测试项目”模板  。

   ![Web 性能和负载测试项目模板](media/web-perf-load-test-project-template.png)

4. 如果不想使用默认名称，请输入项目名，然后选择“确定”  。

::: moniker-end

::: moniker range=">=vs-2019"

1. 打开 Visual Studio。

2. 在“开始”窗口上，选择“创建新项目”  。

3. 在“创建新项目”页中，在搜索框中键入“web test”，然后选择适用于 C# 的“Web 性能和负载测试项目\[已弃用]”模板    。 选择“下一步”  。

4. 如果不想使用默认名称，请输入项目名，然后选择“创建”  。

::: moniker-end

   Visual Studio 将创建项目并在“解决方案资源管理器”  中显示文件。 该项目最初包含一个名为 WebTest1.webtest 的 Web 测试文件  。

## <a name="add-a-load-test-to-the-project"></a>向项目添加一个负载测试

1. 在“解决方案资源管理器”中的项目节点的右键菜单或弹出菜单中，依次选择“添加” > “负载测试”    。

   此时将打开“新建负载测试向导”  。

1. 选择“本地负载测试”选项，然后选择“下一步”   。 可在[此处](/azure/devops/test/load-test/get-started-simple-cloud-load-test?view=vsts)了解有关基于云的负载测试的详细信息。

   ![“新建负载测试向导” - 第一页](media/load-test-wizard-page-1.png)

1. 选择“下一步”以逐步完成向导，直至到达“将测试添加到负载测试方案并编辑测试组合”页   。 选择 **“添加”** 按钮。

   随即打开“添加测试”对话框  。

1. 在“可用测试”下，选择“WebTest1”，然后选择向右键将其移动到“选定的测试”框中    。 选择 **“确定”** 按钮。

   ![“添加测试”对话框](media/add-tests-dialog-box.png)

1. 返回“新建负载测试向导”，选择“完成”按钮   。

   负载测试随即被添加到项目中，并在编辑器窗口中打开负载测试文件。

## <a name="run-the-load-test"></a>运行负载测试

我们已经创建了一个不太有用的负载测试，但我们还是运行它吧。

从在编辑器中打开的负载测试的右键菜单或弹出菜单中，选择“运行负载测试”  。

![“运行负载测试”菜单](media/run-load-test.png)

负载测试开始运行。 “测试结果”窗口显示正在运行测试，并且负载测试分析器显示在编辑器窗口中  。 测试完成后（如果接受默认值，则应为五分钟），编辑器中会显示摘要。 可选择“关系图”、“表”或“详细信息”以获取有关负载测试结果的不同信息    。

![负载测试分析器窗口](media/load-test-analyzer.png)

## <a name="next-steps"></a>后续步骤

现在已创建了一个简单的负载测试项目，下一步是配置方案、计数器集和运行设置。

> [!div class="nextstepaction"]
> [编辑测试设置](edit-load-tests.md)
