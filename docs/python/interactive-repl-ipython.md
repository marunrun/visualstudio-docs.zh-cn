---
title: IPython REPL（交互式窗口）
description: 使用 IPython 模式下的 Visual Studio 交互窗口提供用户友好交互式开发环境，并具有交互式并行计算功能。
ms.date: 01/28/2019
ms.topic: conceptual
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.custom: seodec18
ms.workload:
- python
- data-science
ms.openlocfilehash: 8b4510ed738fdd2b33389ab4242dbde86cffff8c
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "62957718"
---
# <a name="use-ipython-in-the-interactive-window"></a>在交互窗口中使用 IPython

IPython 模式下的 Visual Studio 交互窗口是目前非常先进的用户友好交互式开发环境，具有交互式并行计算功能  。 本文演示如何在 Visual Studio 交互窗口中使用 IPython，其中所有常规[交互窗口](python-interactive-repl-in-visual-studio.md)功能均可用  。

要执行此演练，必须先安装 [Anaconda](https://www.continuum.io) 环境，其中包括 IPython 和必需的库。

> [!Note]
> IronPython 不支持 IPython，但事实上，可以在交互选项窗体上选择 IPython  。 有关详细信息，请参阅[功能请求](https://github.com/Microsoft/PTVS/issues/84)。

1. 打开 Visual Studio，切换到 Python 环境窗口（“视图” > “其他窗口” > “Python 环境”），然后选择 Anaconda 环境     。

2. 检查该环境的“包(Conda)”选项卡（可能显示为 pip 或包），确保已列出 `ipython` 和 `matplotlib`    。 如果没有，请在此处安装。 （请参阅 [Python 环境窗口 -“包”选项卡](python-environments-window-tab-reference.md)。）

3. 依次选择“概述”选项卡和“使用 IPython 交互模式”   。 （在 Visual Studio 2015 中，选择“配置交互选项”以打开“选项”对话框，将“交互模式”设置为 IPython，然后选择“确定”      。）

4. 选择“打开交互窗口”，在 IPython 模式下打开交互窗口   。 如果仅更改了交互模式，可能需要重置窗口；如果仅显示 >>> 提示符，则可能还需按 Enter，以便获得提示符（如“在 [2] 中”）   。

    ![IPython 模式中的交互窗口](media/ipython-repl-03.png)

5. 输入以下代码：

   ```python
   import matplotlib.pyplot as plt
   import numpy as np

   x = np.linspace(0, 5, 10)
   y = x ** 2
   plt.plot(x, y, 'r', x, x ** 3, 'g', x, x ** 4, 'b')
   ```

6. 输入最后一行后，应看到一个内联关系图（可根据需要，拖动右下角重设大小）。

    ![交互窗口中的内联关系图](media/ipython-repl-04.png)

7. 可在编辑器中编写代码，再将其选中并右键单击，然后选择“Send to Interactive”命令（或按 Ctrl+Enter），而无需键入 REPL    。 请将以下代码粘贴到编辑器中的新文件中，使用 Ctrl+A 将其选中，然后发送到交互窗口    。 （Visual Studio 将代码作为一个单位发送，避免提供关系图的中间部分或其中一部分。 如果未在所选的其他环境中打开 Python 项目，Visual Studio 将为在“Python 环境”窗口中选择为默认环境的任何环境打开一个交互窗口   。）

    ```python
    from mpl_toolkits.mplot3d import Axes3D
    import matplotlib.pyplot as plt
    import numpy as np
    fig = plt.figure()
    ax = fig.add_subplot(111, projection='3d')
    for c, z in zip(['r', 'g', 'b', 'y'], [30, 20, 10, 0]):
        xs = np.arange(20)
        ys = np.random.rand(20)
        # You can provide either a single color or an array. To demonstrate this,
        # the first bar of each set is colored cyan.
        cs = [c] * len(xs)
        cs[0] = 'c'
        ax.bar(xs, ys, zs=z, zdir='y', color=cs, alpha=0.8)

    ax.set_xlabel('X')
    ax.set_ylabel('Y')
    ax.set_zlabel('Z')
    plt.show()
    ```

    ![将代码从编辑器发送到交互窗口](media/ipython-repl-05.png)

8. 若要查看在交互窗口之外的关系图，请运行代码，而不是使用“Debug” > “Start without Debugging”命令    。

IPython 有很多其他有用的功能，如转义到系统外壳、变量替换、捕获输出等。请参阅 [IPython 文档](https://ipython.org/documentation.html)了解详细信息。

## <a name="see-also"></a>请参阅

- 若要在不安装的情况下轻松使用 Jupyter，请试用免费的 [Azure 笔记本托管服务](https://notebooks.azure.com/)来保留笔记本并与他人进行共享。

- 还预配置了 [Azure Data Science Virtual Machine](/azure/machine-learning/data-science-virtual-machine/overview) 以运行 Jupyter 笔记本以及各种其他数据科学工具。
