---
title: 创建并运行 UWP 应用的单元测试
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- unit tests, creating
- unit tests
- unit tests, UWP apps
- unit tests, running
ms.author: gewarren
manager: jillfra
ms.workload:
- uwp
author: gewarren
ms.openlocfilehash: a123657e148e4c19c0fab1c1a9bf567ad2ea6fa8
ms.sourcegitcommit: 9a3972eb85de5443ac2bc03964c5a251c39b2921
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/26/2019
ms.locfileid: "71301712"
---
# <a name="walkthrough-create-and-run-unit-tests-for-uwp-apps"></a>演练：创建并运行 UWP 应用的单元测试

Visual Studio 支持对通用 Windows 平台 (UWP) 应用进行单元测试。 Visual Studio 提供 C#、Visual Basic 和 C++ 的单元测试项目模板。

> [!TIP]
> 有关开发 UWP 应用的详细信息，请参阅 [UWP 应用入门](/windows/uwp/get-started/)。

以下过程描述了为 UWP 应用创建、运行和调试单元测试的步骤。

## <a name="create-a-unit-test-project-for-a-uwp-app"></a>为 UWP 应用创建单元测试项目

::: moniker range=">=vs-2019"

1. 打开 Visual Studio。 在“开始”窗口上，选择“创建新项目”  。

2. 在“创建新项目”  搜索框中，输入“单元测试”  。

   模板列表将筛选出用于单元测试的模板。

3. 针对 C# 或 Visual Basic，选择“单元测试应用(通用 Windows)”  模板，然后选择“下一步”  。

   ![在 Visual Studio 中创建新的 UWP 单元测试应用](media/vs-2019/new-uwp-unit-test-app.png)

4. （可选）更改项目或解决方案的名称和位置，然后选择“创建”  。

5. （可选）更改目标和最低平台版本，然后选择“确定”  。

完成这些步骤后，将创建单元测试项目，并在解决方案资源管理器中显示该项目。

![解决方案资源管理器中的 UWP 单元测试项目](media/vs-2019/uwp-unit-test-project-solution-explorer.png)

::: moniker-end

::: moniker range="vs-2017"

1. 从 **“文件”** 菜单中选择 **“新建项目”** 。

   此时将显示“新建项目”对话框  。

2. 在“模板”之下，选择要用以创建单元测试的编程语言，然后选择关联的 Windows 通用单元测试库。 例如，选择“Visual C#”  ，选择“Windows 通用”  ，然后选择“单元测试库(通用 Windows)”  。

3. （可选）在“名称”  文本框中，输入要用于项目的名称。

4. （可选）通过在“位置”  文本框中输入路径，或通过选择  “浏览”按钮，修改项目的创建路径。

5. （可选）在 **“解决方案”** 名称文本框中，输入要用于解决方案的名称。

6. 保持选中 **“创建解决方案的目录”** 选项并选择 **“确定”** 按钮。

   ![定制的单元测试库](../test/media/unit_test_win8_1.png)

   解决方案资源管理器中会填充 UWP 单元测试项目，代码编辑器中显示标题为“UnitTest1”的默认单元测试  。

   ![新建定制的单元测试项目](../test/media/unit_test_win8_unittestexplorer_newprojectcreated.png)

::: moniker-end

## <a name="edit-the-unit-test-projects-uwp-application-manifest-file"></a>编辑单元测试项目的 UWP 应用程序清单文件

1. 在解决方案资源管理器中，右键单击 Package.appxmanifest 文件并选择“打开”    。

2. 在“清单设计器”中，选择“功能”选项卡   。

3. 在 **“功能”** 下面的列表中，选择你的单元测试和所测试代码需要具备的功能。 例如，单元测试及其测试的代码需要具备访问 Internet 的功能，那么请选中 **“Internet”** 复选框。

   > [!NOTE]
   > 所选功能只应包括单元测试正常运行所需的功能。

   ![单元测试清单](../test/media/unit_test_win8_.png)

## <a name="code-the-unit-test-for-a-uwp-app"></a>为 UWP 应用编码单元测试

在代码编辑器中，编辑单元测试并添加测试所需的断言和逻辑。

## <a name="run-unit-tests"></a>运行单元测试

生成解决方案并在测试资源管理器中运行单元测试：

1. 在 **“测试”** 菜单中，选择 **“窗口”** ，然后选择 **“测试资源管理器”** 。

2. 从 **“生成”** 菜单中选择 **“生成解决方案”** 。

   现在，你的单元测试将显示在测试资源管理器中。

   > [!NOTE]
   > 必须生成解决方案，才能在“测试资源管理器”中更新单元测试列表。

3. 在测试资源管理器中，选择创建的单元测试  。

4. 选择 **“全部运行”** 。

   ![单元测试资源管理器 - 运行单元测试](../test/media/unit_test_win8_unittestexplorer_contextmenurun.png)

   > [!TIP]
   > 可以选择测试资源管理器中列出的一个或多个单元测试，然后右击并选择“运行选定测试”  。
   >
   > 此外，你也可以选择 **“调试所选测试”** 、 **“打开测试”** ，并使用 **“属性”** 选项。
   >
   > ![单元测试资源管理器 - 单元测试上下文菜单](../test/media/unit_test_win8_unittestexplorer_contextmenu.png)

   单元测试将运行。 完成后，测试资源管理器会显示测试状态、运行时间并提供指向源的链接。

   ![单元测试资源管理器 - 已完成测试](../test/media/unit_test_win8_unittestexplorer_done.png)

## <a name="see-also"></a>请参阅

- [使用 Visual Studio 测试 UWP 应用](../test/unit-test-your-code.md)
- [生成和测试 UWP 应用](/azure/devops/pipelines/apps/windows/universal?tabs=vsts)