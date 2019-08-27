---
title: 自定义独立的 Shell |Microsoft Docs
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
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62555963"
---
# <a name="customizing-the-isolated-shell"></a>自定义独立的 Shell
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

通过更改 Visual Studio 用户界面的各个方面以及限制的命令和在专用应用程序中包含的功能，可以自定义 Visual Studio 独立 shell 应用程序。  
  
## <a name="using-the-applicationpkgdef-file"></a>使用 Application.pkgdef 文件  
 独立的 shell 模板解决方案包括*SolutionName*。Application.pkgdef 文件，可以修改以下功能：  
  
##### <a name="the-application-title"></a>应用程序标题  
 你可以自定义应用程序标题，这是通过更改"AppName"行中的值显示该应用程序的标题栏中的名称*SolutionName*。Application.pkgdef 文件。 有关更多详细信息，请参阅[演练：创建基本的独立 Shell 应用程序](../extensibility/walkthrough-creating-a-basic-isolated-shell-application.md)。  
  
 如果不希望显示当前加载的项目的应用程序标题，更改"ShowHierarchyRootInTitle"行中的值*SolutionName*。Application.pkgdef dword: 00000001 中的文件复制到 dword:00000000。  
  
##### <a name="the-application-icon"></a>应用程序图标  
 您可以自定义应用程序图标，它是应用程序名称的应用程序标题栏中显示的图标。 将不同的图标复制到图标目录中。 在中**解决方案资源管理器**，将图标添加到资源文件文件夹。 然后打开 VSShellStub.rc 文件并 IDI_STUBPROGRAM 的值替换为新图标的名称。 有关更多详细信息，请参阅[演练：创建基本的独立 Shell 应用程序](../extensibility/walkthrough-creating-a-basic-isolated-shell-application.md)。  
  
##### <a name="the-command-line-logo"></a>命令行的徽标  
 你可以自定义命令行的徽标，它是从命令行中，通过更改"CommandLineLogo"行中的值来启动应用程序时，将显示的文本*SolutionName*。Application.pkgdef 文件。 有关更多详细信息，请参阅[演练：创建基本的独立 Shell 应用程序](../extensibility/walkthrough-creating-a-basic-isolated-shell-application.md)  
  
##### <a name="the-name-of-the-user-files-subfolder"></a>用户文件子文件夹的名称  
 你可以对用户文件维护通过更改"UserFilesSubFolderName"行中的值的应用程序的文件夹的名称*SolutionName*。Application.pkgdef 文件。  
  
##### <a name="the-title-of-the-solution-tree-node-in-the-new-project-dialog"></a>新项目对话框中的解决方案树中节点的标题  
 可以通过更改"NewProjDlgSlnTreeNodeTitle"行中的值来自定义的新项目对话框中的解决方案节点标题*SolutionName*。Application.pkgdef 文件。  
  
##### <a name="the-installed-templates-header-in-the-new-project-dialog"></a>新项目对话框中的已安装的模板标头  
 可以通过更改"NewProjDlgInstalledTemplatesHdr"行中的值更改新项目对话框中的已安装的模板标头*SolutionName*。Application.pkgdef 文件。  
  
##### <a name="whether-or-not-to-hide-miscellaneous-files-by-default"></a>是否默认情况下隐藏杂项文件  
 您可以指定是否默认情况下隐藏杂项文件，方法是更改"HideMiscellaneousFilesByDefault"行中的值*SolutionName*。Application.pkgdef 文件。 若要隐藏杂项文件，请将值设置`dword:00000001`，并以显示的文件，请将值设置`dword:00000000`。  
  
##### <a name="whether-or-not-to-disable-the-output-window"></a>是否禁用输出窗口  
 您可以指定是否禁用你的应用程序中的输出窗口中的"DisableOutputWindow"行的值*SolutionName*。Application.pkgdef 文件。 若要禁用输出窗口，请将值设置`dword:00000001`，并以显示输出窗口，请将值设置`dword:00000000`。  
  
##### <a name="whether-or-not-to-allow-dropped-files-on-the-main-window"></a>是否允许在主窗口拖放的文件  
 您可以指定是否允许在你的应用程序的主窗口上拖放的文件通过更改"AllowsDroppedFilesOnMainWindow"行中的值*SolutionName*。Application.pkgdef 文件。 若要允许拖放的文件，请将值设置`dword:00000001`，并将值设置为不允许拖放的文件， `dword:00000000`。  
  
##### <a name="the-default-search-page"></a>默认搜索页  
 你可以自定义 web 浏览器页上，打开 web 浏览器窗口，方法是更改"DefaultSearchPage"行中的值时显示的页面*SolutionName*。Application.pkgdef 文件。  
  
##### <a name="the-default-home-page"></a>默认的主页  
 可以通过更改的值中的"DefaultHomePage"行的自定义主页*SolutionName*。Application.pkgdef 文件。 有关更多详细信息，请参阅[演练：创建基本的独立 Shell 应用程序](../extensibility/walkthrough-creating-a-basic-isolated-shell-application.md)  
  
##### <a name="whether-or-not-to-hide-the-solution-concept"></a>是否要隐藏的解决方案概念  
 您可以指定是否隐藏您的应用程序中的解决方案，方法是更改"HideSolutionConcept"行中的值*SolutionName*。Application.pkgdef 文件。 若要隐藏解决方案，请将值设置`dword:00000001`，并以显示该解决方案，请将值设置`dword:00000000`。  
  
##### <a name="the-default-debug-engine"></a>默认调试引擎  
 你可以通过更改"DefaultDebugEngine"行中的值使用你的应用程序的调试引擎*SolutionName*。Application.pkgdef 文件复制到调试引擎的 GUID。  
  
##### <a name="the-file-extension-of-the-user-options-file"></a>用户选项文件的文件扩展名  
 你可以对用户文件维护通过更改"UserOptsFileExt"行中的值的应用程序的文件夹的名称*SolutionName*。Application.pkgdef 文件。  
  
##### <a name="the-solution-file-extension"></a>解决方案文件扩展名  
 你可以更改"SolutionFileExt"行中的值用您的解决方案文件的扩展插件*SolutionName*。Application.pkgdef 文件。  
  
##### <a name="the-default-user-files-folder-root"></a>默认用户文件文件夹根  
 您可以通过更改"UserFilesSubFolderName"行中的值更改为应用程序的用户文件的根文件夹名称*SolutionName*。Application.pkgdef 文件。  
  
##### <a name="the-solution-file-creator-identifier"></a>解决方案文件创建者标识符  
 你可以更改"SolutionFileCreatorIdentifier"行中的值时使用的解决方案文件的标识符*SolutionName*。Application.pkgdef 文件。  
  
##### <a name="the-default-projects-location"></a>默认项目位置  
 可以通过更改"DefaultProjectsLocation"行中的值更改默认项目位置的名称*SolutionName*。Application.pkgdef 文件。  
  
##### <a name="the-application-localization-package"></a>应用程序本地化包  
 你可以更改"AppLocalizationPackage"行中的值用于你的应用程序的本地化包*SolutionName*。Application.pkgdef 文件。  
  
##### <a name="whether-or-not-to-show-the-hierarchy-root-in-the-title"></a>是否在标题中显示层次结构根  
 您可以指定是否通过更改"ShowHierarchyRootInTitle"行中的值在你的应用程序中的标题栏中显示层次结构根*SolutionName*。Application.pkgdef 文件。 若要显示在层次结构根，请将值设置`dword:00000001`，并将值设置可隐藏层次结构根， `dword:00000000`。  
  
##### <a name="specifying-a-start-page"></a>指定起始页  
 若要在指定自定义应用程序起始页*SolutionName*。Application.pkgdef 文件中，将"DisableStartPage"值设置为`dword:00000000`，并在`[$RootKey$\StartPage\Default]`将 URI 设置为.xaml 文件的位置：  
  
```  
DisableStartPage=dword:00000000  
[$RootKey$\StartPage\Default]  
"Uri"="$RootFolder$\<name of XAML file>"  
```  
  
 Applicationcommands.vsct 文件中*SolutionName*UI 项目，注释掉"No_ShellPkg_startPageCommand"条目：  
  
```  
<!--<Define name="No_ShellPkg_StartPageCommand"/>-->  
```  
  
 .Xaml 文件，并为需要的任何图形文件必须添加*SolutionName*项目。 实际上必须将这些文件复制到*SolutionName*项目目录中，不会添加一些其他目录中。  
  
 在所有文件上设置**项类型**属性设置为**独立 Shell 的文件**复制到的文件顺序 *$RootFolder$* 目录。 (若要设置**项类型**属性中，右键单击该文件，然后选择**属性**。 此属性位于**配置属性**，**常规**。)  
  
 自定义起始页的详细信息，请参阅[自定义起始页](../ide/customizing-the-start-page-for-visual-studio.md)。  
  
## <a name="using-other-elements-of-the-isolated-shell"></a>使用独立 shell 的其他元素  
 可以使用其他文件和独立的 shell 解决方案模板，以进一步自定义应用程序中包含的项目。  
  
##### <a name="enabledisable-visual-studio-packages"></a>启用/禁用 Visual Studio 包  
 *SolutionName*.pkgundef 文件，您可以通过排除某些包禁用某些类型的 Visual Studio 功能。 例如，以下行：  
  
```  
[$RootKey$\Projects\{A2FE74E1-B743-11d0-AE1A-00A0C90FFFC3}\AddItemTemplates\TemplateDirs\{39c9c826-8ef8-4079-8c95-428f5b1c323f}]  
```  
  
 从项目模板显示在组中删除杂项文件项目**新的项目**对话框。 有关更多详细信息，请参阅[演练：创建基本的独立 Shell 应用程序](../extensibility/walkthrough-creating-a-basic-isolated-shell-application.md)。  
  
##### <a name="enabledisable-menu-commands"></a>启用/禁用菜单命令  
 *SolutionName*UI.vsct 文件包括注释掉所有可用的独立 shell 的菜单命令的列表。 若要禁用给定的命令，取消注释相应的行。 例如，若要禁用的窗口/拆分注释，取消注释`<Define name="No_SplitCommand"/>`行。 有关更多详细信息，请参阅[演练：创建基本的独立 Shell 应用程序](../extensibility/walkthrough-creating-a-basic-isolated-shell-application.md)。  
  
##### <a name="the-bitmap-used-on-the-splash-screen"></a>在初始屏幕上使用位图  
 你可以自定义初始屏幕，这是启动应用程序，方法是更改"SplashScreenBitmap"行中的值时显示的窗口上使用的位图*SolutionName*。Application.pkgdef 文件。 有关更多详细信息，请参阅[演练：创建基本的独立 Shell 应用程序](../extensibility/walkthrough-creating-a-basic-isolated-shell-application.md)。  
  
##### <a name="the-helpabout-window"></a>帮助/关于窗口  
 独立的 shell 模板中没有一个单独的项目可用于自定义帮助 / 关于框中为应用程序。 有关更多详细信息，请参阅[演练：创建基本的独立 Shell 应用程序](../extensibility/walkthrough-creating-a-basic-isolated-shell-application.md)。
