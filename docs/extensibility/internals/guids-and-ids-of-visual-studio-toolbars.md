---
title: Visual Studio 工具栏的 GUID 和 IT |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- visual studio groups
- toolbars
- visual studio toolbar
- id
- toolgar group
- tool window toolbar
- guid
ms.assetid: c9cacd57-9225-450f-a9ac-cbf3168ea844
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: fe42821cdacc038d767e52373d45ddd7b8954323
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80708230"
---
# <a name="guids-and-ids-of-visual-studio-toolbars"></a>Visual Studio 工具栏的 GUID 和 IT
本主题枚举 Visual Studio 集成开发环境 （IDE） 中包含的工具栏的 GUID 和 ID 值及其包含的组。 这些值在作为可视化工作室 SDK 的一部分安装的 *.vsct*文件中定义。 有关详细信息，请参阅[IDE 定义的命令、菜单和组](../../extensibility/internals/ide-defined-commands-menus-and-groups.md)。

> [!NOTE]
> Visual Studio 提供的许多工具栏不是由 Visual Studio 定义的，并且其 GUID 和 ID 值不为公共。 本主题仅列出在 Visual Studio SDK *.vsct*文件中定义的工具栏。

 有关如何处理*在 .vsct*文件中定义的 IDE 对象的详细信息，请参阅[扩展菜单和命令](../../extensibility/extending-menus-and-commands.md)。

 Visual Studio IDE 提供的默认工具栏使用 GUID，`guidSHLMainMenu`除非使用`GUID:ID`语法以其他方式指定。

## <a name="ide-toolbars"></a>IDE 工具栏
 以下工具栏由可视化工作室 IDE 提供。 工具栏可以通过在 **"工具**"菜单的**工具栏**子菜单上选择来显示它们。 工具窗口中的工具栏不包括在此部分中。

 只有组可以直接从工具栏下降。 要添加组，应将其父级设置为工具栏的 GUID 和 ID。 要向工具栏添加按钮，将其父项设置为工具栏上的组。

|工具栏|ID|
|-------------|--------|
|Standard|IDM_VS_TOOL_STANDARD|
|生成|IDM_VS_TOOL_BUILD|
|文本编辑器|IDM_VS_TOOL_TEXTEDITOR|
|调试|吉德VS调试组：IDM_DEBUG_TOOLBAR|
|调试位置|吉德VS调试组：IDM_DEBUG_CONTEXT_TOOLBAR|

### <a name="special-toolbars"></a>专用工具栏
 这些工具栏由 Visual Studio IDE 定义，但它们提供专用功能，不承载命令组。

|工具栏|ID|
|-------------|--------|
|Add 命令|IDM_VS_TOOL_ADDCOMMAND|
|Undefined|IDM_VS_TOOL_UNDEFINED|
|XML 架构|IDM_VS_TOOL_SCHEMA|
|XML 数据|IDM_VS_TOOL_DATA|

## <a name="groups-on-the-ide-toolbars"></a>IDE 工具栏上的组
 要向标准工具栏添加按钮，将以下组之一设置为其父组。 组按父工具栏排序。

### <a name="standard-toolbar-groups"></a>标准工具栏组

|名称|ID|
|----------|--------|
|保存/打开|IDG_VS_TOOLSB_SAVEOPEN|
|剪切/复制|IDG_VS_TOOLSB_CUTCOPY|
|撤消/重做|IDG_VS_TOOLSB_UNDOREDO|
|运行/生成|IDG_VS_TOOLSB_RUNBUILD|
|搜索|IDG_VS_TOOLSB_SEARCH|
|Windows|IDG_VS_TOOLSB_WINDOWS|
|新窗口|IDG_VS_TOOLSB_NEWWINDOWS|
|加载/保存|IDG_VS_WINDOWUI_LOADSAVE|
|仪表|IDG_VS_TOOLSB_GAUGE|

### <a name="build-toolbar-groups"></a>生成工具栏组

|名称|ID|
|----------|--------|
|生成栏|IDG_VS_BUILDBAR|
|取消|IDG_VS_BUILD_CANCEL|

### <a name="text-editor-toolbar-groups"></a>文本编辑器工具栏组

|名称|ID|
|----------|--------|
|Completion|IDM_VS_TOOL_TEXTEDITOR|
|降级|IDG_VS_EDITTOOLBAR_INDENT|
|注释|IDG_VS_EDITTOOLBAR_COMMENT|
|书签|IDG_VS_EDITTOOLBAR_TEMPBOOKMARKS|

### <a name="debug-toolbar-groups"></a>调试工具栏组

|名称|ID|
|----------|--------|
|执行|IDM_DEBUG_TOOLBAR|
|单步执行|IDG_DEBUG_TOOLBAR_STEPPING|
|监视|IDG_DEBUG_TOOLBAR_WATCH|
|Windows|IDG_DEBUG_TOOLBAR_WINDOWS|

### <a name="debug-location-toolbar-groups"></a>调试位置工具栏组

|名称|ID|
|----------|--------|
|调试位置|IDG_DEBUG_CONTEXT_TOOLBAR|

## <a name="tool-window-toolbars"></a>工具窗口工具栏
 工具栏可以直接出现在 IDE 或工具窗口中（如**解决方案资源管理器**）。 由于工具窗口未在 *.vsct*文件中定义，因此工具窗口工具栏没有定义的父控件。 相反，它们被放置在代码中。 下表显示了 IDE 中工具窗口中显示的工具栏及其包含的命令组。

> [!NOTE]
> 工具栏和组使用 GUID `guidSHLMainMenu`，除非使用 GUID：ID 语法另有说明。 如果为工具栏指定 GUID，它也适用于从该工具栏下降的组。

|工具窗口|工具栏|组|
|-----------------|-------------|------------|
|解决方案资源管理器|IDM_VS_TOOL_PROJWIN|IDG_VS_PROJ_TOOLBAR1.5|
|服务器资源管理器|guid_SE_MenuGroup：IDM_SE_TOOLBAR_SERVEREXPLORER|IDG_SE_TOOLBAR_REFRESH|
|属性|IDM_VS_TOOL_PROPERTIES|IDG_VS_PROPERTIES_SORT<br /><br /> IDG_VS_PROPERTIES_PAGES|
|类视图|IDM_VS_TOOL_CLASSVIEW|IDG_VS_CLASSVIEW_FOLDERS<br /><br /> IDG_VS_CLASSVIEW_SEARCH<br /><br /> IDG_VS_CLASSVIEW_SETTINGS|
|类视图|IDM_VS_TOOL_CLASSVIEW_GO|IDG_VS_CLASSVIEW_SEARCH2|
|对象浏览器|IDM_VS_TOOL_OBJBROWSER|IDG_VS_OBJBROWSER_SUBSETS<br /><br /> IDG_VS_OBJBROWSER_SEARCH<br /><br /> IDG_VS_OBJBROWSER_ADDREFERENCE<br /><br /> IDG_VS_OBJBROWSER_BROWSERSETTINGS|
|对象浏览器|IDM_VS_TOOL_OBJECT_BROWSER_GO|IDG_VS_OBJBROWSER_SEARCH2|
|Output|IDM_VS_TOOL_OUTPUTWINDOW|IDG_VS_OUTPUTWINDOW_SELECT<br /><br /> IDG_VS_OUTPUTWINDOW_GOTO<br /><br /> IDG_VS_OUTPUTWINDOW_NEXTPREV<br /><br /> IDG_VS_OUTPUTWINDOW_CLEAR<br /><br /> IDG_VS_OUTPUTWINDOW_WORDWRAP|
|查找和替换|IDM_VS_TOOL_UNIFIEDFIND|IDG_VS_FINDTAB<br /><br /> IDG_VS_REPLACETAB|
|查找结果 1|IDM_VS_TOOL_FINDRESULTS1|IDG_VS_FINDRESULTS1_GOTO<br /><br /> IDG_VS_FINDRESULTS1_NEXTPREV<br /><br /> IDG_VS_FINDRESULTS1_CLEAR<br /><br /> IDG_VS_FINDRESULTS1_STOPFIND|
|查找结果 2|IDM_VS_TOOL_FINDRESULTS2|IDG_VS_FINDRESULTS2_GOTO<br /><br /> IDG_VS_FINDRESULTS2_NEXTPREV<br /><br /> IDG_VS_FINDRESULTS2_CLEAR<br /><br /> IDG_VS_FINDRESULTS2_STOPFIND|
|片段|IDM_VS_TOOL_SNIPPETMENUS|IDG_VS_SNIPPET_REPL<br /><br /> IDG_VS_SNIPPET_REF<br /><br /> IDG_VS_SNIPPET_PROP|
|书签|IDM_VS_TOOL_BOOKMARKWIND|IDG_VS_BWNEWFOLDER<br /><br /> IDG_VS_BWNEXTBM<br /><br /> IDG_VS_BWNEXTBMF<br /><br /> IDG_VS_BWENABLE<br /><br /> IDG_VS_BWDELETE|
|任务列表|IDM_VS_TOOL_TASKLIST|IDG_VS_TASKLIST_PROVIDERLIST|
|用户任务|IDM_VS_TOOL_USERTASKS|IDG_VS_TASKLIST_PROVIDERLIST<br /><br /> IDG_VS_USERTASKS_EDIT|
|错误列表|IDM_VS_TOOL_ERRORLIST|IDG_VS_ERRORLIST_ERRORGROUP<br /><br /> IDG_VS_ERRORLIST_WARNINGGROUP<br /><br /> IDG_VS_ERRORLIST_MESSAGEGROUP|
|调用浏览器|IDM_VS_TOOL_CALLBROWSER1.16|IDG_VS_TOOLBAR_CALLBROWSER1_ACTIONS<br /><br /> IDG_VS_TOOLBAR_CALLBROWSER1_TYPE<br /><br /> IDG_VS_TOOLBAR_CALLBROWSER1_CBSETTINGS|
|断点|吉德VS调试组：IDM_BREAKPOINTS_WINDOW_TOOLBAR|IDG_BREAKPOINTS_WINDOW_NEW<br /><br /> IDG_BREAKPOINTS_WINDOW_DELETE<br /><br /> IDG_BREAKPOINTS_WINDOW_ALL<br /><br /> IDG_BREAKPOINTS_WINDOW_VIEW<br /><br /> IDG_BREAKPOINTS_WINDOW_EDIT<br /><br /> IDG_BREAKPOINTS_WINDOW_COLUMNS|
|反汇编|吉德VS调试组：IDM_DISASM_WINDOW_TOOLBAR|IDG_DISASM_WINDOW_TOOLBAR|
|内存 1-4|吉德VS调试组：IDM_MEMORY_WINDOW_TOOLBAR1...4|IDG_MEMORY_EXPRESSION1.4<br /><br /> IDG_MEMORY_COLUMNS1.4|
|进程|吉德VS调试组：IDM_ATTACHED_PROCS_TOOLBAR|IDG_ATTACHED_PROCS_EXECCNTRLIDG_ATTACHED_PROCS_STEPPING<br /><br /> IDG_ATTACHED_PROCS_EXECCNTRL2<br /><br /> IDG_ATTACHED_PROCS_ATTACH<br /><br /> IDG_ATTACHED_PROCS_COLUMNS|

## <a name="see-also"></a>请参阅
- [将菜单控制器添加到工具栏](../../extensibility/adding-a-menu-controller-to-a-toolbar.md)
- [向工具窗口添加工具栏](../../extensibility/adding-a-toolbar-to-a-tool-window.md)
- [Visual Studio 菜单的 GUID 和 IT](../../extensibility/internals/guids-and-ids-of-visual-studio-menus.md)
