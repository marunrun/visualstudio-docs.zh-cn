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
ms.openlocfilehash: 9843b47e38d5d33a25c455efe619dfcc033fb334
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "71933476"
---
## <a name="discover-and-view-tests"></a>发现和查看测试

根据惯例，Visual Studio 将测试标识为名称以“`test`”开头的方法。 若要查看此行为，请执行以下操作：

1. 打开一个 Visual Studio 中加载的 [Python 项目](../../managing-python-projects-in-visual-studio.md)，右键单击该项目，选择“添加” > “新建项”，然后选择其后有“添加”的“Python 单元测试” 。

1. 如果直接运行脚本，此操作将创建具有导入标准 `unittest` 模块的代码的 test1.py 文件，从 `unittest.TestCase` 派生一个测试类，并调用 `unittest.main()`：

    ```python

    import unittest

    class Test_test1(unittest.TestCase):
        def test_A(self):
            self.fail("Not implemented")

    if __name__ == '__main__':
        unittest.main()
    ```

1. 根据需要保存该文件，然后通过“测试” > “窗口” > “测试资源管理器”菜单命令打开“测试资源管理器”。

1. “测试资源管理器”  会搜索要测试的项目并进行显示，如下所示。 双击测试打开其源文件。

    ![显示默认 test_A 的测试资源管理器](../../media/unit-test-A.png)

1. 向项目添加更多测试时，可以使用工具栏上的“分组”菜单整理“测试资源管理器”中视图：

    ![测试资源管理器分组工具栏菜单](../../media/unit-test-group-menu.png)

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

若要开始调试，请在代码中设置初始断点，然后在“测试资源管理器”  中右键单击测试（或所做选择），然后选择“调试所选测试”  。 Visual Studio 会启动 Python 调试程序，与为应用程序代码启动 Python 调试器一样。

![调试测试](../../media/unit-test-debugging.png)

还可以使用“分析所选测试的代码覆盖率”  。 有关详细信息，请参阅[使用代码覆盖率确定正在测试的代码数量](../../../test/using-code-coverage-to-determine-how-much-code-is-being-tested.md)。

### <a name="known-issues"></a>已知问题

- 启动调试时，Visual Studio 会显示启动和停止调试，然后重新启动。 此行为是预期的行为。
- 调试多个测试时，因为每个测试都是独立运行，所以会中断调试会话。
- 调试时，Visual Studio 启动测试会间歇性地失败。 通常情况下，尝试再次调试测试会成功。
- 调试时，可能会跳出测试转到 `unittest` 实现。 通常情况下，下一步会运行到程序结束，然后停止调试。
