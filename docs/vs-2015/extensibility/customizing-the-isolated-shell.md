---
title: 自定义独立 Shell |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio shell, isolated mode
ms.assetid: e0b7c3ae-210f-4f48-ac49-6a59e6034f5f
caps.latest.revision: 16
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 724d4d0c4b392a362e702f33ea996df3a6fc0ad6
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62555963"
---
# <a name="customizing-the-isolated-shell"></a>自定义独立 Shell
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可以通过更改 Visual Studio 用户界面的不同方面，并限制专用应用程序中包含的命令和功能，自定义 Visual Studio 独立 shell 应用程序。  
  
## <a name="using-the-applicationpkgdef-file"></a>使用 .pkgdef 文件  
 独立 shell 模板解决方案包含解决方案 *名称*。.Pkgdef 文件，可用于修改以下功能：  
  
##### <a name="the-application-title"></a>应用程序标题  
 您可以自定义应用程序标题，这是在应用程序的标题栏中显示的名称，通过更改 *解决方案*名称中 "AppName" 行的值。.Pkgdef 文件。 有关更多详细信息，请参阅 [演练：创建基本的独立 Shell 应用程序](../extensibility/walkthrough-creating-a-basic-isolated-shell-application.md)。  
  
 如果您不希望应用程序标题显示当前加载的项目，请更改 *解决方案名称*中的 "ShowHierarchyRootInTitle" 行的值。.Pkgdef file from dword： 00000001 to dword：00000000。  
  
##### <a name="the-application-icon"></a>应用程序图标  
 你可以自定义应用程序图标，它是应用程序标题栏中的应用程序名称所显示的图标。 将不同的图标复制到图标目录。 在 **解决方案资源管理器**中，将图标添加到 "资源文件" 文件夹。 然后打开 VSShellStub 文件，并将 IDI_STUBPROGRAM 的值替换为新图标的名称。 有关更多详细信息，请参阅 [演练：创建基本的独立 Shell 应用程序](../extensibility/walkthrough-creating-a-basic-isolated-shell-application.md)。  
  
##### <a name="the-command-line-logo"></a>命令行徽标  
 您可以自定义命令行徽标，这是从命令行启动应用程序时显示的文本（通过更改 *解决方案名称*中的 "CommandLineLogo" 行的值）。.Pkgdef 文件。 有关更多详细信息，请参阅 [演练：创建基本的独立 Shell 应用程序](../extensibility/walkthrough-creating-a-basic-isolated-shell-application.md)  
  
##### <a name="the-name-of-the-user-files-subfolder"></a>用户文件子文件夹的名称  
 通过更改 *解决方案*名称中的 "UserFilesSubFolderName" 行的值，可以更改应用程序为用户文件维护的文件夹的名称。.Pkgdef 文件。  
  
##### <a name="the-title-of-the-solution-tree-node-in-the-new-project-dialog"></a>"新建项目" 对话框中解决方案树节点的标题  
 您可以通过 *在 "新建*项目" 对话框中更改 "NewProjDlgSlnTreeNodeTitle" 行的值来自定义该解决方案节点的标题。.Pkgdef 文件。  
  
##### <a name="the-installed-templates-header-in-the-new-project-dialog"></a>"新建项目" 对话框中的 "已安装模板" 标头  
 您可以通过更改 *解决方案名称*中的 "NewProjDlgInstalledTemplatesHdr" 行的值来更改 "新建项目" 对话框中的 "已安装模板" 标头。.Pkgdef 文件。  
  
##### <a name="whether-or-not-to-hide-miscellaneous-files-by-default"></a>是否默认隐藏杂项文件  
 可以通过更改 *解决方案名称*中 "HideMiscellaneousFilesByDefault" 行的值来指定是否默认隐藏杂项文件。.Pkgdef 文件。 若要隐藏杂项文件、设置值 `dword:00000001` 和显示文件，请设置值 `dword:00000000` 。  
  
##### <a name="whether-or-not-to-disable-the-output-window"></a>是否禁用 "输出" 窗口  
 您可以通过更改 *解决方案名称*中的 "DisableOutputWindow" 行的值来指定是否禁用应用程序中的 "输出" 窗口。.Pkgdef 文件。 若要禁用 "输出" 窗口，请设置值 `dword:00000001` ，若要显示 "输出" 窗口，请设置值 `dword:00000000` 。  
  
##### <a name="whether-or-not-to-allow-dropped-files-on-the-main-window"></a>是否允许主窗口上的已删除文件  
 您可以通过更改 *解决方案名称*中的 "AllowsDroppedFilesOnMainWindow" 行的值来指定是否允许在您的应用程序的主窗口上删除文件。.Pkgdef 文件。 若要允许删除的文件、设置值 `dword:00000001` 以及禁止删除的文件，请设置值 `dword:00000000` 。  
  
##### <a name="the-default-search-page"></a>默认搜索页  
 您可以通过更改 *解决方案名称*中的 "DefaultSearchPage" 行的值来自定义 web 浏览器页，该页面是在 web 浏览器窗口打开时显示的页面。.Pkgdef 文件。  
  
##### <a name="the-default-home-page"></a>默认主页  
 您可以通过更改 *解决方案名称*中的 "DefaultHomePage" 行的值来自定义主页。.Pkgdef 文件。 有关更多详细信息，请参阅 [演练：创建基本的独立 Shell 应用程序](../extensibility/walkthrough-creating-a-basic-isolated-shell-application.md)  
  
##### <a name="whether-or-not-to-hide-the-solution-concept"></a>是否隐藏解决方案概念  
 可以通过更改解决方案 *名称*中 "HideSolutionConcept" 行的值来指定是否要在应用程序中隐藏解决方案。.Pkgdef 文件。 若要隐藏解决方案，请设置值 `dword:00000001` ，若要显示解决方案，请设置值 `dword:00000000` 。  
  
##### <a name="the-default-debug-engine"></a>默认调试引擎  
 通过更改 *解决方案名称*中的 "DefaultDebugEngine" 行的值，可以更改应用程序使用的调试引擎。.Pkgdef 文件到调试引擎的 GUID。  
  
##### <a name="the-file-extension-of-the-user-options-file"></a>用户选项文件的文件扩展名  
 通过更改 *解决方案*名称中的 "UserOptsFileExt" 行的值，可以更改应用程序为用户文件维护的文件夹的名称。.Pkgdef 文件。  
  
##### <a name="the-solution-file-extension"></a>解决方案文件扩展名  
 可以通过更改解决方案 *名称*中 "SolutionFileExt" 行的值来更改用于解决方案文件的扩展。.Pkgdef 文件。  
  
##### <a name="the-default-user-files-folder-root"></a>默认的用户文件文件夹根  
 通过更改 *解决方案*名称中的 "UserFilesSubFolderName" 行的值，可以更改应用程序的用户文件的根文件夹的名称。.Pkgdef 文件。  
  
##### <a name="the-solution-file-creator-identifier"></a>解决方案文件创建者标识符  
 您可以通过更改解决方案 *名称*中 "SolutionFileCreatorIdentifier" 行的值来更改用于解决方案文件的标识符。.Pkgdef 文件。  
  
##### <a name="the-default-projects-location"></a>默认项目位置  
 您可以通过更改 *解决方案*名称中的 "DefaultProjectsLocation" 行的值来更改默认项目位置的名称。.Pkgdef 文件。  
  
##### <a name="the-application-localization-package"></a>应用程序本地化包  
 可以通过更改 *解决方案名称*中 "AppLocalizationPackage" 行的值来更改用于应用程序的本地化包。.Pkgdef 文件。  
  
##### <a name="whether-or-not-to-show-the-hierarchy-root-in-the-title"></a>是否在标题中显示层次结构根  
 您可以通过更改 *解决方案名称*中的 "ShowHierarchyRootInTitle" 行的值来指定是否在应用程序的标题栏中显示层次结构根。.Pkgdef 文件。 若要显示层次结构根，请设置值 `dword:00000001` ，若要隐藏层次结构根，请设置值 `dword:00000000` 。  
  
##### <a name="specifying-a-start-page"></a>指定起始页  
 若要指定自定义应用程序的起始页，请在 *解决方案名称*中。.Pkgdef 文件，将 "DisableStartPage" 值设置为 `dword:00000000` ，并在 " `[$RootKey$\StartPage\Default]` 将 URI 设置为 .xaml 文件的位置" 下：  
  
```  
DisableStartPage=dword:00000000  
[$RootKey$\StartPage\Default]  
"Uri"="$RootFolder$\<name of XAML file>"  
```  
  
 在 *解决方案名称*UI 项目的 system.windows.input.applicationcommands.paste 文件中，注释掉 "No_ShellPkg_startPageCommand" 条目：  
  
```  
<!--<Define name="No_ShellPkg_StartPageCommand"/>-->  
```  
  
 您必须将该 .xaml 文件和所需的任何图形文件添加到 *解决方案名称* 项目中。 必须实际将这些文件复制到 *解决方案名称* 项目目录，而不是从其他目录添加。  
  
 对于所有文件，将 " **项类型** " 属性设置为 " **独立 Shell 文件** "，以便将文件复制到 *$RootFolder $* 目录。  (若要设置 " **项类型** " 属性，请右键单击该文件，然后选择 " **属性**"。 此属性位于 " **配置属性**"、" **常规**" 下。 )   
  
 有关自定义起始页的详细信息，请参阅 [自定义起始页](../ide/customizing-the-start-page-for-visual-studio.md)。  
  
## <a name="using-other-elements-of-the-isolated-shell"></a>使用独立 shell 的其他元素  
 您可以使用独立 shell 解决方案模板中包含的其他文件和项目来进一步自定义您的应用程序。  
  
##### <a name="enabledisable-visual-studio-packages"></a>启用/禁用 Visual Studio 包  
 .Pkgundef 文件允许通过排除某些包来禁用某些类型的 Visual Studio*功能。* 例如，以下行：  
  
```  
[$RootKey$\Projects\{A2FE74E1-B743-11d0-AE1A-00A0C90FFFC3}\AddItemTemplates\TemplateDirs\{39c9c826-8ef8-4079-8c95-428f5b1c323f}]  
```  
  
 从 " **新建项目** " 对话框中显示的项目模板集中删除杂项文件项目。 有关更多详细信息，请参阅 [演练：创建基本的独立 Shell 应用程序](../extensibility/walkthrough-creating-a-basic-isolated-shell-application.md)。  
  
##### <a name="enabledisable-menu-commands"></a>启用/禁用菜单命令  
 *解决方案名称*.vsct 文件包含可用于隔离 shell 的所有菜单命令的注释掉列表。 若要禁用某个给定的命令，请取消注释相应的行。 例如，若要禁用 "窗口/拆分" 注释，请取消注释 `<Define name="No_SplitCommand"/>` 该行。 有关更多详细信息，请参阅 [演练：创建基本的独立 Shell 应用程序](../extensibility/walkthrough-creating-a-basic-isolated-shell-application.md)。  
  
##### <a name="the-bitmap-used-on-the-splash-screen"></a>初始屏幕上使用的位图  
 您可以自定义初始屏幕上使用的位图，它是启动应用程序时显示的窗口，通过更改 *解决方案名称*中的 "SplashScreenBitmap" 行的值来显示。.Pkgdef 文件。 有关更多详细信息，请参阅 [演练：创建基本的独立 Shell 应用程序](../extensibility/walkthrough-creating-a-basic-isolated-shell-application.md)。  
  
##### <a name="the-helpabout-window"></a>"帮助/关于" 窗口  
 在独立 shell 模板中，有一个单独的项目，可用于自定义应用程序的 "帮助"/"关于" 框。 有关更多详细信息，请参阅 [演练：创建基本的独立 Shell 应用程序](../extensibility/walkthrough-creating-a-basic-isolated-shell-application.md)。
