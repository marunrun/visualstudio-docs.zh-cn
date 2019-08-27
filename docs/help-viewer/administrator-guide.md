---
title: Help Viewer 管理员指南
ms.date: 11/01/2017
ms.topic: conceptual
ms.assetid: 4340c69f-b96b-4932-bb82-38b16a5ab149
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 037ee411c156d21145160dc95b40078fd841493c
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2019
ms.locfileid: "67825129"
---
# <a name="help-viewer-administrator-guide"></a>Help Viewer 管理员指南

通过帮助查看器可以在具有或不具有 Internet 访问的情况下为网络环境管理本地帮助安装。 本地帮助内容按每台计算机进行配置。 默认情况下，用户必须具有管理员权限才能更新其本地帮助安装。

如果网络环境允许客户端访问 Internet，则可以使用 Help Content Manager 可执行文件从 Internet 部署本地帮助内容  。 有关 HlpCtntMgr.exe 命令行语法的详细信息，请参阅 [Help Content Manager 的命令行参数](../help-viewer/command-line-arguments.md)  。

有关创建内容、创建 Intranet 服务终结点以及相似类型的活动的信息，请参阅 [Help Viewer SDK](../extensibility/internals/microsoft-help-viewer-sdk.md)。

如果网络环境不允许访问 Internet，则 Help Viewer 可以从 Intranet 或网络共享部署本地帮助内容。 还可以使用[注册表项重写](../help-viewer/behavior-overrides.md)功能禁用 Visual Studio IDE 帮助选项，比如：

- 联机与脱机帮助

- 首次启动 IDE 时的内容安装

- 指定 Intranet 内容服务

- 管理内容

## <a name="deploy-local-help-content-from-the-internet"></a>从 Internet 部署本地帮助内容

可使用 Help Content Mananger (HlpCtntMgr.exe) 从 Internet 将本地帮助内容部署到客户端计算机   。 请使用以下语法：

```cmd
\\%ProgramFiles(x86)%\Microsoft Help Viewer\v2.3\HlpCtntmgr.exe /operation \<*name*> /catalogname \<*catalog name*> /locale \<*locale*>
```

有关 HlpCtntMgr.exe 命令行语法的详细信息，请参阅 [Help Content Manager 的命令行参数](../help-viewer/command-line-arguments.md)  。

要求：

- 客户端计算机必须可以访问 Internet。

- 用户必须具有管理员权限才能在安装之后更新、添加或移除本地帮助内容。

注意：

- 帮助的默认源仍处于联机状态。

### <a name="example"></a>示例

以下示例将用于 Visual Studio 的英语内容安装到客户端计算机。

#### <a name="to-install-english-content-from-the-internet"></a>从 Internet 安装英语内容

1. 选择“开始”  ，然后选择“运行”  。

2. 键入下列命令：

     `C:\Program Files (x86)\Microsoft Help Viewer\v2.3\hlpctntmgr.exe /operation install /catalogname VisualStudio15 /locale en-us`

3. 按 **Enter**。

## <a name="deploy-pre-installed-local-help-content-on-client-computers"></a>在客户端计算机上部署预先安装的本地帮助内容

可以将联机的内容集安装到一台计算机，然后将已安装的该内容复制到其他计算机。

要求：

- 用于安装内容集的计算机必须可以访问 Internet。

- 用户必须具有管理员权限才能在安装之后更新、添加或移除本地帮助内容。

    > [!TIP]
    > 如果用户没有管理员权限，则建议在 Help Viewer 中禁用“管理内容”选项卡  。 有关详细信息，请参阅 [Help Content Manager 重写](../help-viewer/behavior-overrides.md)。

注意：

- 帮助的默认源仍处于联机状态。

### <a name="create-the-content-set"></a>创建内容集

必须先在目标计算机上卸载所有本地 Visual Studio 内容，然后才能创建基本内容集。

#### <a name="to-uninstall-local-help"></a>卸载本地帮助

1. 在 Help Viewer 中，选择“管理内容”  选项卡。

2. 导航到 Visual Studio 文档集。

3. 选择每个子项旁的“删除”  。

4. 选择“更新”  进行卸载。

5. 浏览到 %ProgramData%\Microsoft\HelpLibrary2\Catalogs\VisualStudio15 并验证该文件夹是否仅包含文件 catalogType.xml   。

   一旦移除所有以前安装的本地 Visual Studio 帮助内容，便已准备好下载基本内容集。

#### <a name="to-download-the-content"></a>下载内容

1. 在 Help Viewer 中，选择“管理内容”  选项卡。

2. 在“推荐的文档”  或“可用的文档”  下，导航到要下载的文档集，然后选择“添加”  。

3. 选择“更新”  。

接下来，需要对内容进行打包，以便它可以部署到客户端计算机。

#### <a name="to-package-the-content"></a>对内容进行打包

1. 创建要将内容复制到其中的文件夹以便将来进行部署。 例如:C:\VSHelp  。

2. 使用管理员权限打开 cmd.exe  。

3. 导航到在步骤 1 中创建的文件夹。

4. 键入下列命令：

     `Xcopy %ProgramData%\Microsoft\HelpLibrary2 \<*foldername*>\ /y /e /k /o`

     例如： `Xcopy %ProgramData%\Microsoft\HelpLibrary2 c:\VSHelp\ /y /e /k /o`

### <a name="deploy-the-content"></a>部署内容

1. 创建网络共享，然后将帮助内容复制到该位置。

     例如，将 C:\VSHelp 中的内容复制到 \\\myserver\VSHelp   。

2. 创建用于包含帮助内容的部署脚本的 .bat 文件  。 由于客户端可能对在推送过程中删除的任何文件具有读取锁定，所以应在推送更新之前关闭客户端。 例如:

    ```cmd
    REM - copy pre-ripped content to ProgramData
    Xcopy %~dp0HelpLibrary2 %SYSTEMDRIVE%\ProgramData\Microsoft\HelpLibrary2\ /y /e /k /o
    if ERRORLEVEL 1 ECHO *** ERROR COPYING Help Library files to ProgramData (%ERRORLEVEL%)
    ```

3. 在要安装帮助内容的本地计算机上运行 .bat 文件  。

## <a name="see-also"></a>请参阅

- [Help Content Manager 的命令行参数](../help-viewer/command-line-arguments.md)
- [Help Content Manager 重写](../help-viewer/behavior-overrides.md)
- [Microsoft Help Viewer](../help-viewer/overview.md)
- [Help Viewer SDK](../extensibility/internals/microsoft-help-viewer-sdk.md)