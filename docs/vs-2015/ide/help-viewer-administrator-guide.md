---
title: Help Viewer 管理员指南 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-help-viewer
ms.topic: conceptual
ms.assetid: 4340c69f-b96b-4932-bb82-38b16a5ab149
caps.latest.revision: 15
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 03cacd8de574de92002b44b237cd84c22e761eaf
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72645576"
---
# <a name="help-viewer-administrator-guide"></a>帮助查看器管理员指南
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

通过帮助查看器可以在具有或不具有 Internet 访问的情况下为网络环境管理本地帮助安装。 本地帮助内容按每台计算机进行配置。 默认情况下，用户必须具有管理员权限才能更新其本地帮助安装。

 如果网络环境允许客户端访问 Internet，则帮助查看器允许使用命令行脚本从 Internet 部署本地帮助内容。

 如果网络环境不允许客户端访问 Internet，则帮助查看器可以从 Intranet 或网络共享部署本地帮助内容。 还可以使用注册表项替代来禁用 Visual Studio IDE 帮助选项（如联机/脱机帮助、首次启动 IDE 时的内容安装、指定 Intranet 内容服务以及管理内容）。

 基本语法如下所示：

 \<*路径*> \HlpCtntmgr.exe/operation \<*参数*>/catalogname \<*名称*>/locale \<*区域设置*>/sourceuri \< *. .msha 路径或 URL* 0

 有关 HlpCtntMgr.exe 命令行语法的详细信息，请参阅 [Help Content Manager 的命令行参数](../ide/command-line-arguments-for-the-help-content-manager.md)。

 有关创建内容、创建 Intranet 服务终结点以及相似类型的活动的详细信息，请参阅帮助查看器 SDK。

## <a name="deploying-local-help-content-from-the-internet"></a>从 Internet 部署本地帮助内容
 可以使用 MSDN 内容包服务从 Internet 将本地帮助内容部署到客户端计算机。 请使用以下语法：

 \\<path to>\v2.2\HlpCtntmgr.exe /operation \<name> /catalogname \<catalog name> /locale \<locale>

 有关 HlpCtntMgr.exe 命令行语法的详细信息，请参阅 [Help Content Manager 的命令行参数](../ide/command-line-arguments-for-the-help-content-manager.md)。

 要求：

- 客户端计算机必须可以访问 Internet。

- 用户必须具有管理员权限才能在安装之后更新、添加或移除本地帮助内容。

  注意：

- 帮助的默认源仍处于联机状态。

  > [!TIP]
  > 可以通过修改 HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\14.0\help\UseOnlineHelp 注册表项来更改帮助的默认源。 有关详细信息，请参阅 [Help Content Manager 重写](../ide/help-content-manager-overrides.md)。

- 系统仍会在首次启动 Visual Studio 时提示客户端安装基本帮助内容。 可以通过修改 HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\VisualStudio\14.0\Help\DisableFirstRunHelpSelection 注册表项来禁用此提示。

### <a name="example"></a>示例
 以下示例将用于 Visual Studio 的英语内容安装到客户端计算机。

##### <a name="to-install-english-content-from-the-internet"></a>从 Internet 安装英语内容

1. 选择“开始”，然后选择“运行”。

2. 键入下列命令：

     C:\Program Files (x86)\Microsoft Help Viewer\v2.2\hlpctntmgr.exe /operation install /catalogname VisualStudio14 /locale en-us

3. 按 Enter。

## <a name="deploying-pre-installed-local-help-content-on-client-computers"></a>在客户端计算机上部署预安装的本地帮助内容
 可以将联机的内容集安装到一台计算机，然后将已安装的该内容复制到其他计算机。

 要求：

- 用于安装内容集的计算机必须可以访问 Internet。

- 用户必须具有管理员权限才能在安装之后更新、添加或移除本地帮助内容。

  > [!TIP]
  > 如果用户没有管理员权限，则建议在帮助查看器中禁用“管理内容”选项卡。 有关详细信息，请参阅 [Help Content Manager 重写](../ide/help-content-manager-overrides.md)。

  注意：

- 如果用户没有管理员权限，则建议在帮助查看器中禁用“管理内容”选项卡。 有关详细信息，请参阅 [Help Content Manager 重写](../ide/help-content-manager-overrides.md)。

- 帮助的默认源仍处于联机状态。

- 系统仍会在首次启动 Visual Studio 时提示客户端安装基本帮助内容。 有关详细信息，请参阅 [Help Content Manager 重写](../ide/help-content-manager-overrides.md)。

### <a name="create-the-content-set"></a>创建内容集
 必须先在目标计算机上卸载所有本地 Visual Studio 内容，然后才能创建基本内容集。

##### <a name="to-uninstall-local-help"></a>卸载本地帮助

1. 在 Help Viewer 中，选择“管理内容”选项卡。

2. 在“可用的文档”下，导航到 Visual Studio 文档集。

3. 选择每个子项旁的“删除”。

4. 选择“开始”开始卸载

5. 浏览到 n:\ProgramData\Microsoft\HelpLibrary2\Catalogs\VisualStudio12 并验证该文件夹是否仅包含文件 catalogType.xml。

   一旦移除所有以前安装的本地 Visual Studio 帮助内容，便已准备好下载基本内容集。

##### <a name="to-download-the-content"></a>下载内容

1. 在 Help Viewer 中，选择“管理内容”选项卡。

2. 在“可用的文档”下，导航到要下载的文档集，然后选择“添加”。

3. 选择“启动”。

   接下来，需要对内容进行打包，以便它可以部署到客户端计算机。

##### <a name="to-package-the-content"></a>对内容进行打包

1. 创建要将内容复制到其中的文件夹以便将来进行部署。

     例如：c:\VS12Help。

2. 使用管理员权限打开 cmd.exe。

3. 导航到在步骤 1 中创建的文件夹。

4. 键入下列命令：

     Xcopy %SYSTEMDRIVE%\ProgramData\Microsoft\HelpLibrary2 \<*文件夹名*>\ /y /e /k /o

     例如： `Xcopy %SYSTEMDRIVE%\ProgramData\Microsoft\HelpLibrary2 c:\VS12Help\ /y /e /k /o`

### <a name="deploying-the-content"></a>部署内容

##### <a name="to-deploy-the-content"></a>部署内容

1. 创建网络共享，然后将帮助内容复制到该位置。

     例如，将 c:\VS12Help 中的内容复制到 \\\myserver\VS12Help。

2. 创建用于包含帮助内容的部署脚本的 .bat 文件。 由于客户端可能对在推送过程中删除的任何文件具有读取锁定，所以应在推送更新之前关闭客户端。

     例如:

    ```
    REM - copy pre-ripped content to ProgramData
    Xcopy %~dp0HelpLibrary2 %SYSTEMDRIVE%\ProgramData\Microsoft\HelpLibrary2\ /y /e /k /o
    if ERRORLEVEL 1 ECHO *** ERROR COPYING Help Library files to Programdata (%ERRORLEVEL%)

    REM - get processor type and create/run registry update file
    IF "%PROCESSOR_ARCHITECTURE%"=="AMD64" GOTO AMD64

    @echo Architecture type is x86

    ECHO Windows Registry Editor Version 5.00 > x86.reg

    ECHO [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Help\v2.2\Catalogs] >> x86.reg
    ECHO "ContentStore"="%SYSTEMDRIVE%\\ProgramData\\Microsoft\\HelpLibrary2\\Catalogs\\" >> x86.reg

    ECHO [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Help\v2.2\Catalogs\VisualStudio12] >> x86.reg
    ECHO "LocationPath"="%SYSTEMDRIVE%\\ProgramData\\Microsoft\\HelpLibrary2\\Catalogs\\VisualStudio12\\"  >> x86.reg
    ECHO "FirstTimeRun"="False"  >> x86.reg

    ECHO [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Help\v2.2\Catalogs\VisualStudio12\en-US]  >> x86.reg
    ECHO "ContentStore"="%SYSTEMDRIVE%\\ProgramData\\Microsoft\\HelpLibrary2\\Catalogs\\VisualStudio12\\"  >> x86.reg
    ECHO "catalogName"="Visual Studio version Help Documentation"  >> x86.reg

    ECHO [HKEY_LOCAL_MACHINE\Software\Microsoft\VSWinExpress\14.0\help]  >> x86.reg
    ECHO "UseOnlineHelp"=dword:00000000  >> x86.reg

    regedit.exe /s x86.reg
    if ERRORLEVEL 1 ECHO *** ERROR inserting the x86 reg (%ERRORLEVEL%)

    GOTO CONTINUE

    :AMD64
    @echo Architecture type is AMD64

    ECHO Windows Registry Editor Version 5.00 > x64.reg

    ECHO [HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Help\v2.2\Catalogs] >> x64.reg
    ECHO "ContentStore"="%SYSTEMDRIVE%\\ProgramData\\Microsoft\\HelpLibrary2\\Catalogs\\" >> x64.reg

    ECHO [HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Help\v2.2\Catalogs\VisualStudio14] >> x64.reg
    ECHO "LocationPath"="%SYSTEMDRIVE%\\ProgramData\\Microsoft\\HelpLibrary2\\Catalogs\\VisualStudio14\\"  >> x64.reg
    ECHO "FirstTimeRun"="False"  >> x64.reg

    ECHO [HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Help\v2.2\Catalogs\VisualStudio14\en-US]  >> x64.reg
    ECHO "ContentStore"="%SYSTEMDRIVE%\\ProgramData\\Microsoft\\HelpLibrary2\\Catalogs\\VisualStudio12\\en-US\\"  >> x64.reg
    ECHO "catalogName"="Visual Studio version Help Documentation"  >> x64.reg

    ECHO [HKEY_LOCAL_MACHINE\Software\Wow6432Node\Microsoft\VSWinExpress\14.0\help]  >> x64.reg
    ECHO "UseOnlineHelp"=dword:00000000  >> x64.reg

    regedit.exe /s x64.reg
    if ERRORLEVEL 1 ECHO *** ERROR inserting the x64 reg (%ERRORLEVEL%)

    :CONTINUE
    ```

3. 在要安装帮助内容的本地计算机上运行 bat 文件。

## <a name="see-also"></a>请参阅
 [Help Content manager](../ide/command-line-arguments-for-the-help-content-manager.md) [帮助内容管理器替代](../ide/help-content-manager-overrides.md)的命令行参数
