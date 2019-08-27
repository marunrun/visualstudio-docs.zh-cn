---
title: 针对 HPC（高性能计算）群集进行分析 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.performance.hpc.wizard.exeoptions
- vs.performance.hpc.wizard.summary
- vs.performance.hpc.wizard.startoptions
- vs.performance.hpc.wizard.intro
- vs.performance.hpc.property.basic
- vs.performance.hpc.wizard.application
- vs.performance.hpc.wizard.clusteroptions
- vs.performance.hpc.property.advanced
helpviewer_keywords:
- profililng tools,HPC
- HPC profiling
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 38cde5c1500168dcb36021c530799d1d8d1effb9
ms.sourcegitcommit: 12f2851c8c9bd36a6ab00bf90a020c620b364076
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/06/2019
ms.locfileid: "66745320"
---
# <a name="profile-on-hpc-high-performance-computing-clusters"></a>对 HPC（高性能计算）群集进行分析

可以使用 Visual Studio 分析工具的采样方法对 Microsoft Windows HPC 群集的计算节点进行分析。 有关 HPC 的详细信息，请参阅 Microsoft 网站上的 [Windows HPC](https://azure.microsoft.com/solutions/big-compute/)。

## <a name="prerequisites"></a>系统必备

若要对 HPC 计算节点进行分析，必须执行以下操作：

- 在与 Visual Studio 相同的计算机上安装 Microsoft HPC Pack 2008。 计算机不必是 HPC 群集的一部分。 可以在 [Microsoft 下载中心](http://go.microsoft.com/fwlink/?LinkID=177414)安装 HPC 包。

- 在 HPC 计算节点上安装 .NET Framework 4 以及分析工具的独立版本。 .NET Framework 和独立探查器的安装程序都位于 Visual Studio 安装介质上。 注意：安装 .NET Framework 后，必须重启计算机，然后才能安装分析工具  。

  要在活动 HPC 计算节点上安装 .NET Framework 4 和独立分析工具并对群集计算机启用分析，请按照以下步骤操作：

1. 打开随 HPC 包安装的命令提示符窗口。

2. 在单独的命令提示符处输入以下命令：

    1. `clusrun /all /scheduler:` *%HeadNode% %FxPath%* `/q /norestart`

    2. `clusrun /all /scheduler:` *%HeadNode%* `shutdown /r /t 0 /d u:4:2 /c "Microsoft .NET Framework install required restart"`

    3. `clusrun /all /scheduler:` *%HeadNode% %ProfilerPath%* `/q /norestart`

| | |
|------------------| - |
| *%HeadNode%* | 群集的头节点的名称。 |
| *%FxPath%* | .NET Framework 4 安装程序的路径。 在 Visual Studio 安装介质上，路径为：WCU\dotNetFramework\dotNetFx40_Full_x86_x64.exe |
| *%ProfilerPath%* | 分析工具安装程序的独立版本的路径。 在 Visual Studio 安装介质上，路径为：Standalone Profiler\x64\vs_profiler.exe |

## <a name="profile-on-an-hpc-compute-node"></a>对 HPC 计算节点进行分析

可通过使用 HPC 性能向导指定 HPC 群集和目标信息，来配置分析会话。 可以在性能会话属性页中设置其他选项。 分析工具会自动部署所需目标二进制文件并启动探查器和 HPC 应用程序。

1. 在“分析”  菜单上，单击“启动 HPC 性能向导”  。 如果该命令不可用，请确保具有上面列出的先决条件。

2. 在向导的第一页上单击“下一步”  。

3. 在向导的第二页上，选择要分析的应用程序。

   - 若要分析当前在 [!INCLUDE[vs_current_short](../code-quality/includes/vs_current_short_md.md)] 中打开的项目，请选择“一个或多个可用项目”  选项，然后从列表中选择项目名。

   - 若要分析不在打开的项目中的二进制文件，请选择“可执行文件(.EXE 文件)”  选项。

4. 单击 **“下一步”** 。

5. 在向导的第三页上：

    - 如果要分析不在打开的项目中的可执行文件，请在“可执行文件的完整路径是什么”  中指定二进制文件的路径。

    - 如果要分析不在打开的项目中的可执行文件，则可以在“命令行参数”  中指定要传递到进程的任何命令行参数。

    - 在“远程工作目录”  中，指定单个计算节点上由进程实例使用的文件夹的路径。

    - 在“部署位置”  中，指定 HPC 服务器用于为部署暂存映像的目录的路径。

6. 单击 **“下一步”** 。

7. 在向导的第四页上：

    - 在“头节点”  列表中，单击在分析运行中充当 HPC 头节点的计算机。 头节点可以是“localhost”，这使你可以对本地计算机进行分析而无需群集。

    - 在“进程数”  列表中，单击要运行的应用程序的实例数。

    - 从“分析选项”  列表中，选择分析目标。

         若要分析群集中的特定进程，请选择“针对轶分析”  选项，然后从下拉列表中选择进程的秩。

         若要分析在 HPC 群集中的特定节点上运行的进程，请选择“针对节点分析”  选项，然后从下拉列表中选择节点。

8. 单击 **“下一步”** 。

9. 在向导的第五页上，可以选择立即启动探查器和分析进程，或以后使用性能资源管理器启动分析。

    - 选择“在向导完成后启动分析”  立即启动分析，或清除该复选框手动启动分析。

10. 单击 **“完成”** 。

## <a name="set-hpc-profiling-properties-by-using-performance-session-property-pages"></a>使用性能会话属性页设置 HPC 分析属性

可以在性能会话属性页的“HPC 启动属性”页上更改在 HPC 分析向导中设置的性能会话属性。 可在“HPC 高级属性”页上设置其他选项。

### <a name="to-open-the-performance-session-property-pages"></a>打开性能会话属性页

1. 如有必要，请在“性能资源管理器”中打开性能会话 (.psess) 文件。 在“文件”  菜单上，单击“打开”  ，然后找到文件。

2. 在“性能资源管理器”中，右键单击性能会话名，然后单击“属性”  。

3. 若要访问“属性页”对话框，请使用以下方法之一：

    - 单击“常规”  ，然后选中“在 HPC 群集上收集”  以启用 HPC 分析或清除该复选框以禁用 HPC 分析。

    - 单击“HPC 启动属性”  以更改用于启动 HPC 应用程序的属性。

    - 单击“HPC 高级属性”  以设置其他选项

### <a name="hpc-launch-properties"></a>HPC 启动属性

|Property|说明|
|--------------|-----------------|
|**头节点**|指定在分析运行中充当 HPC 头节点的计算机。|
|**进程数**|指定要在分析的应用程序中运行的应用程序实例数。|
|**针对轶分析**|若要分析群集中的特定进程，请选择“针对轶分析”  选项，然后从下拉列表中选择进程的秩。|
|**针对节点分析**|若要分析在 HPC 群集中的特定节点上运行的进程，请选择“针对节点分析”  选项，然后从下拉列表中选择节点。|
|**远程工作目录**|指定单个计算节点上由进程实例使用的文件夹的路径。|
|**部署位置**|指定 HPC 服务器用于为部署暂存映像的目录的路径。|

### <a name="advanced-properties"></a>高级属性

| Property | 说明 |
|---------------------------------------| - |
| **项目名称** | 当前 [!INCLUDE[vs_current_short](../code-quality/includes/vs_current_short_md.md)] 项目或解决方案的名称。 |
| **探查器停止时进行清理** | 为 true 时，删除已部署到执行目录的二进制文件。 在此步骤中不会删除用户程序创建的文件和目录。 如果执行目录和部署目录是由 IDE 创建的，则 IDE 会尝试删除它们，但是如果它们包含不是由 IDE 部署的文件，则 IDE 不会执行此操作。 |
| **其他要部署的文件** | 指定要在计算节点上部署的任何其他文件的分号分隔列表。 可以单击省略号按钮 ( **...** ) 以使用对话框选择多个文件。 |
| **Mpiexec 命令** | 指定启动 MPI 应用程序的应用程序。 默认值为 **mpiexec.exe** |
| **Mpiexec 参数** | 指定要传递到 mpiexec.exe 命令的参数。 |
| **该群集中的所请求的节点** | 指定群集中要在其上运行应用程序的节点数。 |
| **部署 CRT 文件** | 为 true 时，在群集上部署 C/C++ 运行时。 |
| **分析前脚本** | 指定在分析会话启动之前要在本地开发计算机上运行的脚本的路径和文件名。 |
| **分析前脚本参数** | 指定要传递到分析前脚本的参数。 |
| **分析后脚本** | 指定在分析会话结束之后要在本地开发计算机上运行的脚本的路径和文件名。 |
| **分析后脚本参数** | 指定要传递到分析后脚本的参数。 |
