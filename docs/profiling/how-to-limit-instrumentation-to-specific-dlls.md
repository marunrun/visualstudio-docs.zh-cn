---
title: 如何：将检测限定为特定 DLL | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- performance tools, runtime profiling control window
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b39689219b113343162aa0e814cfa68e2422f08d
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62980910"
---
# <a name="how-to-limit-instrumentation-to-specific-dlls"></a>如何：将检测限定为特定 DLL

通过使用检测分析方法，可以将分析数据的收集限定为应用程序中的一个或多个 DLL。 若要分析应用程序中的一个或多个 DLL，请创建一个将 .dll 文件作为目标包含在内的性能会话。 可以将要分析的 DLL 指定为 Visual Studio 解决方案中的项目或独立的二进制文件。

## <a name="to-limit-instrumentation-to-specific-dlls-in-a-visual-studio-solution"></a>将检测限定为 Visual Studio 解决方案中的特定 DLL

1. 在 Visual Studio 中打开包含该 DLL 的解决方案。

2. 在“分析”菜单上，选择“启动性能向导”。

3. 选择“检测”作为分析方法，然后单击“下一步”。

4. 从“要分析以下哪些可用目标?”中，选择 .dll 项目的名称，然后单击“下一步”。

5. 单击“完成”退出向导，将在“性能资源管理器”窗口中显示新的性能会话。

6. 右键单击“目标”，然后选择“添加目标项目”。

7. 在“添加目标项目”列表中，选择执行 DLL 时要使用的可执行项目。

     可选。 可以添加任何要分析的 DLL 项目。

8. 若要防止对某个已添加的项目进行数据收集，请右键单击该项目的名称，然后清除“检测”复选框。

## <a name="to-specify-specific-dlls-to-profile-as-independent-binaries"></a>将要分析的特定 DLL 指定为独立的二进制文件

1. 打开 Visual Studio。

2. 在“分析”菜单上，选择“启动性能向导”。

3. 在“要分析以下哪些可用目标?”中，选择“分析动态链接库(.DLL)”，然后单击“下一步”。

4. 在该向导的第二页上，执行下列步骤：

    - 在“DLL 路径”中键入要分析的 .dll 文件的路径和文件名。 还可以单击省略号按钮 (...) 在“要分析的动态链接库”对话框中查找该文件。 请注意，必须指定接下来将选择的可执行 (.exe) 文件将启动的 .dll 文件的副本。

    - 在“可执行文件路径”中键入将执行该 .dll 的可执行 (.exe) 文件的路径和文件名。 还可以单击省略号按钮 (...) 在“要启动的可执行文件”对话框中查找该文件。

    - 可选。 在“命令行参数”中键入要传递给可执行文件的任何命令行参数。 如有必要，请在“工作目录”中指定应用程序的工作目录。

    - 单击 **“下一步”**。

5. 选择“检测”作为分析方法，然后单击“下一步”。

6. 单击“完成”退出向导，将在“性能资源管理器”窗口中显示新的性能会话。

7. 可选。 若要添加更多 .dll 文件，请右键单击“目标”，然后选择“添加目标二进制文件”。 在“添加目标二进制文件”对话框中选择这些文件。

    > [!NOTE]
    > 请勿指定执行 DLL 的可执行 (.exe) 文件。

## <a name="see-also"></a>请参阅

[控制数据收集](../profiling/controlling-data-collection.md)
[如何：将检测限定为特定函数](../profiling/how-to-limit-instrumentation-to-specific-functions.md)