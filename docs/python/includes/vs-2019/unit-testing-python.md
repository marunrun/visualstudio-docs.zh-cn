---
title: 单元测试 Python 代码
description: 在 Visual Studio 中为 Python 代码设置单元测试，以充分利用测试资源管理器功能来发现、运行和调试测试。
ms.date: 09/18/2019
ms.topic: include
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.custom: seodec18
ms.workload:
- python
- data-science
ms.openlocfilehash: 8adce700524c4ade6c627aa91480460f8f2571f2
ms.sourcegitcommit: 9f6f63a2d76c6e579b4b67a96ec86faba99ad1df
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/03/2019
ms.locfileid: "71933436"
---
## <a name="select-the-test-framework-for-a-python-project"></a>选择适用于 Python 项目的测试框架

Visual Studio 支持两种适用于 Python 的测试框架，即 [unittest](https://docs.python.org/3/library/unittest.html) 和 [pytest](https://pytest.org/en/latest/)（从版本 16.3 开始，在 Visual Studio 2019 中可用）。 默认情况下，在创建 Python 项目时，不会选择任何框架。 若要指定框架，在“解决方案资源管理器”中，右键单击“项目名称”，然后选择“属性”选项  。 此操作将打开项目设计器，可用于通过“测试”选项卡配置测试  。在此选项卡中，可以选择要用于项目的测试框架。 

* 对于 unittest 框架，项目的根目录用于测试发现  。 可在“测试”选项卡上将此位置以及用于标识测试的文本模式修改为用户指定的值  。
* 对于 pytest 框架，测试位置和文件名模式等测试选项是使用标准的 pytest .ini 配置文件指定的  。 有关详细信息，请参阅 [pytest 参考文档](https://docs.pytest.org/en/latest/reference.html#ini-options-ref)。

保存框架选择和设置后，将在“测试资源管理器”中启动测试发现。 如果“测试资源管理器”窗口尚未打开，请导航至工具栏并选择“测试” > “测试资源管理器”   。

## <a name="configure-testing-for-python-without-a-project"></a>在不使用项目的情况下针对 Python 配置测试
使用 Visual Studio，可以在不使用项目的情况下运行和测试现有 Python 代码，方法是使用 Python 代码[打开文件夹](../../quickstart-05-python-visual-studio-open-folder.md)。 在这些情况下，需要使用 PythonSettings.json 文件来配置测试  。 
1. 使用“打开本地文件夹”选项来打开现有 Python 代码  。 

   ![Visual Studio 启动屏幕](../../media/quickstart-open-folder/01-open-local-folder.png)

1. 在“解决方案资源管理器”窗口中，单击“显示所有文件”图标以显示当前文件夹中的所有文件  。

   ![“显示所有文件”按钮](../../media/unit-test-show-files.png)

1. 导航到“本地设置”文件夹中的 PythonSettings.json 文件   。 如果在“本地设置”文件夹中看不到此文件，请手动创建它  。
   
1. 将字段 TestFramework 添加到设置文件，并将其设置为 pytest 或 unittest，具体取决于要使用的测试框架    。

    ```json
    {
    "TestFramework": "unittest",
    "UnitTestRootDirectory": "testing",
    "UnitTestPattern": "test_*.py"
    }
    ```

    > [!Note]
    > 对于 unittest 框架，如果未在 PythonSettings.json 文件中指定字段 UnitTestRootDirectory 和 UnitTestPattern，则系统会添加它们并分别向其分配默认值“.”和“test*.py”    。

1. 如果你的文件夹包含 src 目录，该目录独立于包含测试的文件夹，则使用 PythonSettings.json 文件中的 SearchPaths 字段指定指向 src 文件夹的路径     。

    ```json
    {
    "TestFramework": "unittest",
    "UnitTestRootDirectory": "testing",
    "UnitTestPattern": "test_*.py",
    "SearchPaths": [ ".\\src"]
    }
    ```

1. 保存对 PythonSettings.json 文件的更改，以启动指定框架的测试发现。 
   > [!Note]
   > 如果“测试资源管理器”窗口已打开，按 Ctrl + R,A 也会触发发现   。

## <a name="discover-and-view-tests"></a>发现和查看测试

默认情况下，Visual Studio 将 unittest 和 pytest 测试标识为名称以“`test`”开头的方法   。 若要查看测试发现，请执行以下操作：

1. 打开 [Python 项目](../../managing-python-projects-in-visual-studio.md)。

1. 在 Visual Studio 中加载项目后，在“解决方案资源管理器”中，右键单击“项目”，然后从“属性测试”选项卡中选择 unittest 或 pytest 框架    。
   > [!Note]
   > 如果使用 pytest 框架，可以使用标准的 pytest .ini 配置文件指定测试位置和文件名模式。 默认情况下，使用工作区/项目文件夹，模式为 `test_*py` 和 `*_test.py`。 有关详细信息，请参阅 [pytest 参考文档](https://docs.pytest.org/en/latest/reference.html#ini-options-ref)。

1. 选择框架后，再次右键单击项目，选择“添加” > “新建项”，然后依次选择“Python 单元测试”、“添加”     。

1. 如果直接运行脚本，此操作将创建具有可导入标准 `unittest` 模块的代码的 test_1.py 文件，从 `unittest.TestCase` 派生一个测试类，并调用 `unittest.main()`  ：

    ```python
    import unittest

    class Test_test1(unittest.TestCase):
        def test_A(self):
            self.fail("Not implemented")

    if __name__ == '__main__':
        unittest.main()
    ```

1. 根据需要保存该文件，然后通过“测试” > “测试资源管理器”菜单命令打开“测试资源管理器”    。

1. “测试资源管理器”  会搜索要测试的项目并进行显示，如下所示。 双击测试打开其源文件。

    ![显示默认 test_A 的测试资源管理器](../../media/unit-test-a-2.png) 

1. 向项目添加更多测试时，可以使用工具栏上的“分组依据”菜单整理“测试资源管理器”中的视图   ：

    ![测试资源管理器分组工具栏菜单](../../media/unit-test-group-menu-2.png) 

1. 还可以在“搜索”  字段中输入文本以按名称筛选测试。

有关 `unittest` 模块和编写测试的详细信息，请参阅 [Python 2.7 文档](https://docs.python.org/2/library/unittest.html)或 [Python 3.7 文档](https://docs.python.org/3/library/unittest.html) (python.org)。

## <a name="run-tests"></a>运行测试

在“测试资源管理器”  中，可以通过多种方式来运行测试：

- “运行所有”  将运行所有显示的测试（取决于筛选器）。
- “运行”  菜单提供以下命令：运行失败的、通过的或未作为一组运行的测试。
- 可以选择一个或多个测试，右键单击，然后选择“运行选定测试”  。

测试在后台运行，每个测试完成后，“测试资源管理器”  将更新其状态：

- 通过的测试将显示一个绿勾和运行测试所花费的时间：

    ![test_A 通过状态](../../media/unit-test-A-pass.png)

- 失败的测试将显示带有**输出**链接的红叉，该链接显示控制台输出和测试运行中的 `unittest` 输出：

    ![test_A 失败状态](../../media/unit-test-A-fail.png)

    ![test_A 失败及原因](../../media/unit-test-A-fail-reason.png)

## <a name="debug-tests"></a>调试测试

因为单元测试是代码片段，所以和任何其他代码一样会受到 bug 的影响，有时需要在调试器中运行。 在调试程序中，可以设置断点、检查变量和逐行执行代码。 Visual Studio 还提供了用于单元测试的诊断工具。

> [!Note]
> 默认情况下，测试调试使用 ptvsd 4 调试程序。 如果要改用 ptvsd 3，可以在“工具” > “选项” > “Python” > “调试”中选择“使用旧版调试程序”      。 

若要开始调试，请在代码中设置初始断点，然后在“测试资源管理器”  中右键单击测试（或所做选择），然后选择“调试所选测试”  。 Visual Studio 会启动 Python 调试程序，与为应用程序代码启动 Python 调试器一样。

![调试测试](../../media/unit-test-debugging.png)

还可以使用“分析所选测试的代码覆盖率”  。 有关详细信息，请参阅[使用代码覆盖率确定正在测试的代码数量](../../../test/using-code-coverage-to-determine-how-much-code-is-being-tested.md)。
