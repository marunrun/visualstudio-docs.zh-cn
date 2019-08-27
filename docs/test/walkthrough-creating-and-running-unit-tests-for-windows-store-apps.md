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
ms.openlocfilehash: 1284dc529e4f150b282dcab2d919e027c9b606c4
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62976420"
---
# <a name="walkthrough-create-and-run-unit-tests-for-uwp-apps"></a>演练：创建并运行 UWP 应用的单元测试

Visual Studio 支持对通用 Windows 平台 (UWP) 应用进行单元测试。 其中包括 Visual C#、Visual Basic 和 Visual C++ 的单元测试项目模板。

> [!TIP]
> 有关开发 UWP 应用的详细信息，请参阅 [UWP 应用入门](/windows/uwp/get-started/)。

以下过程描述了为 UWP 应用创建、运行和调试单元测试的步骤。

## <a name="create-a-unit-test-project-for-a-uwp-app"></a>为 UWP 应用创建单元测试项目

1. 从 **“文件”** 菜单中选择 **“新建项目”**。

     此时将显示“新建项目”对话框。

2. 在“模板”之下，选择要用以创建单元测试的编程语言，然后选择关联的 Windows 通用单元测试库。 例如，选择“Visual C#”，选择“Windows 通用”，然后选择“单元测试库(通用 Windows)”。

3. （可选）在“名称”文本框中，输入要用于项目的名称。

4. （可选）通过在“位置”文本框中输入路径，或通过选择“浏览”按钮，修改项目的创建路径。

5. （可选）在 **“解决方案”** 名称文本框中，输入要用于解决方案的名称。

6. 保持选中 **“创建解决方案的目录”** 选项并选择 **“确定”** 按钮。

     ![定制的单元测试库](../test/media/unit_test_win8_1.png)

     解决方案资源管理器中会填充 UWP 单元测试项目，代码编辑器中显示标题为“UnitTest1”的默认单元测试。

     ![新建定制的单元测试项目](../test/media/unit_test_win8_unittestexplorer_newprojectcreated.png)

## <a name="edit-the-unit-test-projects-uwp-application-manifest-file"></a>编辑单元测试项目的 UWP 应用程序清单文件

1. 在解决方案资源管理器中，右键单击 Package.appxmanifest 文件并选择“打开”。

     “清单设计器”将显示以便进行编辑。

2. 在“清单设计器”中，选择“功能”选项卡。

3. 在 **“功能”** 下面的列表中，选择你的单元测试和所测试代码需要具备的功能。 例如，单元测试及其测试的代码需要具备访问 Internet 的功能，那么请选中 **“Internet”** 复选框。

    > [!NOTE]
    > 所选功能只应包括单元测试正常运行所需的功能。

     ![单元测试清单](../test/media/unit_test_win8_.png)

## <a name="code-the-unit-test-for-a-uwp-app"></a>为 UWP 应用编码单元测试

在代码编辑器中，编辑单元测试并添加测试所需的断言和逻辑。

## <a name="run-unit-tests"></a>运行单元测试

### <a name="to-build-the-solution-and-run-the-unit-test-using-test-explorer"></a>生成解决方案并在“测试资源管理器”中运行单元测试

1. 在 **“测试”** 菜单中，选择 **“窗口”**，然后选择 **“测试资源管理器”**。

     测试资源管理器将显示，但不会列出你的测试。

2. 从 **“生成”** 菜单中选择 **“生成解决方案”**。

     现在，你的单元测试已列出。

    > [!NOTE]
    > 必须生成解决方案，才能在“测试资源管理器”中更新单元测试列表。

3. 在测试资源管理器中，选择创建的单元测试。

    > [!TIP]
    > “测试资源管理器”在 **“源:”** 旁边提供指向源代码的链接。

4. 选择 **“全部运行”**。

     ![单元测试资源管理器 - 运行单元测试](../test/media/unit_test_win8_unittestexplorer_contextmenurun.png)

    > [!TIP]
    > 可以选择资源管理器中列出的一个或多个单元测试，然后右击并选择 **“运行选定测试”**。
    >
    > 此外，你也可以选择 **“调试所选测试”**、 **“打开测试”**，并使用 **“属性”** 选项。
    >
    > ![单元测试资源管理器 - 单元测试上下文菜单](../test/media/unit_test_win8_unittestexplorer_contextmenu.png)

    单元测试将运行。 完成后，测试资源管理器会显示测试状态、运行时间并提供指向源的链接。

    ![单元测试资源管理器 - 已完成测试](../test/media/unit_test_win8_unittestexplorer_done.png)

## <a name="see-also"></a>请参阅

- [使用 Visual Studio 测试 UWP 应用](../test/unit-test-your-code.md)
- [生成和测试 UWP 应用](/azure/devops/pipelines/apps/windows/universal?tabs=vsts)