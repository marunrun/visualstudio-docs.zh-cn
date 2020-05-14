---
title: 故障排除 VS 包 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSPackages, troubleshooting
- debugging, VSPackages
ms.assetid: 274673e7-72e7-476f-a263-3411b5b874be
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a4827a36bd8e76462a137ae7e903c1ab624121c0
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80698920"
---
# <a name="troubleshooting-vspackages"></a>VSPackages 故障排除
以下是 VSPackage 中可能存在的常见问题以及解决问题的提示。

### <a name="to-troubleshoot-a-vspackage-that-keeps-visual-studio-from-starting"></a>排除阻止可视化工作室启动的 VS 包的故障

- 在[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]安全模式下启动。

   要在[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]安全模式下启动，在命令提示符下，键入**devenv.exe /safemode**。

   在此过程中，除了附带的 VS 包外，不会加载任何 VS[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]包。

### <a name="to-troubleshoot-a-vspackage-that-does-not-load"></a>排除未加载的 VS 包

1. 请确保正在使用注册 VSPackage 的注册表根（通常是实验注册表根）。

    有关详细信息，请参阅[实验实例](../extensibility/the-experimental-instance.md)。

2. 如果 VSPackage 的目标是在实验注册表根中运行，请确保运行 的实验版本[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]。

    要运行实验版本，在命令窗口中键入以下内容 **：devenv /rootuffix exp**。

3. 检查您的 VSPackage 注册表项。

    有关详细信息，请参阅注册[VS 包](registering-and-unregistering-vspackages.md)和管理[VS 包](../extensibility/managing-vspackages.md)。

4. 打开无法**Output**加载 VSPackage 的[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]实例的输出窗口。 有关 VSPackage 无法加载原因的信息可能会显示在该窗口中。

   > [!NOTE]
   > 如果要从[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)][!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]集成开发环境 （IDE） 启动 其实验版本，请检查两个版本的**输出**窗口。

5. 检查活动日志。

    有关详细信息，请参阅[：使用活动日志](../extensibility/how-to-use-the-activity-log.md)。

6. 有关 IDE 引发的异常的详细信息，请单击 **"调试**"菜单上**的异常**以启用异常。 在 **"例外"** 对话框中，选择您希望了解有关的详细信息的异常类型。

### <a name="to-troubleshoot-a-vspackage-that-does-not-register"></a>排除未注册的 VS 包

1. 确保 VSPackage 程序集驻留在受信任的位置。 RegPkg 无法在不受信任或部分受信任的位置（如默认 .net 安全配置中的网络共享）注册程序集。 尽管每当用户在不受信任的位置创建项目时都会出现警告，但"不再显示此消息"复选框可以防止此警告再次发生。

### <a name="to-troubleshoot-a-command-that-is-not-visible-or-that-generates-an-error-when-you-click-a-command"></a>对不可见的命令进行故障排除，或在单击命令时生成错误

1. 通过在[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]命令提示符中键入以下内容 **：devenv /rootuffix Exp /setup，** 合并新的或更改的菜单命令以及已在 IDE 中的命令。

2. 请确保[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]可以为 VSPackage 找到 UI.dll。

   1. 在注册表的"打包"部分查找 VS 包的 CLSID：

        HKLM_软件_微软_视觉工作室\\*\<版本>[* 包]

   2. 验证 SatelliteDll 子键给出的路径是否正确。

### <a name="to-troubleshoot-a-vspackage-that-behaves-unexpectedly"></a>排除行为意外的 VS 包

1. 在代码中设置断点。

     调试的良好起点是构造函数和初始化方法。 您还可以在要计算的区域（如菜单命令）中设置断点。 要启用断点，必须在调试器下运行。

    1. 在 **“项目”** 菜单上，单击 **“属性”**。

    2. 在"**属性页"** 对话框中，选择 **"调试**"选项卡。

    3. 在 **"命令行参数"** 框中，键入 VSPackage 目标开发环境的根后缀。 例如，要选择实验生成，请键入 **：/RootSuffix Exp**。

    4. 在 **"调试"** 菜单上，单击 **"开始调试"** 或按 F5。

        > [!NOTE]
        > 如果要调试项目，请立即创建或加载项目的现有实例。

2. 使用活动日志。

     通过在关键点将信息写入活动日志来跟踪 VSPackage 行为。 当您在零售环境中运行 VSPackage 时，此技术特别有用。 有关详细信息，请参阅[：使用活动日志](../extensibility/how-to-use-the-activity-log.md)。

3. 使用公共符号。

     为了提高调试时的可读性，可以将符号附加到调试器。

    1. 从 **"工具/选项**"菜单中导航到 **"调试/符号"** 对话框。

    2. 添加此**符号文件 （.pdb） 位置**：

         `https://msdl.microsoft.com/download/symbols`

    3. 为了提高性能，请指定符号缓存文件夹，例如：

        ```
        C:\symbols
        ```

### <a name="to-troubleshoot-a-missing-vspackage-or-one-of-its-dependencies"></a>排除丢失的 VSPackage 或其依赖项之一

1. 对于托管代码，请确保引用路径正确。

   1. 在 **“项目”** 菜单上，单击 **“属性”**。

   2. 在"**属性页"** 对话框中选择 **"引用**"选项卡，并确保所有路径都正确。 或者，您可以使用**对象浏览器**浏览引用的对象。

        对于托管代码，可以使用[Fuslogvw.exe（程序集绑定日志查看器）](/dotnet/framework/tools/fuslogvw-exe-assembly-binding-log-viewer)来显示程序集负载失败的详细信息。

2. 对于非托管代码，在[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]CLSID 注册表节点中找到 VSPackage 的 CLSID：

    HKLM_软件_微软_视觉工作室\\*\<版本*>[CLSID]

   确保 InprocServer32 条目具有 VSPackage dll 的正确路径。

## <a name="see-also"></a>请参阅
- [VSPackage](../extensibility/internals/vspackages.md)
