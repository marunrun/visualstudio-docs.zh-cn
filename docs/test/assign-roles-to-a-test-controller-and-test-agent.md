---
title: 使用测试控制器和测试代理角色进行自动测试
ms.date: 10/20/2016
ms.topic: conceptual
helpviewer_keywords:
- testing, walkthroughs, test controller and test agents
- test agent, walkthrough
- walkthroughs [Visual Studio ALM] testing
- test controller, walkthrough
- walkthroughs, test controller and test agents
ms.assetid: 57ed43ae-4e67-4139-8aec-3e9fceb0a745
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: dc7936041746872fdf30ce3159506d93c378376d
ms.sourcegitcommit: 5b34052a1c7d86179d7898ed532babb2d9dad4a3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/15/2019
ms.locfileid: "69490605"
---
# <a name="assign-roles-to-a-test-controller-and-test-agent"></a>为测试控制器和测试代理分配角色

本演练演示如何创建和配置使用测试控制器和测试代理跨多台使用 Visual Studio 的计算机分发测试的测试设置。 本演练还演示如何将诊断和数据适配器添加到测试设置中。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## <a name="prerequisites"></a>系统必备

- 创建要使用测试设置运行的单元测试或编码的 UI 测试。

- 安装测试控制器和测试代理。 有关如何安装测试控制器和测试代理的详细信息，请参阅[安装和配置测试代理](../test/lab-management/install-configure-test-agents.md)。

## <a name="to-create-and-configure-a-test-setting"></a>创建和配置测试设置

1. 在“解决方案资源管理器”中，右键单击“解决方案项”，指向“添加”，然后选择“新建项”     。

     “添加新项”  对话框随即出现。

2. 在“已安装的模板”窗格中，选择“测试设置”   。

3. 在“名称”框中，键入 TestSettingDistributedTestWalkthrough   。

4. 选择“添加”  。

     新的测试 TestSettingDistributedTestWalkthrough.testsettings 文件会显示在“解决方案资源管理器”中的“解决方案项”文件夹下    。

     此时会显示“测试设置”对话框  。 “常规”页处于选中状态  。

     你现在可以编辑并保存测试设置值。

5. 在“名称”下键入测试设置的名称  。

6. 在“说明”下，键入“分布式测试设置”   。

7. 保持“默认命名方案”处于选中状态  。

## <a name="to-assign-roles-to-a-test-controller-and-test-agents"></a>为测试控制器和测试代理分配角色

1. 选择“角色”  。

     “角色”页随即显示  。

2. 要远程运行测试，请使用“测试执行方法”下拉列表，然后选择“远程执行”   。

3. 在“控制器”下拉列表中，键入[你的测试控制器](../test/lab-management/install-configure-test-agents.md)的计算机名称  。

    > [!NOTE]
    > 如果这是首次添加控制器，则下拉列表中不会列出任何控制器。 列表由先前在其他测试设置中指定的控制器填充。

4. 在“角色”下，选择“添加”   。

5. 在突出显示行的“名称”列中，键入“分布式测试”   。

## <a name="to-assign-a-diagnostic-and-data-adapter-to-your-test-setting"></a>为测试设置分配诊断和数据适配器

1. 选择“数据和诊断”  。

     “数据和诊断”页随即显示  。

2. 在“角色”下，验证是否选中了“分布式测试”角色   。

3. 在“所选角色的数据和诊断”下，选择“IntelliTrace”和“系统信息”适配器    。

     有关可在测试设置中使用的这些适配器及其他适配器的信息，请参阅[配置单元测试](../test/configure-unit-tests-by-using-a-dot-runsettings-file.md)。

4. 选择“主机”  。

5. （可选）如果计算机是在 64 位版本的 Microsoft Windows 下运行，并且使用“任意 CPU”配置编译了测试，则请使用“在 32 位或 64 位进程中运行测试”下拉列表，并选择“在 64 位计算机上的 64 位进程中运行测试”    。

    > [!TIP]
    > 为了最大限度地提高灵活性，应使用“任何 CPU”  配置来编译测试项目。 然后，可以在 32 位和 64 位代理上运行。 使用“64 位”  配置编译测试项目毫无优势可言。

6. 要保存新的测试设置，请选择“应用”  。

7. 选择“关闭”  。

::: moniker range="vs-2017"

8. 在“测试”菜单上，选择“选择测试设置文件”，然后选择“TestSettingDistributedTestWalkthrough.testsettings”   。

::: moniker-end

::: moniker range=">=vs-2019"

8. 在“测试资源管理器”中，选择“设置”按钮上的箭头，然后选择“选择设置文件”    。 浏览到“TestSettingDistributedTestWalkthrough.testsettings”文件并选择它  。

::: moniker-end

9. 按常规方式运行测试。

     当测试控制器处理单元测试和编码的 UI 测试时，测试控制器将这些测试每 100 个分成一组，并将这些组发送给测试代理计算机。 例如，如果有 250 个单元测试和 3 个测试代理，则前 100 个单元测试会发送给 agent1，接下来的 100 个单元测试发送给 agent2，余下的 50 个单元测试发送给 agent3。

## <a name="see-also"></a>请参阅

- [安装和配置测试代理](../test/lab-management/install-configure-test-agents.md)