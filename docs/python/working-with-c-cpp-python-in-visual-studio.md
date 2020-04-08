---
title: 编写 Python 的 C++ 扩展
description: 使用 Visual Studio、CPython 和 PyBind11 创建适用于 Python 的 C++ 扩展的演练，包括混合模式调试。
ms.date: 11/19/2018
ms.topic: conceptual
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.custom: seodec18
ms.workload:
- python
- data-science
ms.openlocfilehash: 9c81984e8921e44e32b58ae7f5c5c27c5fe8b12f
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "62956925"
---
# <a name="create-a-c-extension-for-python"></a>创建适用于 Python 的 C++ 扩展

使用 C++（或 C）编写的模块常用于扩展 Python 解释器的功能和启用对低级别操作系统功能的访问。 主要有以下 3 种类型的模块：

- 加速器模块：Python 是一种解释型语言，某些代码段可使用 C++ 进行编写来提高性能。
- 包装器模块：向 Python 代码公开现有 C/C++ 接口，或公开易于通过 Python 使用的更“Python 化”的 API。
- 低级别系统访问模块：用于访问 CPython 运行时的较低级别功能、操作系统或基础硬件。

本文介绍了如何为 CPython 生成 C++ 扩展模块，该模块计算双曲正切并从 Python 代码中调用它。 首先使用 Python 实现此例程，以演示使用 C++ 实现此相同例程时可获得的相对性能提升。

本文还演示了使 C++ 可用于 Python 的两种方法：

- [Python 文档](https://docs.python.org/3/c-api/)中所述的标准 CPython 扩展
- [PyBind11](https://github.com/pybind/pybind11)，由于其简单易用，推荐用于 C++ 11。

本文末尾的[替代方法](#alternative-approaches)下可找到这些方法与其他方法的比较。

要获取本演练的完整示例，请访问 [python-samples-vs-cpp-extension](https://github.com/Microsoft/python-sample-vs-cpp-extension) (GitHub)。

## <a name="prerequisites"></a>先决条件

- 将 C++ 桌面开发和 Python 开发工作负载作为默认选项安装的 Visual Studio 2017 或更高版本。
- 在“Python 开发”工作负载中，同时选择右侧的“Python 本机开发工具”方框。 此选项设置本文所述的大部分配置。 （此选项还自动包括 C++ 工作负载。）

    ![选择“Python 本机开发工具”选项](media/cpp-install-native.png)

    > [!Tip]
    > 安装**数据科学和分析应用程序**工作负载还包括默认安装 Python 和“Python 本机开发工具”选项。

有关详细信息，请参阅[安装针对 Visual Studio 的 Python 支持](installing-python-support-in-visual-studio.md)，其中包括使用其他版本的 Visual Studio。 如果单独安装 Python，请务必在安装程序的“高级选项”下选择“下载调试符号”和“下载调试二进制文件”。 此选项确保在选择进行调试生成时能够使用必要的调试库。

## <a name="create-the-python-application"></a>创建 Python 应用程序

1. 要在 Visual Studio 中创建新 Python 项目，请选择“文件” > “新建” > “项目”。 搜索"Python"，选择“Python 应用程序”模板，为其提供合适的名称和位置，然后选择“确定”。

1. 必须具备 32 位 Python 解释器才可使用 C++（推荐 Python 3.6 或更高版本）。 在 Visual Studio 的“解决方案资源管理器”窗口中，展开项目节点，然后展开“Python 环境”节点。 如果发现默认值不是 32 位环境（加粗或标记为“全局默认值”），请按照[选择项目的 Python 环境](selecting-a-python-environment-for-a-project.md)中的说明进行操作。 如果未安装 32 位解释器，请参阅[安装 Python 解释器](installing-python-interpreters.md)。

1. 在项目的 .py 文件中，粘贴以下代码，用于对双曲正切的计算进行基准测试（无需使用数学库即可实现，以便简化比较）。 可随意手动输入代码，体验某些 [Python 编辑功能](editing-python-code-in-visual-studio.md)。

    ```python
    from itertools import islice
    from random import random
    from time import perf_counter

    COUNT = 500000  # Change this value depending on the speed of your computer
    DATA = list(islice(iter(lambda: (random() - 0.5) * 3.0, None), COUNT))

    e = 2.7182818284590452353602874713527

    def sinh(x):
        return (1 - (e ** (-2 * x))) / (2 * (e ** -x))

    def cosh(x):
        return (1 + (e ** (-2 * x))) / (2 * (e ** -x))

    def tanh(x):
        tanh_x = sinh(x) / cosh(x)
        return tanh_x

    def test(fn, name):
        start = perf_counter()
        result = fn(DATA)
        duration = perf_counter() - start
        print('{} took {:.3f} seconds\n\n'.format(name, duration))

        for d in result:
            assert -1 <= d <= 1, " incorrect values"

    if __name__ == "__main__":
        print('Running benchmarks with COUNT = {}'.format(COUNT))

        test(lambda d: [tanh(x) for x in d], '[tanh(x) for x in d] (Python implementation)')
    ```

1. 使用“调试” > “启动而不调试”(Ctrl+F5) 运行程序以查看结果。 用户可调整 `COUNT` 变量，更改基准检验的运行时长。 对于本演练，请将计数设置为让基准检验运行约 2 秒。

> [!TIP]
> 运行基准检验时，请始终使用“调试” > “启动而不调试”，从而避免在 Visual Studio 调试器中运行代码时产生开销。

## <a name="create-the-core-c-projects"></a>创建核心 C++ 项目

按照本节中的说明，创建名为“superfastcode”和“superfastcode2”的两个完全相同的 C++ 项目。 之后，在每个项目中使用不同的方法将 C++ 代码公开到 Python。

1. 确保将 `PYTHONHOME` 环境变量设置为要使用的 Python 解释器。 Visual Studio 中的 C++ 项目依赖此变量来定位 python.h 等文件，这些文件在创建 Python 扩展时使用。

1. 在“解决方案资源管理器”中右键单击此解决方案并选择“添加” > “新建项目”。 一个 Visual Studio 解决方案可同时包含 Python 和 C++ 项目（这是使用 Visual Studio for Python 的优势之一）。

1. 搜索“C++”，选择“空项目”，指定名称“superfastcode”（第二个项目则指定名称“superfastcode2”），然后选择“确定”。

    > [!Tip]
    > 如果在 Visual Studio 中安装了 Python 本机开发工具，则可改为从 Python 扩展模块模板开始，其中有许多现成的以下所述的内容。 但是，对于本演练，从空项目开始可以逐步演示如何生成扩展模块。 了解该过程后，在编写自己的扩展时，使用模板可帮助你节省时间。

1. 在新项目中创建 C++ 文件，方法是右键单击“源文件”节点，然后选择“添加” > “新建项”，选择“C++ 文件”，将其命名为 `module.cpp`，然后选择“确定”。

    > [!Important]
    > 需要扩展名为 .cpp 的文件才能在随后步骤中打开 C++ 属性页。

1. 右键单击“解决方案资源管理器”中的 C++ 项目，然后选择“属性”。

1. 在显示的“属性页”对话框顶部，将“配置”设置为“所有配置”，并将“平台”设置为“Win32”。

1. 如下表所述设置特定属性，然后选择“确定”。

    | Tab | Property | “值” |
    | --- | --- | --- |
    | **常规** | **常规** > **目标名称** | 指定想要在 `from...import` 语句中从 Python 引用的模块的名称。 定义 Python 的模块时，在 C++ 中使用相同的名称。 如果想要将项目的名称用作模块名称，请保留默认值 $(ProjectName)。 |
    | | **常规** > **目标扩展名** | **.pyd** |
    | | **项目默认值** > **配置类型** | **动态库(.dll)** |
    | **C/C++** > **常规** | **附加包含目录** | 根据相应的安装添加 Python“include” 文件夹，例如 `c:\Python36\include`。  |
    | **C/C++** > **预处理器** | **预处理器定义** | **仅 CPython**：将 `Py_LIMITED_API;` 添加到字符串开头（包括分号）。 此定义会限制可从 Python 调用的某些函数，并使代码在 Python 不同版本之间更易于移植。 如果使用的是 PyBind11，请勿添加此定义，否则将会看到生成错误。 |
    | **C/C++** > **代码生成** | **运行时库** | **多线程 DLL (/MD)**（请参阅下面的“警告”） |
    | 链接器 > **常规** | **附加库目录** | 根据相应的安装添加包含 .lib 文件的 Python“libs”文件夹，例如 `c:\Python36\libs`。 （务必指向包含 .lib 文件的“libs”文件夹，而非包含 .py 文件的 Lib 文件夹。） |

    > [!Tip]
    > 如果在项目属性中未看到 C/C++ 选项卡，这是因为项目不包含标识为 C/C++ 源文件的任何文件。 如果创建的源文件不含 .c 或 .cpp 扩展名，则可能出现这种情况。 例如，如果之前在“新建项”对话框中不小心输入了 `module.coo`（而不是 `module.cpp`），则 Visual Studio 会创建文件，但不会将文件类型设置为“C/C+ 代码”，而正是它激活 C/C++ 属性选项卡。即使将文件重命名为带 `.cpp`，此类识别错误仍会存在。 为了正确设置文件类型，请在“解决方案资源管理器”中右键单击文件，选择“属性”，然后将“文件类型”设置为“C/C++ 代码”。

    > [!Warning]
    > 即使对于调试配置，也始终将“C/C++” > “代码生成” > “运行时库”选项设置为“多线程 DLL (/MD)”，因为此设置是生成非调试 Python 二进制文件时使用的设置。 使用 CPython 时，如果碰巧设置了“多线程调试 DLL (/MDd)”选项，生成“调试”配置会生成错误 C1189:Py_LIMITED_API is incompatible with Py_DEBUG, Py_TRACE_REFS, and Py_REF_DEBUG。 此外，如果删除 `Py_LIMITED_API`（使用 CPython 时必须这样做，但在使用 PyBind11 时则不是）以免出现生成错误，Python 会在尝试导入模块时发生故障。 （如下所述，对 `PyModule_Create` 的 DLL 调用中发生故障，显示输出消息“Python 错误:PyThreadState_Get: 无当前线程”。）
    >
    > /MDd 选项用于生成 Python 调试二进制文件（例如 python_d.exe），但对扩展 DLL 选择此选项仍会导致 `Py_LIMITED_API` 的生成错误。

1. 右键单击 C++ 项目，然后选择“生成”来测试配置（包括“调试”和“发布”）。 .pyd 文件位于“调试”和“发布”下的“解决方案”文件夹中，而非位于 C++ 项目文件夹本身。

1. 将以下代码添加到 C++ 项目的 module.cpp 文件：

    ```cpp
    #include <Windows.h>
    #include <cmath>

    const double e = 2.7182818284590452353602874713527;

    double sinh_impl(double x) {
        return (1 - pow(e, (-2 * x))) / (2 * pow(e, -x));
    }

    double cosh_impl(double x) {
        return (1 + pow(e, (-2 * x))) / (2 * pow(e, -x));
    }

    double tanh_impl(double x) {
        return sinh_impl(x) / cosh_impl(x);
    }
    ```

1. 再次生成 C++ 项目以确认代码正确。

1. 如果尚未执行此操作，请重复上述步骤，再创建一个内容相同的项目，且名为“superfastcode2”。

## <a name="convert-the-c-projects-to-extensions-for-python"></a>将 C++ 项目转换为适用于 Python 的扩展

若要使 C++ DLL 成为适用于 Python 的扩展，首先应修改导出的方法以与 Python 类型交互。 然后，添加一个可导出模块的函数以及该模块的方法的定义。

以下各节介绍如何使用 CPython 扩展和 PyBind11 执行这些步骤。

### <a name="cpython-extensions"></a>CPython 扩展

要了解本节介绍的有关 Python 3.x 的背景信息，请在 python.org 上参阅 [Python/C API Reference Manual](https://docs.python.org/3/c-api/index.html)（Python/C API 参考手册），并着重了解 [Module Objects](https://docs.python.org/3/c-api/module.html)（模块对象）（请不要忘记从右上角的下拉列表中选择你的 Python 版本，以便查看正确的文档）。

如果使用的是 Python 2.7，请改为参阅 python.org 上的 [Extending Python 2.7 with C or C++](https://docs.python.org/2.7/extending/extending.html)（使用 C 或 C++ 扩展 Python 2.7）和 [Porting Extension Modules to Python 3](https://docs.python.org/2.7/howto/cporting.html)（将扩展模块移植到 Python 3）。

1. 在 module.cpp 的顶部，包含 Python.h：

    ```cpp
    #include <Python.h>
    ```

1. 修改 `tanh_impl` 方法以接受和返回 Python 类型（即，`PyOjbect*`）：

    ```cpp
    PyObject* tanh_impl(PyObject *, PyObject* o) {
        double x = PyFloat_AsDouble(o);
        double tanh_x = sinh_impl(x) / cosh_impl(x);
        return PyFloat_FromDouble(tanh_x);
    }
    ```

1. 添加一个定义如何向 Python 呈现 C++ `tanh_impl` 函数的结构：

    ```cpp
    static PyMethodDef superfastcode_methods[] = {
        // The first property is the name exposed to Python, fast_tanh, the second is the C++
        // function name that contains the implementation.
        { "fast_tanh", (PyCFunction)tanh_impl, METH_O, nullptr },

        // Terminate the array with an object containing nulls.
        { nullptr, nullptr, 0, nullptr }
    };
    ```

1. 添加一个定义模块的结构，因为要在 Python 代码中引用它（特别是在使用 `from...import` 语句时）。 （使其与“配置属性” > “常规” > “目标名称”中的项目属性中的值匹配。）在以下示例中，“superfastcode”模块名意味着可在 Python 中使用 `from superfastcode import fast_tanh`，因为 `fast_tanh` 是在 `superfastcode_methods` 中定义的。 （C++ 项目内部使用的文件名，如 module.cpp，是无关紧要的。）

    ```cpp
    static PyModuleDef superfastcode_module = {
        PyModuleDef_HEAD_INIT,
        "superfastcode",                        // Module name to use with Python import statements
        "Provides some functions, but faster",  // Module description
        0,
        superfastcode_methods                   // Structure that defines the methods of the module
    };
    ```

1. 添加 Python 加载模块时要调用的方法，该模块必须命名为 `PyInit_<module-name>`，其中 &lt;module-name&gt; 与 C++ 项目的“常规” > “目标名称”属性完全匹配（也就是说，其与项目生成的 .pyd 的文件名相匹配）。

    ```cpp
    PyMODINIT_FUNC PyInit_superfastcode() {
        return PyModule_Create(&superfastcode_module);
    }
    ```

1. 将目标配置设置为“发布”并再次生成 C++ 项目来验证代码。 如果遇到错误，请参阅下面的[疑难解答](#troubleshooting)一节。

### <a name="pybind11"></a>PyBind11

如果已完成上一节中的步骤，你肯定已注意到，你使用了大量样本代码来为 C++ 代码创建必要的模块结构。 PyBind11 通过 C++ 头文件中的宏简化了进程，这些宏通过更少的代码实现了相同的结果。 有关本节所示内容的背景信息，请参阅[PyBind11 基础知识](https://github.com/pybind/pybind11/blob/master/docs/basics.rst)。

1. 使用 pip 安装 PyBind11：`pip install pybind11` 或 `py -m pip install pybind11`。

1. 在 module.cpp 的顶部，包含 pybind11.h：

    ```cpp
    #include <pybind11/pybind11.h>
    ```

1. 在 module.cpp 的底部，使用 `PYBIND11_MODULE` 宏来定义 C++ 函数的入口点：

    ```cpp
    namespace py = pybind11;

    PYBIND11_MODULE(superfastcode2, m) {
        m.def("fast_tanh2", &tanh_impl, R"pbdoc(
            Compute a hyperbolic tangent of a single argument expressed in radians.
        )pbdoc");

    #ifdef VERSION_INFO
        m.attr("__version__") = VERSION_INFO;
    #else
        m.attr("__version__") = "dev";
    #endif
    }
    ```

1. 将目标配置设置为“发布”并生成 C++ 项目来验证代码。 如果遇到错误，请参阅下一节有关疑难解答的内容。

### <a name="troubleshooting"></a>疑难解答

C++ 模块可能无法编译的原因如下：

- 无法找到 Python.h （E1696：无法打开源文件 "Python.h" 和/或 C1083：无法打开 include 文件："Python.h"：没有此类文件或目录）：验证项目属性中的“C/C++” > “常规” > “附加 Include 目录”中的路径是否指向 Python 安装的“include”文件夹。 请参阅[创建核心 C++ 项目](#create-the-core-c-projects)中的步骤 6。

- 无法找到 Python 库：验证项目属性中的“链接器” > “常规” > “附加库目录”中的路径是否指向 Python 安装的“libs”文件夹。 请参阅[创建核心 C++ 项目](#create-the-core-c-projects)中的步骤 6。

- 与目标体系结构相关的链接器错误：更改 C++ 目标的项目体系结构以匹配 Python 安装。 例如，如果你将 C++ 项目的目标定为 x64，但是 Python 安装是 x86，则将 C++ 项目更改为目标 x86。

## <a name="test-the-code-and-compare-the-results"></a>测试代码和比较结果

将 DLL 结构化为 Python 扩展后，便可从 Python 项目引用它们，导入模块，并使用其方法。

### <a name="make-the-dll-available-to-python"></a>使 DLL 可供 Python 使用

可通过两种方法使 DLL 可供 Python 使用。

如果 Python 项目和 C++ 项目在相同的解决方案中，则使用第一种方法。 转到“解决方案资源管理器”，右键单击 Python 项目中的“引用”节点，然后选择“添加引用”。 在随即出现的对话框中，选择“项目”选项卡，同时选择“superfastcode”和“superfastcode2”项目，然后选择“确定”。

![添加对 superfastcode 项目的引用](media/cpp-add-reference.png)

另一种方法，如以下步骤所述，在全局 Python 环境中安装模块，使其也可供其他 Python 项目使用。 （执行此操作通常需要在 Visual Studio 2017 版本 15.5 和更早版本中刷新该环境的 IntelliSense 完成数据库。 从环境中删除模块时也必须执行刷新。）

1. 如果使用的是 Visual Studio 2017 或更高版本，请运行 Visual Studio 安装程序，选择“修改”，然后选择“单个组件” > “编译器、生成工具和运行时” > “Visual C++ 2015.3 v140 工具集”。 此步骤是必需的，因为 Python（适用于 Windows）本身是使用 Visual Studio 2015（版本 14.0）生成的，并期望通过此处所述的方法生成扩展时能够使用这些工具。 （请注意，可能需要安装 32 位版本的 Python，并将 DLL 定向到 Win32 而不是 x64。）

1. 右键单击 C++ 项目，然后选择“添加” > “新建项”，在项目中创建名为 setup.py 的文件。 然后选择“C++ 文件 (.cpp)”并命名为 `setup.py`，再选择“确定”（尽管使用了 C++ 文件模板，但使用 .py 扩展命名文件可让 Visual Studio 将其识别为 Python）。 编辑器中出现该文件时，以适合扩展方法的形式将以下代码粘贴到其中：

    CPython 扩展（superfastcode 项目）：

    ```python
    from distutils.core import setup, Extension, DEBUG

    sfc_module = Extension('superfastcode', sources = ['module.cpp'])

    setup(name = 'superfastcode', version = '1.0',
        description = 'Python Package with superfastcode C++ extension',
        ext_modules = [sfc_module]
        )
    ```

    请参阅 [Building C and C++ Extentions](https://docs.python.org/3/extending/building.html)（生成 C 和 C++ 扩展）(python.org)，获取此脚本相关文档。

    PyBind11（superfastcode2 项目）：

    ```python
    import os, sys

    from distutils.core import setup, Extension
    from distutils import sysconfig

    cpp_args = ['-std=c++11', '-stdlib=libc++', '-mmacosx-version-min=10.7']

    sfc_module = Extension(
        'superfastcode2', sources = ['module.cpp'],
        include_dirs=['pybind11/include'],
        language='c++',
        extra_compile_args = cpp_args,
        )

    setup(
        name = 'superfastcode2',
        version = '1.0',
        description = 'Python package with superfastcode2 C++ extension (PyBind11)',
        ext_modules = [sfc_module],
    )
    ```

1. setup.py 代码指示 Python 通过命令行使用 Visual Studio 2015 C++ 工具集生成扩展。 打开提升的命令提示符，导航到包含 C++ 项目（即，包含 setup.py 的文件夹），然后输入以下命令：

    ```command
    pip install .
    ```

    或：

    ```command
    py -m pip install .
    ```

### <a name="call-the-dll-from-python"></a>从 Python 调用 DLL

如上一节所述，使 DLL 可用于 Python 之后，现在可以从 Python 代码中调用 `superfastcode.fast_tanh` 和 `superfastcode2.fast_tanh2` 函数，并将它们的性能与 Python 实现进行比较：

1. 在 .py 文件中添加以下行，调用从 DLL 中导出的方法并显示其输出：

    ```python
    from superfastcode import fast_tanh
    test(lambda d: [fast_tanh(x) for x in d], '[fast_tanh(x) for x in d] (CPython C++ extension)')

    from superfastcode2 import fast_tanh2
    test(lambda d: [fast_tanh2(x) for x in d], '[fast_tanh2(x) for x in d] (PyBind11 C++ extension)')
    ```

1. 运行 Python 程序（“调试” > “启动而不调试”或按 Ctrl+F5），观察到 C++ 例程的运行速度约比 Python 实现快 5 到 20 倍。 典型输出形式如下：

    ```output
    Running benchmarks with COUNT = 500000
    [tanh(x) for x in d] (Python implementation) took 0.758 seconds

    [fast_tanh(x) for x in d] (CPython C++ extension) took 0.076 seconds

    [fast_tanh2(x) for x in d] (PyBind11 C++ extension) took 0.204 seconds
    ```

    如果已禁用“启动而不调试”命令，请右键单击“解决方案资源管理器”中的 Python 项目，选择“设为启动项目”。

1. 尝试增加 `COUNT` 变量，让差异变得更明显。 C++ 模块调试版本的运行速度慢于发布版本的运行速度，因为调试版本优化程度较低，并包含各种错误检查。 请随意在这些配置之间切换，以便比较。

> [!NOTE]
> 在输出中，可以看到尽管 PyBind11 扩展仍然明显快于直接 Python 实现，但其速度不如 CPython 扩展。 这种差异是由于 PyBind11 引入了少量的单调用开销，使其 C++ 接口变得更加简单。 实际上，这种单调用差异可以忽略不计：因为测试代码调用扩展函数 500,000 次，所以此处显示的结果大大放大了开销！ 通常，C++ 函数比此处使用的普通 `fast_tanh[2]` 方法执行的工作更多，在这种情况下，开销并不重要。 但是，如果实现的方法每秒可能会被调用数千次，则使用 CPython 方法可以获得比 PyBind11 更佳的性能。

## <a name="debug-the-c-code"></a>调试 C++ 代码

Visual Studio 支持一起调试 Python 和 C++ 代码。 本节演示了使用 superfastcode 项目的整个过程；superfastcode2 项目的步骤与此相同。

1. 在“解决方案资源管理器”中，右键单击 Python 项目，依次选择“属性”、“调试”选项卡，然后选择“调试” > “启用本机代码调试”选项。

    > [!Tip]
    > 启用本机代码调试后，Python 输出窗口可能在程序完成后立即消失，而不出现通常的“按任何键以继续”暂停界面。 若要强制暂停，请在启用本机代码调试后，向“调试”选项卡上的“运行” > “解释器参数”字段添加 `-i` 选项。 此参数会在代码完成后将 Python 解释器置于交互模式，此时它等待用户按 Ctrl+Z > Enter 退出。 （或者，如果不介意修改 Python 代码，则可在程序结束时添加 `import os` 和 `os.system("pause")` 语句。 此代码会复制初始的暂停提示符。）

1. 选择“文件” > “保存”以保存属性更改。

1. 在 Visual Studio 工具栏中，将生成配置设置为“调试”。

    ![将生成配置设置为“调试”](media/cpp-set-debug.png)

1. 由于代码在调试器中运行时通常需要更长时间，可能需要将 .py 文件中的 `COUNT` 变量更改为小五倍的值（例如，从 `500000` 更改为 `100000`）。

1. 在 C++ 代码中，在 `tanh_impl` 方法内的第一行设置一个断点，然后启动调试器（F5 或“调试” > “开始调试”）。 调用该代码时，调试器将会停止。 如果未命中断点，请检查配置是否设置为“调试”以及是否已保存项目（启动调试器时，不会自动执行该操作）。

    ![在 C++ 代码中的断点处停止](media/cpp-debugging.png)

1. 此时，可浏览 C++ 代码、检查变量等。 这些功能在[一起调试 C++ 和 Python](debugging-mixed-mode-c-cpp-python-in-visual-studio.md) 中有详细介绍。

## <a name="alternative-approaches"></a>替代方法

下表描述了创建 Python 扩展的各种方法。 CPython 和 PyBind11 的前两项已在本文中讨论过。

| 方法 | 年份 | 代表用户 | 优点 | 缺点 |
| --- | --- | --- | --- | --- |
| 适用于 CPython 的 C/C++ 扩展模块 | 1991 | 标准库 | [丰富的文档和教程](https://docs.python.org/3/c-api/)。 完全控制。 | 编译、可移植性、引用管理。 扎实的 C 知识。 |
| [PyBind11](https://github.com/pybind/pybind11)（推荐用于 C++） | 2015 |  | 用于创建现有 C++ 代码的 Python 绑定的轻量型纯标头库。 依赖项少。 兼容 PyPy。 | 较新，不够成熟。 需使用大量 C++11 功能。 支持的编译器较少（包含 Visual Studio）。 |
| Cython（推荐用于 C） | 2007 | [gevent](https://www.gevent.org/)、[kivy](https://kivy.org/) | 类似于 Python。 非常成熟。 高性能。 | 编译、新语法、新工具链。 |
| [Boost.Python](https://www.boost.org/doc/libs/1_66_0/libs/python/doc/html/index.html) | 2002 | | 几乎可与任何 C++ 编译器一起使用。 | 库套件较大且复杂；包含旧编译器的许多解决方法。 |
| ctype | 2003 | [oscrypto](https://github.com/wbond/oscrypto) | 无编译，广泛可用性。 | 访问和转变 C 结构的过程比较繁琐且容易出错。 |
| SWIG | 1996 | [crfsuite](http://www.chokkan.org/software/crfsuite/) | 针对多种语言立即生成绑定。 | 如果 Python 是唯一目标，则开销过大。 |
| cffi | 2013 | [cryptography](https://cryptography.io/en/latest/)、[pypy](https://pypy.org/) | 易于集成，与 PyPy 兼容。 | 较新，不够成熟。 |
| [cppyy](https://cppyy.readthedocs.io/en/latest/) | 2017 | | 类似于使用 C++ 的 cffi。 | 较新，与 VS 2017 有一些兼容性问题。 |

## <a name="see-also"></a>请参阅

要获取本演练的完整示例，请访问 [python-samples-vs-cpp-extension](https://github.com/Microsoft/python-sample-vs-cpp-extension) (GitHub)。
