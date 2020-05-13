---
title: 如何：指定检测前和检测后命令 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.performance.property.instrument
helpviewer_keywords:
- profiling tools, pre-instrument events
- events [Visual Studio], pre-instrument
- pre-instrument events, performance tools
ms.assetid: 6a8d5340-1d1b-4d81-88dd-8e1f435eb828
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 22ad5558ed01e5bb1b8d12b7a4cc65b4d677d0cd
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "74778708"
---
# <a name="how-to-specify-pre--and-post-instrument-commands"></a>如何：指定检测前和检测后命令

可以指定在检测性能会话中的二进制文件之前或之后运行的命令。 任何可以从命令行发出的命令都可以指定为检测前或检测后事件。 例如，可以指定一些命令，这些命令会在检测完二进制文件后，自动使用所执行的批处理文件中的强名称密钥重新签名程序集。

可以为分析运行期间的所有受检测二进制文件或单个二进制文件指定命令。 但是，可以仅指定一个检测前命令以在检测过程前运行，并仅指定一个检测后命令以在检测过程后运行。 无法同时为所有二进制文件和单个二进制文件指定命令。 为所有二进制文件指定命令时，这些命令在检测会话中的每个二进制文件之前或之后运行。

执行命令时所在的工作目录取决于正运行 [!INCLUDE[vs_current_short](../code-quality/includes/vs_current_short_md.md)] 的操作系统以及所分析应用程序的目标平台。

若要获取分析工具的路径，请参阅[指定命令行工具的路径](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md)。

## <a name="to-specify-pre-instrument-commands"></a>指定检测前命令

1. 执行以下步骤之一：

    - 若要为性能会话中的所有二进制文件指定检测前命令，请在“性能资源管理器”中选择性能会话节点，然后右键单击并选择“属性”   。

    - 若要为某个特定的二进制文件指定检测前命令，请在性能会话的“目标”列表中右键单击该二进制文件的名称，然后选择“属性”   。

2. 在“属性页”中，单击“检测”   。

3. 在“检测前事件”下的“命令行”文本框中键入命令   。

    > [!NOTE]
    > 可以单击“命令行”  框旁边的省略号按钮“(…)”  浏览到相应的 .exe、.cmd 或 .bat 文件并选择该文件。

4. 单击 **“确定”** 。

     若要禁止命令运行但不删除它，请选中“从检测中排除”复选框  。 若要修改编译器或链接器设置，请使用项目属性页。

## <a name="to-specify-post-instrument-commands"></a>指定检测后命令

1. 执行以下步骤之一：

    - 若要为性能会话中的所有二进制文件指定检测后命令，请在“性能资源管理器”中选择性能会话节点，然后右键单击并选择“属性”   。

    - 若要为某个特定的二进制文件指定检测后命令，请在性能会话的“目标”列表中右键单击该二进制文件的名称，然后选择“属性”   。

2. 在“属性页”中，单击“检测”   。

3. 在“检测后事件”下的“命令行”文本框中键入命令   。

    > [!NOTE]
    > 可以单击“命令行”  框旁边的省略号按钮“(…)”  浏览到相应的 .exe、.cmd 或 .bat 文件并选择该文件。

4. 单击 **“确定”** 。

     若要禁止命令运行但不删除它，请选中“从检测中排除”复选框  。 若要修改编译器或链接器设置，请使用项目属性页。

## <a name="see-also"></a>另请参阅

[配置性能会话](../profiling/configuring-performance-sessions.md)
