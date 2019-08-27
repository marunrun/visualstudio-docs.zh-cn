---
title: Visual Studio 菜单的 Guid 和 Id |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- visual studio menus
- visual studio groups
- id
- existing menus
- guid
- menus
ms.assetid: 84639d86-dd21-4b35-9988-6bb654162488
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 26171ae9f4464c3b8b63762d92e9a91d5a4b8420
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66329107"
---
# <a name="guids-and-ids-of-visual-studio-menus"></a>Guid 和 Id 的 Visual Studio 菜单
这篇文章枚举菜单和 Visual Studio 菜单栏上的组的 GUID 和 ID 的值。 这些值中定义 *.vsct*作为 Visual Studio SDK 的一部分安装的文件。 有关详细信息，请参阅[IDE 定义的命令、 菜单和组](../../extensibility/internals/ide-defined-commands-menus-and-groups.md)。

 有关如何使用集成的开发环境 (IDE) 对象中定义的详细信息 *.vsct*文件，请参阅[扩展菜单和命令](../../extensibility/extending-menus-and-commands.md)。

 菜单和 Visual Studio 菜单栏上的组使用的 GUID `guidSHLMainMenu`。 在菜单栏本身具有 ID 的`IDM_VS_TOOL_MAINMENU`。

## <a name="groups-on-the-visual-studio-menu-bar"></a>在 Visual Studio 菜单栏上的组
 若要将菜单添加到菜单栏，其中一个组作为其父进行设置。

|Group|Id|
|-----------|--------|
|文件/编辑/查看|IDG_VS_MM_FILEEDITVIEW|
|重构|IDG_VS_MM_REFACTORING:|
|项目|IDG_VS_MM_PROJECT|
|Build|IDG_VS_MM_BUILDDEBUGRUN|
|格式/工具|IDG_VS_MM_TOOLSADDINS|
|窗口 / 帮助 / 社区|IDG_VS_MM_WINDOWHELP|
|外接程序|IDG_VS_MM_MACROS|
|FullScreenBar|IDG_VS_MM_FULLSCREENBAR|

## <a name="menus-on-the-visual-studio-menu-bar"></a>在 Visual Studio 菜单栏上的菜单
 若要将组添加到现有 Visual Studio 菜单中，设置作为其父一个以下菜单。 此列表中不包含子菜单。

|菜单|Id|
|----------|--------|
|文件|IDM_VS_MENU_FILE|
|Edit|IDM_VS_MENU_EDIT|
|视图|IDM_VS_MENU_VIEW|
|重构|IDM_VS_MENU_REFACTORING|
|项目|IDM_VS_MENU_PROJECT|
|Build|IDM_VS_MENU_BUILD|
|格式|IDM_VS_MENU_FORMAT|
|工具|IDM_VS_MENU_TOOLS|
|Extensions|IDM_VS_MENU_EXTENSIONS|
|窗口|IDM_VS_MENU_WINDOW|
|外接程序|IDM_VS_MENU_ADDINS|
|社区|IDM_VS_MENU_COMMUNITY|
|Help|IDM_VS_MENU_HELP|

## <a name="groups-on-visual-studio-menus"></a>Visual Studio 菜单上的组
 以下列表显示了源自直接菜单在 Visual Studio 菜单栏的组。 将命令添加到 Visual Studio 菜单的最快方法是设置其中某个组的父级。 在本部分中不显示源自子菜单的组。

### <a name="file-menu-groups"></a>文件菜单组

|Group|Id|
|-----------|--------|
|打开新 /|IDG_VS_FILE_FILE|
|添加|IDG_VS_FILE_ADD|
|解决方案|IDG_VS_FILE_SOLUTION|
|杂项|IDG_VS_FILE_MISC|
|保存|IDG_VS_FILE_SAVE|
|重命名|IDG_VS_FILE_RENAME|
|浏览者|IDG_VS_FILE_BROWSER|
|的|IDG_VS_FILE_PRINT|
|最近使用|IDG_VS_FILE_MRU|
|移动|IDG_VS_FILE_MOVE|
|Exit|IDG_VS_FILE_EXIT|

### <a name="edit-menu-groups"></a>编辑菜单组

|Group|Id|
|-----------|--------|
|撤消/重做|IDG_VS_EDIT_UNDOREDO|
|剪切/复制/粘贴|IDG_VS_EDIT_CUTCOPY|
|选择|IDG_VS_EDIT_SELECT|
|GoTo|IDG_VS_EDIT_GOTO|
|查找|IDG_VS_EDIT_FIND|
|对象|IDG_VS_EDIT_OBJECTS|
|OLE 谓词|IDG_VS_EDIT_OLEVERBS|
|命令的格式|IDG_VS_EDIT_COMMANDWELL|

### <a name="refactor-menu-groups"></a>重构菜单组

|Group|Id|
|-----------|--------|
|通用|IDG_REFACTORING_COMMON|
|高级|IDG_REFACTORING_ADVANCED|

### <a name="view-menu-groups"></a>视图菜单组

|Group|Id|
|-----------|--------|
|窗体代码|IDG_VS_VIEW_FORMCODE|
|浏览者|IDG_VS_VIEW_BROWSER|
|定义视图|IDG_VS_VIEW_DEFINEVIEWS|
|Windows|IDG_VS_VIEW_WINDOWS|
|构建 Windows|IDG_VS_VIEW_ARCH_WINDOWS|
|组织 Windows|IDG_VS_VIEW_ORG_WINDOWS|
|代码浏览器|IDG_VS_VIEW_CODEBROWSENAV_WINDOWS|
|开发 Windows|IDG_VS_VIEW_DEV_WINDOWS|
|工具栏|IDG_VS_VIEW_TOOLBARS|
|Symbols|IDG_VS_VIEW_SYMBOLNAVIGATE|
|导航|IDG_VS_VIEW_NAVIGATE|
|小导航|IDG_VS_VIEW_SMALLNAVIGATE|
|对象浏览器|IDG_VS_VIEW_OBJBRWSR|
|命令的格式|IDG_VS_VIEW_COMMANDWELL|
|属性页|IDG_VS_VIEW_PROPPAGES|
|刷新|IDG_VS_VIEW_REFRESH|

### <a name="project-menu-groups"></a>项目菜单组

|Group|Id|
|-----------|--------|
|杂项添加|IDG_VS_PROJ_MISCADD|
|添加|IDG_VS_PROJ_ADD|
|文件夹|IDG_VS_PROJ_FOLDER|
|卸载/重载|IDG_VS_PROJ_UNLOADRELOAD|
|参考|IDG_VS_PROJ_REFERENCE|
|选项|IDG_VS_PROJ_OPTIONS|
|设置|IDG_VS_PROJ_SETTINGS|

### <a name="build-menu-groups"></a>生成的菜单组

|Group|Id|
|-----------|--------|
|解决方案|IDG_VS_BUILD_SOLUTION|
|选择|IDG_VS_BUILD_SELECTION|
|按配置优化|IDG_VS_PGO_SELECTION|
|杂项|IDG_VS_BUILD_MISC|
|取消|IDG_VS_BUILD_CANCEL|

### <a name="tools-menu-groups"></a>工具菜单组

|Group|Id|
|-----------|--------|
|命令行|IDG_VS_TOOLS_CMDLINE|
|代码段|IDG_VS_TOOLS_SNIPPETS|
|对象子集|IDG_VS_TOOLS_OBJSUBSET|
|选项|IDG_VS_TOOLS_OPTIONS|
|另外 2 个|IDG_VS_TOOLS_OTHER2|
|外部工具|IDG_VS_TOOLS_EXT_TOOLS|
|外部自定义项|IDG_VS_TOOLS_EXT_CUST|

### <a name="window-menu-groups"></a>窗口菜单组

|Group|Id|
|-----------|--------|
|新建|IDG_VS_WINDOW_NEW|
|停靠/关闭|IDG_VS_DOCKCLOSE|
|停靠/隐藏|IDG_VS_DOCKHIDE|
|排列|IDG_VS_WINDOW_ARRANGE|
|导航|IDG_VS_WINDOW_NAVIGATION|
|列表|IDG_VS_WINDOW_LIST|

### <a name="help-menu-groups"></a>帮助菜单组

|Group|Id|
|-----------|--------|
|示例|IDG_VS_HELP_SAMPLES|
|支持|IDG_VS_HELP_SUPPORT|
|关于|IDG_VS_HELP_ABOUT|

## <a name="submenus-of-visual-studio-menus"></a>Visual Studio 菜单的子菜单
 以下层次结构显示了与 Visual Studio 菜单栏上的菜单相关联的子菜单。 由于仅允许一组可作为其父菜单，因此每个子菜单必须降从组在菜单上，而不是直接从菜单。 有关菜单、 组和子菜单之间的关系的详细信息，请参阅[添加到菜单的子菜单](../../extensibility/adding-a-submenu-to-a-menu.md)。

> [!NOTE]
> 在 Visual Studio 菜单栏上的菜单名称单独不显示此层次结构中因为它们可以根据推断出在 IDE 中，组的命名约定，如下所示：*IDG_VS_\<菜单名称\>_\<组名\>* 。

|父组|子菜单|子组|
|------------------|-------------|------------------|
|IDG_VS_FILE_FILE|IDM_VS_CSCD_NEW|IDG_VS_FILE_NEW_CASCADE|
||IDM_VS_CSCD_OPEN|IDG_VS_FILE_OPENP_CASCADE|
|||IDG_VS_FILE_OPENF_CASCADE|
|IDG_VS_FILE_ADD|IDM_VS_CSCD_ADD|IDG_VS_FILE_ADD_PROJECT_NEW|
|||IDG_VS_FILE_ADD_PROJECT_EXI|
|IDG_VS_FILE_MRU|IDM_VS_CSCD_FILEMRU|IDG_VS_FILE_FMRU_CASCADE|
||IDM_VS_CSCD_PROJMRU|IDG_VS_FILE_PMRU_CASCADE|
|IDG_VS_FILE_MOVE|IDM_VS_CSCD_MOVETOPRJ|IDG_VS_FILE_MOVE_CASCADE|
|||IDG_VS_FILE_MOVE_PICKER|
|IDG_VS_VIEW_DEV_WINDOWS|IDM_VS_CSCD_FINDRESULTS|IDG_VS_WNDO_FINDRESULTS|
||IDM_VS_CSCD_WINDOWS|IDG_VS_VIEW_CALLBROWSER|
|||IDG_VS_WNDO_OTRWNDWS1...6|
|||IDG_VS_WNDO_WINDOWS2|
|IDG_VS_VIEW_TOOLBARS|IDM_VS_CSCD_COMMANDBARS||
|IDG_VS_EDIT_GOTO|IDM_VS_EDITOR_FIND_MENU||
|IDG_VS_EDIT_OBJECTS|IDM_VS_CSCD_MNUDES|IDG_VS_MNUDES_INSERT|
|||IDG_VS_MNUDES_EDITNAMES|
||IDM_VS_CSCD_OLEVERBS|IDG_VS_EDIT_OLEVERBS|
|IDG_VS_BUILD_SELECTION|IDM_VS_CSCD_BUILD|IDG_VS_BUILD_CASCADE|
|||IDG_VS_BUILD_PROJPICKER|
||IDM_VS_CSCD_REBUILD|IDG_VS_REBUILD_CASCADE|
|||IDG_VS_REBUILD_PROJPICKER|
||IDM_VS_CSCD_PROJONLY|IDG_VS_PROJONLY_CASCADE|
||IDM_VS_CSCD_CLEAN|IDG_VS_CLEAN_CASCADE|
|||IDG_VS_CLEAN_PROJPICKER|
||IDM_VS_CSCD_DEPLOY|IDG_VS_DEPLOY_CASCADE|
|||IDG_VS_DEPLOY_PROJPICKER|
|IDG_VS_PGO_SELECTION|IDM_VS_CSCD_PGO_BUILD|IDG_VS_PGO_BUILD_CASCADE_BUILD|
|||IDG_VS_PGO_BUILD_CASCADE_RUN|

## <a name="see-also"></a>请参阅
- [Guid 和 Id 的 Visual Studio 工具栏](../../extensibility/internals/guids-and-ids-of-visual-studio-toolbars.md)
- [Guid 和 Id 的 Visual Studio 命令](../../extensibility/internals/guids-and-ids-of-visual-studio-commands.md)
- [Visual Studio 命令表格 (.vsct) 文件](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
