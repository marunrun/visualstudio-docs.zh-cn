---
title: 排查 Vspackage |Microsoft Docs
ms.date: 11/04/2016
ms.topic: troubleshooting
helpviewer_keywords:
- VSPackages, troubleshooting
- debugging, VSPackages
ms.assetid: 274673e7-72e7-476f-a263-3411b5b874be
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f79bfcb73749992365b167bae84a15de17d2440d
ms.sourcegitcommit: 9a7fb8556a5f3dbb4459122fefc7e7a8dfda753a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/27/2020
ms.locfileid: "87235025"
---
# <a name="troubleshooting-vspackages"></a>VSPackages 故障排除
下面是你可能会遇到的一些常见问题和解决问题的技巧。

### <a name="to-troubleshoot-a-vspackage-that-keeps-visual-studio-from-starting"></a>排查使 Visual Studio 启动的 VSPackage

- [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]在安全模式下启动。

   若要 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 在安全模式下启动，请在命令提示符下键入**devenv.exe/safemode**。

   在此过程中，不会加载 Vspackage，除了附带的 Vspackage [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 。

### <a name="to-troubleshoot-a-vspackage-that-does-not-load"></a>对不加载的 VSPackage 进行故障排除

1. 请确保使用注册 VSPackage 的注册表根目录，通常是实验性的注册表根。

    有关详细信息，请参阅[实验实例](../extensibility/the-experimental-instance.md)。

2. 如果 VSPackage 的目标是在实验性注册表根中运行，请确保运行的实验版本 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 。

    若要运行实验版本，请在命令窗口中键入以下内容： **devenv/rootsuffix exp**。

3. 检查 VSPackage 注册表项。

    有关详细信息，请参阅[注册 vspackage](registering-and-unregistering-vspackages.md)和[管理 vspackage](../extensibility/managing-vspackages.md)。

4. 打开无法加载 VSPackage 的实例的 "**输出**" 窗口 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 。 在该窗口中可能会显示 VSPackage 未能加载的原因的相关信息。

   > [!NOTE]
   > 如果要 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 从 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 集成开发环境（IDE）启动的实验版，请检查这两个版本的 "**输出**" 窗口。

5. 检查活动日志。

    有关详细信息，请参阅[如何：使用活动日志](../extensibility/how-to-use-the-activity-log.md)。

6. 有关 IDE 引发的异常的详细信息，请单击 "**调试**" 菜单上的 "**异常**" 以启用异常。 在 "**异常**" 对话框中，选择想要了解其详细信息的异常类型。

### <a name="to-troubleshoot-a-vspackage-that-does-not-register"></a>对未注册的 VSPackage 进行故障排除

1. 请确保 VSPackage 程序集位于受信任的位置。 RegPkg 无法在不受信任或部分信任的位置（例如，默认的 .net 安全配置中的网络共享）注册程序集。 尽管每当用户在不受信任的位置中创建项目时就会出现警告，但 "不再显示此消息" 复选框可防止此警告重复出现。

### <a name="to-troubleshoot-a-command-that-is-not-visible-or-that-generates-an-error-when-you-click-a-command"></a>排查在单击命令时不可见或生成错误的命令

1. 在命令提示符下键入以下命令，合并新的或更改的菜单命令以及已在 IDE 中的命令 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] ： **Devenv/rootsuffix Exp/setup**。

2. 请确保 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 可以找到 VSPackage 的 UI.dll。

   1. 在注册表的 "包" 部分中找到 VSPackage 的 CLSID：

        HKLM\Software\Microsoft\Visual Studio \\ *\<version>* \Packages

   2. 验证 SatelliteDll 子项给定的路径是否正确。

### <a name="to-troubleshoot-a-vspackage-that-behaves-unexpectedly"></a>排查发生意外行为的 VSPackage 问题

1. 在代码中设置断点。

     调试的良好起点是构造函数和初始化方法。 您还可以在要计算的区域中设置断点，例如菜单命令。 若要启用断点，必须在调试器下运行。

    1. 在“项目”菜单上，单击“属性” 。

    2. 在 "**属性页**" 对话框中，选择 "**调试**" 选项卡。

    3. 在 "**命令行参数**" 框中，键入 VSPackage 目标的开发环境的根后缀。 例如，若要选择实验生成，请键入： **/RootSuffix Exp**。

    4. 在 "**调试**" 菜单上，单击 "**启动调试**" 或按 F5。

        > [!NOTE]
        > 如果正在调试项目，请立即创建或加载现有项目的实例。

2. 使用活动日志。

     通过在关键点将信息写入活动日志来跟踪 VSPackage 行为。 在零售环境中运行 VSPackage 时，此方法特别有用。 有关详细信息，请参阅[如何：使用活动日志](../extensibility/how-to-use-the-activity-log.md)。

3. 使用公共符号。

     若要在调试时提高可读性，可以将符号附加到调试器。

    1. 从 "**工具"/"选项**" 菜单中，导航到 "**调试"/"符号**" 对话框。

    2. 添加此**符号文件（.pdb）位置**：

         `https://msdl.microsoft.com/download/symbols`

    3. 若要提高性能，请指定符号缓存文件夹，例如：

        ```
        C:\symbols
        ```

### <a name="to-troubleshoot-a-missing-vspackage-or-one-of-its-dependencies"></a>排查缺少的 VSPackage 或它的某个依赖项

1. 对于托管代码，请确保引用路径正确。

   1. 在“项目”菜单上，单击“属性” 。

   2. 在 "**属性页**" 对话框中选择 "**引用**" 选项卡，并确保所有路径都是正确的。 或者，您可以使用**对象浏览器**浏览引用的对象。

        对于托管代码，你可以使用[Fuslogvw.exe （程序集绑定日志查看器）](/dotnet/framework/tools/fuslogvw-exe-assembly-binding-log-viewer)来显示失败的程序集加载的详细信息。

2. 对于非托管代码，请在 clsid 注册表节点中找到 VSPackage 的 CLSID [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] ：

    HKLM\Software\Microsoft\Visual Studio \\ *\<version>* \CLSID

   请确保 InprocServer32 项具有 VSPackage dll 的正确路径。

## <a name="see-also"></a>另请参阅
- [VSPackages](../extensibility/internals/vspackages.md)
- [Visual Studio 疑难解答](/troubleshoot/visualstudio/welcome-visual-studio/)
