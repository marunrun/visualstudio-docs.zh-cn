---
title: 项目设置为C++调试配置 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
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
- FSharp
- VB
- CSharp
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
caps.latest.revision: 52
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: ca9ff0678ba2c7abafa0d988efa09437ccd27dca
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65687555"
---
# <a name="project-settings-for-a-c-debug-configuration"></a>C++ 调试配置的项目设置
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可以更改 C 或视觉对象的项目设置C++中的调试配置**属性页**对话框中，如中所述[如何：设置调试和发布配置](../debugger/how-to-set-debug-and-release-configurations.md)。 下表显示“属性页”对话框中与调试器有关的设置的位置  。  
  
> [!WARNING]
> 中的调试项目设置**配置属性/调试**类别的 Windows 应用商店应用程序和组件中编写的C++不同。 请参阅[启动调试会话 (VB、 C#，C++和 XAML)](../debugger/start-a-debugging-session-for-a-store-app-in-visual-studio-vb-csharp-cpp-and-xaml.md) Windows 开发中心中。  
  
 指定要在中使用的调试器**要启动的调试器**列表框。 您的选择将影响属性的可见性。  
  
 每当您保存解决方案时，每个调试属性设置均自动写入并保存到解决方案的“每用户”文件 (.vcxproj.user) 中。  
  
### <a name="configuration-properties-folder-debugging-category"></a>“配置属性”文件夹（“调试”类别）  
  
|**设置**|**说明**|  
|-----------------|---------------------|  
|**要启动的调试器**|指定要运行的调试器，有以下选择：<br /><br /> -   本地 Windows 调试器 <br />-   远程 Windows 调试器 <br />-   Web 浏览器调试器 <br />-   Web 服务调试器 |  
|**命令**（本地 Windows 调试器）|指定在本地计算机上用于启动要调试程序的命令。|  
|**远程命令**（远程 Windows 调试器）|远程计算机上的 .exe 的路径。 可以像在远程计算机上一样输入路径。|  
|**命令参数**（本地 Windows 调试器和远程 Windows 调试器）|-   为前面指定的命令指定自变量。<br /><br /> 可以在此框中使用下列重定向运算符：<br /><br /> < `file`<br /> 从文件中读取 stdin。<br /><br /> > `file`<br /> 将 stdout 写入文件。<br /><br /> >> `file`<br /> 将 stdout 追加到文件中。<br /><br /> 2> `file`<br /> 将 stderr 写入文件。<br /><br /> 2>> `file`<br /> 将 stderr 追加到文件中。<br /><br /> 2> &1<br /> 将 stderr (2) 输出发送到与 stdout (1) 相同的位置。<br /><br /> 1> &2<br /> 将 stdout (1) 输出发送到与 stderr (2) 相同的位置。<br /><br /> 在大多数情况下，这些运算符仅适用于控制台应用程序。|  
|**工作目录**|指定要调试的程序的工作目录（相对于 EXE 所在的项目目录）。 如果将此设置保留为空，则工作目录将为项目目录。 对于远程调试，项目目录将位于远程服务器上。|  
|**附加**（本地 Windows 调试器和远程 Windows 调试器）|指定是启动应用程序还是附加到应用程序。 默认设置为“否”。|  
|**远程服务器名称**（远程 Windows 调试器）|指定您要在其上调试应用程序的计算机（不是您的计算机）的名称。<br /><br /> RemoteMachine 生成宏被设置为此属性影响; 的值有关详细信息，请参阅[用于生成命令和属性的宏](https://msdn.microsoft.com/library/239bd708-2ea9-4687-b264-043f1febf98b)。|  
|**连接**（远程 Windows 调试器）|允许您在远程调试的标准与非身份验证连接类型之间切换。 在“远程服务器名称”框中指定远程计算机的名称  。 连接类型包括：<br /><br /> -   带 Windows 身份验证的远程访问 <br />-   **带不进行身份验证 （仅限本机） 的远程访问**<br /><br /> 注意：不带身份验证的远程调试可能会使远程计算机容易受到安全侵犯  。 Windows 身份验证模式更安全。<br /><br /> 有关详细信息，请参阅[远程调试安装](../debugger/remote-debugging.md)。|  
|**HTTP URL**（Web 服务调试器和 Web 浏览器调试器）|指定您要调试的项目所在的 URL。|  
|调试器类型 |指定要使用的调试器类型：**仅限本机**，**仅限托管**，**仅限 GPU**，**混合**，**自动**（默认值），或**脚本**.<br /><br /> -   “仅限本机”用于非托管 C++ 代码  。<br />-   “仅限托管”适用于在公共语言运行时下运行的代码（托管代码）  。<br />-   “混合”对托管代码和非托管代码都调用调试器  。<br />-   “自动”将根据编译器和 EXE 信息确定调试器类型  。<br />-   “脚本”调用脚本调试器  。<br />-   “仅限 GPU”用于在 GPU 设备或 DirectX 参考光栅器上运行的 C++ AMP 代码  。 请参阅[调试 GPU 代码](../debugger/debugging-gpu-code.md)。|  
|**环境**（本地 Windows 调试器）|为要调试的程序指定环境变量。 使用标准环境变量语法 (例如， `PATH="%SystemRoot%\..."`)。 根据“合并环境”设置的不同，这些变量将重写系统环境或与系统环境合并  。 在设置列中单击时，会出现“编辑…”。 单击该链接可编辑环境变量。|  
|**合并环境**（本地 Windows 调试器）|确定在“环境”框中指定的变量是否与操作系统定义的环境合并  。 默认设置为“是”。|  
|**SQL 调试**（除 MPI 群集调试器外的所有调试器）|启用 [!INCLUDE[vcprvc](../includes/vcprvc-md.md)] 应用程序中的 SQL 过程的调试。 默认设置为“否”。|  
|**调试加速器类型**（仅限 GPU 调试）|指定要用于调试的 GPU 设备。 为兼容的 GPU 设备安装设备驱动器将添加其他选项。 默认设置为“GPU - 软件仿真程序”。|  
|**GPU 默认断点行为**（仅限 GPU 调试）|指定是否应为 SIMD 经线中的每个线程引发断点事件。 默认设置是仅每次换行引发一次断点事件。|  
|**Amp 默认快捷键**（仅限 GPU 调试）|在调试 GPU 代码时，指定默认 AMP 快捷键。 如果问题是由硬件或驱动程序导致，而非你的代码导致，请选择“WARP 软件快捷键”进行调查  。|  
|**部署目录**（远程 Windows 调试器）|指定项目输出在启动前要被复制的远程计算机上的路径。 路径可以是远程计算机上的网络共享，也可以是到远程计算机上的文件夹的路径。 默认设置为空，这意味着项目输出未复制到网络共享。 若要启用文件的部署，还必须在“配置管理器”对话框中选中“部署”复选框  。 有关详细信息，请参阅[如何：创建和编辑配置](../ide/how-to-create-and-edit-configurations.md)。|  
|**其他要部署的文件**（远程 Windows 调试器）|如果“部署目录”属性已设置，则它是一个要复制到部署目录中的分号分隔的附加文件列表。 默认设置为空，这意味着不会将其他文件复制到部署目录中。 若要启用文件的部署，还必须在“配置管理器”对话框中选中“部署”复选框  。 有关详细信息，请参阅[如何：创建和编辑配置](../ide/how-to-create-and-edit-configurations.md)。|  
|**部署 Visual C++ 调试运行库**（远程 Windows 调试器）|如果“部署目录”属性已设置，则它可以指定当前平台的 Visual C++ 调试运行库是否应被复制到网络共享中。 默认设置为“是”。|  
  
### <a name="cc-folder-general-category"></a>“C/C++”文件夹（“常规”类别）  
  
|设置|描述|  
|-------------|-----------------|  
|**调试信息格式**([/Z7、/Zd、/Zi、/ZI](https://msdn.microsoft.com/library/ce9fa7e1-0c9b-47e3-98ea-26d1a16257c8))|指定要为项目创建的调试信息类型。<br /><br /> 默认选项 (/ZI) 以“编辑并继续”的兼容格式创建程序数据库 (PDB)。 有关详细信息，请参阅[/Z7、 /Zd、 /Zi、 /ZI （调试信息格式）](https://msdn.microsoft.com/library/ce9fa7e1-0c9b-47e3-98ea-26d1a16257c8)。|  
  
### <a name="cc-folder-optimization-category"></a>“C/C++”文件夹（“优化”类别）  
  
|设置|描述|  
|-------------|-----------------|  
|**优化**|指定编译器是否应优化其生成的代码。 优化过程将更改执行的代码。 优化的代码不再与源代码匹配。 因此，调试将变得非常困难。<br /><br /> 默认选项 (**已禁用 (/ 0d**) 会取消优化。 你可以在开发时取消优化，然后在创建代码的产品版本时再启用优化。|  
  
### <a name="linker-folder-debugging-category"></a>“链接器”文件夹（“调试”类别）  
  
|设置|描述|  
|-------------|-----------------|  
|**生成调试信息** ([/DEBUG](https://msdn.microsoft.com/library/1af389ae-3f8b-4d76-a087-1cdf861e9103))|通知链接器包含调试信息，这些信息具有 /Z7、/Zd、/Zi 或 /ZI 指定的格式。|  
|**生成程序数据库文件** ([/PDB:name](https://msdn.microsoft.com/library/d23db0ce-10cb-427a-bc60-d6b2a852723d))|在该框中指定 PDB 文件的名称。 必须为“调试信息格式”选择 /ZI 或 /Zi。|  
|**去除私有符号** ([/PDBSTRIPPED:filename](https://msdn.microsoft.com/library/9b9e0070-6a13-4142-8180-19c003fbbd55))|如果不希望在 PDB 文件中包含私有符号，则在该框中指定 PDB 文件的名称。 当使用任何生成 PDB 文件的编译器或链接器选项（如 /DEBUG、/Z7、/Zd）生成程序图像时，此选项创建另一个程序数据库 (PDB) 文件。 或 /Zi。 此 PDB 文件省略您不希望交付给客户的符号。 有关详细信息，请参阅 [/PDBSTRIPPED（去除私有符号）](https://msdn.microsoft.com/library/9b9e0070-6a13-4142-8180-19c003fbbd55)。|  
|**生成映射文件** ([/MAP](https://msdn.microsoft.com/library/9ccce53d-4e36-43da-87b0-7603ddfdea63))|通知链接器在链接过程中生成映射文件。 默认设置为“否”。 有关详细信息，请参阅 [/MAP（生成映射文件）](https://msdn.microsoft.com/library/9ccce53d-4e36-43da-87b0-7603ddfdea63)。|  
|**映射文件名**([/map:](https://msdn.microsoft.com/library/9ccce53d-4e36-43da-87b0-7603ddfdea63)*名称*)|如果选择“生成映射文件”，则可在该框中指定映射文件。 有关详细信息，请参阅 [/MAP（生成映射文件）](https://msdn.microsoft.com/library/9ccce53d-4e36-43da-87b0-7603ddfdea63)。|  
|**映射导出** ([/MAPINFO:EXPORTS](https://msdn.microsoft.com/library/533d2bce-f9b7-4fea-ae1c-0b4864c9d10b))|在映射文件中包含导出函数。 默认设置为“否”。 有关详细信息，请参阅[/MAPINFO （包含映射文件中信息）](https://msdn.microsoft.com/library/533d2bce-f9b7-4fea-ae1c-0b4864c9d10b)。|  
|**可调试程序集** ([/ASSEMBLYDEBUG](https://msdn.microsoft.com/library/533d2bce-f9b7-4fea-ae1c-0b4864c9d10b))|为链接器 /ASSEMBLYDEBUG 选项指定设置。 可能的值如下：<br /><br /> -   未发送可调试属性  。<br />-   运行时跟踪和禁用优化 (/ASSEMBLYDEBUG)  。 此设置为默认设置。<br />-   无运行时跟踪和启用优化 (/ASSEMBLYDEBUG:DISABLE)  。<br />-   \<从父级或项目默认设置继承>  。<br />有关详细信息，请参阅 [/ASSEMBLYDEBUG（添加 DebuggableAttribute）](https://msdn.microsoft.com/library/94443af3-470c-41d7-83a0-7434563d7982)。|  
  
 通过使用 Microsoft.VisualStudio.VCProjectEngine.VCDebugSettings 接口，可以在“配置属性”文件夹（“调试”类别）中以编程方式更改这些设置。 有关详细信息，请参阅 <xref:Microsoft.VisualStudio.VCProjectEngine.VCDebugSettings>。  
  
## <a name="see-also"></a>请参阅  
 [调试本机代码](../debugger/debugging-native-code.md)   
 [调试器设置和准备](../debugger/debugger-settings-and-preparation.md)   
 [创建和管理 Visual C++ 项目](https://msdn.microsoft.com/library/11003cd8-9046-4630-a189-a32bf3b88047)   
 [/ASSEMBLYDEBUG（添加 DebuggableAttribute）](https://msdn.microsoft.com/library/94443af3-470c-41d7-83a0-7434563d7982)   
 [用于生成命令和属性的常用宏](https://msdn.microsoft.com/library/239bd708-2ea9-4687-b264-043f1febf98b)
