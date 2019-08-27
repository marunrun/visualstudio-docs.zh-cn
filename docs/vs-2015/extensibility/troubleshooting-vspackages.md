---
title: VSPackages 故障排除 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: troubleshooting
helpviewer_keywords:
- VSPackages, troubleshooting
- debugging, VSPackages
ms.assetid: 274673e7-72e7-476f-a263-3411b5b874be
caps.latest.revision: 23
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 62c1847e9ff476e364ed99cabc4b47a970c4c4da
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65695509"
---
# <a name="troubleshooting-vspackages"></a>VSPackages 故障排除
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

以下是常见的问题可能与你的 VSPackage 并解决问题的提示。  
  
### <a name="to-troubleshoot-a-vspackage-that-keeps-visual-studio-from-starting"></a>若要防止 Visual Studio 启动 VSPackage 进行故障排除  
  
- 启动[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]在安全模式下。  
  
     若要启动[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]在安全模式下，在命令提示符处，键入**devenv.exe /safemode**。  
  
     在此过程中没有 Vspackage 加载 Vspackage 的附带除[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]。  
  
### <a name="to-troubleshoot-a-vspackage-that-does-not-load"></a>若要进行故障排除不会加载 VSPackage  
  
1. 请确保使用注册 VSPackage 来运行，通常的实验性注册表根注册表根。  
  
     有关详细信息，请参阅[实验实例](../extensibility/the-experimental-instance.md)。  
  
2. 如果 VSPackage 针对在实验性注册表根目录中运行，请确保你正在运行的实验版本[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]。  
  
     若要运行的实验版本，可在命令窗口中键入以下： **devenv /rootsuffix exp**。  
  
3. 请检查 VSPackage 的注册表条目。  
  
     有关详细信息，请参阅[注册 Vspackage](internals/registering-vspackages.md)并[管理 Vspackage](../extensibility/managing-vspackages.md)。  
  
4. 打开**输出**的实例的窗口[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]无法加载 VSPackage。 有关 VSPackage 无法加载的原因的信息可能显示在该窗口中。  
  
    > [!NOTE]
    > 如果要开始的实验版本[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]从[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]集成的开发环境 (IDE) 中，检查**输出**窗口中的这两个版本。  
  
5. 活动日志中检查。  
  
     有关详细信息，请参阅[如何：使用活动日志](../extensibility/how-to-use-the-activity-log.md)。  
  
6. 有关由 IDE 引发的异常的详细信息，请单击**异常**上**调试**菜单启用例外。 在中**异常**对话框中选择要了解详细信息的异常的类型。  
  
### <a name="to-troubleshoot-a-vspackage-that-does-not-register"></a>若要进行故障排除不会注册 VSPackage  
  
1. 请确保 VSPackage 程序集位于受信任的位置。 RegPkg 无法在不受信任或部分受信任的位置，例如默认的.net 安全配置中的网络共享中注册程序集。 每当用户在不受信任的位置创建一个项目时，会出现一个警告，尽管"不再显示此消息"复选框可以避免重复此警告。  
  
### <a name="to-troubleshoot-a-command-that-is-not-visible-or-that-generates-an-error-when-you-click-a-command"></a>若要进行故障排除的命令不可见或当您单击的命令生成错误  
  
1. 通过键入以下内容合并新的或更改菜单命令和已在 IDE[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]命令提示符： **devenv /rootsuffix Exp /setup**。  
  
2. 请确保[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]可以找到 UI.dll 为你的 VSPackage。  
  
    1. 在注册表的程序包部分中找到的 vspackage 的 CLSID:  
  
         HKLM\Software\Microsoft\Visual Studio\\*\<version>* \Packages  
  
    2. 验证给定 SatelliteDll 子项的路径正确。  
  
### <a name="to-troubleshoot-a-vspackage-that-behaves-unexpectedly"></a>若要解决意外的行为的 VSPackage  
  
1. 在代码中设置断点。  
  
     用于调试的良好起点是构造函数和初始化方法。 此外可以在您想要评估，如菜单命令的区域中设置断点。 若要启用断点，必须在调试器下运行。  
  
    1. 在“项目”菜单上，单击“属性”。  
  
    2. 上**属性页**对话框中，选择**调试**选项卡。  
  
    3. 在中**命令行参数**框中，键入在开发环境的根后缀的 VSPackage 目标。 例如，若要选择的实验性生成，请键入： **RootSuffix Exp**。  
  
    4. 上**调试**菜单上，单击**开始调试**或按 F5。  
  
        > [!NOTE]
        > 如果你正在调试一个项目，创建或现在加载你的项目的现有实例。  
  
2. 使用活动日志。  
  
     通过将信息写入到的关键点的活动日志跟踪 VSPackage 行为。 此方法时，尤其是零售环境中运行 VSPackage。 有关详细信息，请参阅[如何：使用活动日志](../extensibility/how-to-use-the-activity-log.md)。  
  
3. 使用公共符号。  
  
     若要调试的同时提高可读性，可以附加到调试器符号。  
  
    1. 从**工具/选项**菜单中，导航到**调试/符号**对话框。  
  
    2. 添加以下**符号文件 (.pdb) 位置**:  
  
         [http://msdl.microsoft.com/download/symbols](http://msdl.microsoft.com/download/symbols)  
  
    3. 为了提高性能，请指定一个符号缓存文件夹，例如：  
  
        ```  
        C:\symbols  
        ```  
  
### <a name="to-troubleshoot-a-missing-vspackage-or-one-of-its-dependencies"></a>若要解决缺少 VSPackage 或其某个依赖项  
  
1. 对于托管代码中，请确保引用路径正确。  
  
   1. 在“项目”菜单上，单击“属性”。  
  
   2. 选择**引用**选项卡**属性页**对话框，并确保所有路径都是否正确。 或者，可以使用**对象浏览器**来查找被引用对象。  
  
        对于托管代码中，你可以使用[Fuslogvw.exe （程序集绑定日志查看器）](https://msdn.microsoft.com/library/e32fa443-0778-4cc3-bf36-5c8ea297d296)显示失败的程序集加载的详细信息。  
  
2. 对于非托管代码中，找到的 VSPackage 中 CLSID [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] CLSID 注册表节点：  
  
    HKLM\Software\Microsoft\Visual Studio\\*\<version>* \CLSID  
  
   请确保 InprocServer32 项具有 VSPackage dll 的正确路径。  
  
## <a name="see-also"></a>请参阅  
 [VSPackage](../extensibility/internals/vspackages.md)
