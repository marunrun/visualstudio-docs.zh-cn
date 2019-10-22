---
title: C++调试配置的项目设置
ms.custom: seodec18
ms.date: 11/26/2018
ms.topic: reference
f1_keywords:
- VC.Project.VCDebugSettings.WebBrowser.DebuggerType
- VC.Project.IVCGPUDebugPageObject.EnvironmentMerge
- VC.Project.VCDebugSettings.SymbolPath
- VC.Project.IVCClusterDebugPageObject.ApplicationCommand
- VC.Project.IVCRemoteDebugPageObject.WorkingDirectory
- VC.Project.VCDebugSettings.DebuggerType
- VC.Project.IVCLocalDebugPageObject.GPUDebuggerTargetType
- VC.Project.IVCRemoteDebugPageObject.SQLDebugging
- VC.Project.IVCRemoteDebugPageObject.Remote
- VC.Project.IVCGPUDebugPageObject.CommandArguments
- VC.Project.VCDebugSettings.CommandArguments
- VC.Project.IVCClusterDebugPageObject.MPIRunWorkingDirectory
- VC.Project.IVCLocalDebugPageObject.SQLDebugging
- VC.Project.IVCWebSvcDebugPageObject.HttpUrl
- VC.Project.IVCLocalDebugPageObject.WorkingDirectory
- VC.Project.IVCLocalDebugPageObject.CommandArguments
- VC.Project.IVCClusterDebugPageObject.MPIRunCommand
- VC.Project.IVCGPUDebugPageObject.WorkingDirectory
- VC.Project.IVCWebSvcDebugPageObject.DebuggerType
- VC.Project.IVCRemoteDebugPageObject.CommandArguments
- VC.Project.IVCRemoteDebugPageObject.DebuggerType
- VC.Project.IVCLocalDebugPageObject.GPUBreakOnAllThreads
- VC.Project.IVCRemoteDebugPageObject.RemoteMachine
- VC.Project.IVCClusterDebugPageObject.MPIRunArguments
- VC.Project.IVCClusterDebugPageObject.MPIAcceptFilter
- VC.Project.IVCGPUDebugPageObject.RemoteConnection
- VC.Project.VCDebugSettings.PDBPath
- VC.Project.IVCRemoteDebugPageObject.DeploymentDirectory
- VC.Project.VCDebugSettings.SQLDebugging
- VC.Project.VCDebugSettings.RemoteCommand
- VC.Project.IVCClusterDebugPageObject.ShimCommand
- VC.Project.IVCLocalDebugPageObject.Command
- VC.Project.IVCRemoteDebugPageObject.GPUBreakOnAllThreads
- VC.Project.IVCLocalDebugPageObject.Attach
- VC.Project.VCDebugSettings.Command
- VC.Project.IVCRemoteDebugPageObject.GPUDebuggerTargetType
- VC.Project.IVCRemoteDebugPageObject.RemoteCommand
- VC.Project.IVCClusterDebugPageObject.ApplicationArguments
- VC.Project.IVCLocalDebugPageObject.Environment
- VC.Project.IVCGPUDebugPageObject.DeploymentDirectory
- VC.Project.IVCLocalDebugPageObject.EnvironmentMerge
- VC.Project.VCDebugSettings.Environment
- VC.Project.IVCGPUDebugPageObject.BreakpointBehavior
- VC.Project.IVCLocalDebugPageObject.DebuggerType
- VC.Project.VCDebugSettings.WebBrowser.WebBrowserDebuggerHttpUrl
- VC.Project.IVCWebSvcDebugPageObject.SQLDebugging
- VC.Project.IVCGPUDebugPageObject.AcceleratorType
- VC.Project.IVCGPUDebugPageObject.Environment
- VC.Project.VCDebugSettings.RemoteMachine
- VC.Project.IVCGPUDebugPageObject.AdditionalFilesToDeploy
- VC.Project.VCDebugSettings.WorkingDirectory
- vs.debug.builds
- VC.Project.VCDebugSettings.Attach
- VC.Project.VCDebugSettings.HttpUrl
- VC.Project.IVCClusterDebugPageObject.MPIAcceptMode
- VC.Project.IVCGPUDebugPageObject.Attach
- VC.Project.IVCRemoteDebugPageObject.AdditionalFiles
- VC.Project.IVCGPUDebugPageObject.Command
- VC.Project.VCDebugSettings.Remote
- VC.Project.IVCRemoteDebugPageObject.Attach
- VC.Project.VCDebugSettings.EnvironmentMerge
- VC.Project.IVCGPUDebugPageObject.MachineName
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- DEBUG linker option
- -PDB linker option
- -Zl compiler option [C++]
- /DEBUG linker option
- /PDBSTRIPPED linker option
- /MAPINFO linker option
- -Zd compiler option [C++]
- -DEBUG linker option
- MAPINFO linker option
- /ZI compiler option [C++]
- ZI compiler option [C++]
- Z7 compiler option [C++]
- debugging [C++], debugger settings
- project settings [Visual Studio], debug configurations
- mapfiles, project settings
- debug configurations, C++
- project settings [Visual Studio]
- /PDB linker option
- -PDBSTRIPPED linker option
- debug builds, project settings
- PDB linker option
- projects [Visual Studio], debug configurations
- project configurations, debug
- Zd compiler option [C++]
- MAP linker option
- /Z7 compiler option [C++]
- .pdb files, debug build project settings
- -MAP linker option
- -MAPINFO linker option
- /Zd compiler option [C++]
- PDBSTRIPPED linker option
- -Z7 compiler option [C++]
- pdb files, debug build project settings
- /MAP linker option
ms.assetid: 860c7f13-a108-4fe5-8fca-d235cd3ca1cb
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- cplusplus
ms.openlocfilehash: bca39b97f6363d8b8fefcfd691b69baf85c32170
ms.sourcegitcommit: 485ffaedb1ade71490f11cf05962add1718945cc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/16/2019
ms.locfileid: "72450377"
---
# <a name="project-settings-for-a-c-debug-configuration"></a>C++ 调试配置的项目设置
可以在 "**属性页**" 对话框中更改 C C++或 debug 配置的项目设置，如[如何：设置调试和发布配置](../debugger/how-to-set-debug-and-release-configurations.md)中所述。 下表显示“属性页”对话框中与调试器有关的设置的位置。

> [!NOTE]
> 对于 UWP 应用和用编写的组件，"**配置属性/调试**" 类别中的 "调试" 项目设置C++是不同的。 请参阅[启动调试会话（VB、 C# C++和 XAML）](../debugger/start-a-debugging-session-for-a-store-app-in-visual-studio-vb-csharp-cpp-and-xaml.md)。

 保存解决方案时，每个调试属性设置都会自动写入并保存到解决方案的 "每用户" 文件（. .vcxproj）。

 按照下表中所述，在要**启动的调试器**列表框中指定要使用的调试器。 您的选择将影响属性的可见性。

## <a name="configuration-properties-folder-debugging-category"></a>“配置属性”文件夹（“调试”类别）

| **设置** | **描述** |
| - | - |
| **要启动的调试器** | 指定要运行的调试器，有以下选择：<br /><br /> -   本地 Windows 调试器<br />-   远程 Windows 调试器<br />-   Web 浏览器调试器<br />-   Web 服务调试器 |
| **命令**（本地 Windows 调试器） | 指定在本地计算机上用于启动要调试程序的命令。 |
| **远程命令**（远程 Windows 调试器） | 远程计算机上的 .exe 的路径。 可以像在远程计算机上一样输入路径。 |
| **命令参数**（本地 Windows 调试器）<br /><br /> **远程命令参数**（远程 Windows 调试器） | -   为前面指定的命令指定自变量。<br /><br /> 可以在此框中使用下列重定向运算符：<br /><br /> < `file`<br /> 从文件中读取 stdin。<br /><br /> > `file`<br /> 将 stdout 写入文件。<br /><br /> >> `file`<br /> 将 stdout 追加到文件中。<br /><br /> 2> `file`<br /> 将 stderr 写入文件。<br /><br /> 2>> `file`<br /> 将 stderr 追加到文件中。<br /><br /> 2> &1<br /> 将 stderr (2) 输出发送到与 stdout (1) 相同的位置。<br /><br /> 1> &2<br /> 将 stdout (1) 输出发送到与 stderr (2) 相同的位置。<br /><br /> 在大多数情况下，这些运算符仅适用于控制台应用程序。 |
| **工作目录** | 指定要调试的程序的工作目录（相对于 EXE 所在的项目目录）。 如果将此设置保留为空，则工作目录将为项目目录。 对于远程调试，项目目录位于远程服务器上。 |
| **附加**（本地 Windows 调试器和远程 Windows 调试器） | 指定是启动应用程序还是附加到应用程序。 默认设置为“否”。 |
| **远程服务器名称**（远程 Windows 调试器） | 指定您要在其上调试应用程序的计算机（不是您的计算机）的名称。<br /><br /> RemoteMachine 生成宏被设置为此属性的值；有关详细信息，请参阅[用于生成命令和属性的宏](/cpp/build/reference/common-macros-for-build-commands-and-properties)。 |
| **连接**（远程 Windows 调试器） | 允许您在远程调试的标准与非身份验证连接类型之间切换。 在“远程服务器名称”框中指定远程计算机的名称。 连接类型包括：<br /><br /> -   带 Windows 身份验证的远程访问<br />-   不带身份验证的远程访问<br /><br /> 注意：不带身份验证的远程调试可能会使远程计算机容易受到安全侵犯。 Windows 身份验证模式更安全。<br /><br /> 有关详细信息，请参阅[远程调试安装](../debugger/remote-debugging.md)。 |
| **HTTP URL**（Web 服务调试器和 Web 浏览器调试器） | 指定您要调试的项目所在的 URL。 |
| 调试器类型 | 指定要使用的调试器类型：“仅限本机”、“仅限托管”、“仅限 GPU”、“混合”、“自动”（默认）或“脚本”。<br /><br /> -   “仅限本机”用于非托管 C++ 代码。<br />-   “仅限托管”适用于在公共语言运行时下运行的代码（托管代码）。<br />-   “混合”对托管代码和非托管代码都调用调试器。<br />-   “自动”将根据编译器和 EXE 信息确定调试器类型。<br />-   “脚本”调用脚本调试器。<br />-   “仅限 GPU”用于在 GPU 设备或 DirectX 参考光栅器上运行的 C++ AMP 代码。 请参阅[调试 GPU 代码](../debugger/debugging-gpu-code.md)。 |
| **环境**（本地 windows 调试器和远程 Windows 调试器） | 为要调试的程序指定环境变量。 使用标准环境变量语法（例如 `PATH="%SystemRoot%\..."`）。 根据“合并环境”设置的不同，这些变量将重写系统环境或与系统环境合并。 在 "设置" 列中左键单击时，将出现 "编辑 ..."上去. 选择该链接可编辑环境变量。 |
| **合并环境**（本地 Windows 调试器） | 确定在“环境”框中指定的变量是否与操作系统定义的环境合并。 默认设置为“是”。 |
| **SQL 调试**（除 MPI 群集调试器外的所有调试器） | 启用 [!INCLUDE[vcprvc](../code-quality/includes/vcprvc_md.md)] 应用程序中的 SQL 过程的调试。 默认设置为“否”。 |
| **调试加速器类型**（仅限 GPU 调试） | 指定要用于调试的 GPU 设备。 为兼容的 GPU 设备安装设备驱动器将添加其他选项。 默认设置为“GPU - 软件仿真程序”。 |
| **GPU 默认断点行为**（仅限 GPU 调试） | 指定是否应为 SIMD 经线中的每个线程引发断点事件。 默认设置是仅每次换行引发一次断点事件。 |
| **Amp 默认快捷键** | 在调试 GPU 代码时，指定默认 AMP 快捷键。 如果问题是由硬件或驱动程序导致，而非你的代码导致，请选择“WARP 软件快捷键”进行调查。 |
| **部署目录**（远程 Windows 调试器） | 指定项目输出在启动前要被复制的远程计算机上的路径。 路径可以是远程计算机上的网络共享，也可以是到远程计算机上的文件夹的路径。 默认设置为空，这意味着项目输出未复制到网络共享。 若要启用文件的部署，还必须在“配置管理器”对话框中选中“部署”复选框。 有关详细信息，请参阅[如何：创建和编辑配置](../ide/how-to-create-and-edit-configurations.md)。 |
| **其他要部署的文件**（远程 Windows 调试器） | 如果设置了 "部署目录" 属性，则这是要复制到部署目录的附加文件的分号分隔列表。 默认设置为空，这意味着不会将其他文件复制到部署目录中。 若要启用文件的部署，还必须在“配置管理器”对话框中选中“部署”复选框。 有关详细信息，请参阅[如何：创建和编辑配置](../ide/how-to-create-and-edit-configurations.md)。 |
| **部署 Visual C++ 调试运行库**（远程 Windows 调试器） | 如果“部署目录”属性已设置，则它可以指定当前平台的 Visual C++ 调试运行库是否应被复制到网络共享中。 默认设置为“是”。 |

## <a name="cc-folder-general-category"></a>“C/C++”文件夹（“常规”类别）

|设置|描述|
|-------------|-----------------|
|**调试信息格式**([/Z7、/Zd、/Zi、/ZI](/cpp/build/reference/z7-zi-zi-debug-information-format))|指定要为项目创建的调试信息类型。<br /><br /> 默认选项 (/ZI) 以“编辑并继续”的兼容格式创建程序数据库 (PDB)。 有关详细信息，请参阅 [/Z7、/Zd、/Zi、/ZI（调试信息格式）](/cpp/build/reference/z7-zi-zi-debug-information-format)。|

## <a name="cc-folder-optimization-category"></a>“C/C++”文件夹（“优化”类别）

|设置|描述|
|-------------|-----------------|
|**优化**|指定编译器是否应优化其生成的代码。 优化过程将更改执行的代码。 优化的代码不再与源代码匹配，这使得调试变得更加困难。<br /><br /> 默认选项（“禁用(/0d)”）取消优化。 你可以在开发时取消优化，然后在创建代码的产品版本时再启用优化。|

## <a name="linker-folder-debugging-category"></a>“链接器”文件夹（“调试”类别）

|设置|描述|
|-------------|-----------------|
|**生成调试信息** ([/DEBUG](/cpp/build/reference/debug-generate-debug-info))|通知链接器包含调试信息，这些信息具有 [/Z7、/Zd、/Zi 或 /ZI](/cpp/build/reference/z7-zi-zi-debug-information-format) 指定的格式。|
|**生成程序数据库文件** ([/PDB:name](/cpp/build/reference/pdb-use-program-database))|在此框中指定程序数据库（PDB）文件的名称。 必须为“调试信息格式”选择 /ZI 或 /Zi。|
|**去除私有符号** ([/PDBSTRIPPED:filename](/cpp/build/reference/pdbstripped-strip-private-symbols))|如果不希望在 PDB 文件中包含私有符号，则在该框中指定 PDB 文件的名称。 使用生成 PDB 文件的编译器或链接器选项（如/DEBUG、/Z7、/Zd.）生成程序映像时，此选项会创建第二个 PDB 文件。 或 /Zi。 此 PDB 文件省略您不希望交付给客户的符号。 有关详细信息，请参阅 [/PDBSTRIPPED（去除私有符号）](/cpp/build/reference/pdbstripped-strip-private-symbols)。|
|**生成映射文件** ([/MAP](/cpp/build/reference/map-generate-mapfile))|通知链接器在链接过程中生成映射文件。 默认设置为“否”。 有关详细信息，请参阅 [/MAP（生成映射文件）](/cpp/build/reference/map-generate-mapfile)。|
|**映射文件名**（[/MAP：](/cpp/build/reference/map-generate-mapfile)*name*）|如果选择“生成映射文件”，则可在该框中指定映射文件。 有关详细信息，请参阅 [/MAP（生成映射文件）](/cpp/build/reference/map-generate-mapfile)。|
|**映射导出** ([/MAPINFO:EXPORTS](/cpp/build/reference/mapinfo-include-information-in-mapfile))|在映射文件中包含导出函数。 默认设置为“否”。 有关详细信息，请参阅[/MAPINFO （在映射中包含信息）](/cpp/build/reference/mapinfo-include-information-in-mapfile)。|
|**可调试程序集** ([/ASSEMBLYDEBUG](/cpp/build/reference/mapinfo-include-information-in-mapfile))|为链接器 /ASSEMBLYDEBUG 选项指定设置。 可能的值有：<br /><br /> -   未发送可调试属性。<br />-   运行时跟踪和禁用优化 (/ASSEMBLYDEBUG)。 此设置为默认设置。<br />-   无运行时跟踪和启用优化 (/ASSEMBLYDEBUG:DISABLE)。<br />-   \<从父级或项目默认设置继承>。<br />有关详细信息，请参阅 [/ASSEMBLYDEBUG（添加 DebuggableAttribute）](/cpp/build/reference/assemblydebug-add-debuggableattribute)。|

 通过使用 Microsoft.VisualStudio.VCProjectEngine.VCDebugSettings 接口，可以在“配置属性”文件夹（“调试”类别）中以编程方式更改这些设置。 有关更多信息，请参见<xref:Microsoft.VisualStudio.VCProjectEngine.VCDebugSettings>。

## <a name="other-project-settings"></a>其他项目设置

若要调试静态库和 Dll 等项目类型，Visual Studio 项目必须能够找到正确的文件。 当源代码可用时，可以将静态库和 Dll 作为单独的项目添加到同一个解决方案中，以便更轻松地进行调试。 有关创建这些项目类型的信息，请参阅[创建和使用动态链接库（DLL）](/cpp/build/walkthrough-creating-and-using-a-dynamic-link-library-cpp)和[使用静态库创建](/cpp/windows/walkthrough-creating-and-using-a-static-library-cpp)。 使用可用的源代码，你还可以通过**从现有代码中**选择 "**文件**"  > **新建** >  项目来创建新的 Visual Studio 项目。

若要调试项目外部的 Dll，请参阅[调试 dll 项目](../debugger/debugging-dll-projects.md#vxtskdebuggingdllprojectsexternal)。 如果需要调试自己的 DLL 项目，但不能访问调用应用程序的项目，请参阅[如何从 DLL 项目中进行调试](../debugger/how-to-debug-from-a-dll-project.md)。

## <a name="see-also"></a>请参阅
- [调试本机代码](../debugger/debugging-native-code.md)
- [调试器设置和准备](../debugger/debugger-settings-and-preparation.md)
- [创建和管理C++项目](/cpp/ide/creating-and-managing-visual-cpp-projects)
- [/ASSEMBLYDEBUG（添加 DebuggableAttribute）](/cpp/build/reference/assemblydebug-add-debuggableattribute)
- [用于生成命令和属性的常用宏](/cpp/ide/common-macros-for-build-commands-and-properties)