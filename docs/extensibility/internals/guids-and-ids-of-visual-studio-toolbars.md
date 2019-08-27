---
title: Visual Studio 工具栏的 Guid 和 Id |Microsoft Docs
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
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 62384942bb0577860161f8ae11d2eb6e787257bf
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66328884"
---
# <a name="guids-and-ids-of-visual-studio-toolbars"></a>Guid 和 Id 的 Visual Studio 工具栏
本主题枚举包括 Visual Studio 集成的开发环境 (IDE) 中的工具栏的 GUID 和 ID 值，并包含的组。 这些值中定义 *.vsct*作为 Visual Studio SDK 的一部分安装的文件。 有关详细信息，请参阅[IDE 定义的命令、 菜单和组](../../extensibility/internals/ide-defined-commands-menus-and-groups.md)。

> [!NOTE]
> 许多发布到 Visual Studio 工具栏未定义的 Visual Studio 中，并且其 GUID 和 ID 值不是公共。 本主题列出了在 Visual Studio SDK 中定义的工具栏 *.vsct*文件。

 有关如何使用 IDE 对象中定义的详细信息 *.vsct*文件，请参阅[扩展菜单和命令](../../extensibility/extending-menus-and-commands.md)。

 提供的 Visual Studio IDE 的默认工具栏使用的 GUID `guidSHLMainMenu`，除非另行指定通过使用`GUID:ID`语法。

## <a name="ide-toolbars"></a>IDE 工具栏
 以下工具栏提供了 Visual Studio IDE。 可以通过选择上显示工具栏**工具栏**的子菜单**工具**菜单。 在本部分中不包括的工具窗口的工具栏。

 只有组可以降直接从工具栏中。 若要添加一个组，将其父级设置为 GUID 和 ID 的工具栏。 若要添加到工具栏按钮，请在工具栏上向组设置其父级。

|Toolbar|Id|
|-------------|--------|
|标准|IDM_VS_TOOL_STANDARD|
|Build|IDM_VS_TOOL_BUILD|
|文本编辑器|IDM_VS_TOOL_TEXTEDITOR|
|调试|guidVSDebugGroup:IDM_DEBUG_TOOLBAR|
|调试位置|guidVSDebugGroup:IDM_DEBUG_CONTEXT_TOOLBAR|

### <a name="special-toolbars"></a>特殊工具栏
 这些工具栏定义由 Visual Studio IDE，但它们提供专用的函数，并且未承载命令组。

|Toolbar|Id|
|-------------|--------|
|Add 命令|IDM_VS_TOOL_ADDCOMMAND|
|未定义|IDM_VS_TOOL_UNDEFINED|
|XML 架构|IDM_VS_TOOL_SCHEMA|
|XML 数据|IDM_VS_TOOL_DATA|

## <a name="groups-on-the-ide-toolbars"></a>在 IDE 工具栏上的组
 若要添加到标准工具栏按钮，设置作为其父级的以下组之一。 组将按在父级工具栏。

### <a name="standard-toolbar-groups"></a>标准工具栏组

|名称|Id|
|----------|--------|
|保存/打开|IDG_VS_TOOLSB_SAVEOPEN|
|剪切/复制|IDG_VS_TOOLSB_CUTCOPY|
|撤消/重做|IDG_VS_TOOLSB_UNDOREDO|
|运行/生成|IDG_VS_TOOLSB_RUNBUILD|
|搜索|IDG_VS_TOOLSB_SEARCH|
|Windows|IDG_VS_TOOLSB_WINDOWS|
|新的 windows|IDG_VS_TOOLSB_NEWWINDOWS|
|加载/保存|IDG_VS_WINDOWUI_LOADSAVE|
|仪表|IDG_VS_TOOLSB_GAUGE|

### <a name="build-toolbar-groups"></a>生成工具栏组

|名称|Id|
|----------|--------|
|生成栏|IDG_VS_BUILDBAR|
|取消|IDG_VS_BUILD_CANCEL|

### <a name="text-editor-toolbar-groups"></a>文本编辑器工具栏组

|名称|Id|
|----------|--------|
|完成|IDM_VS_TOOL_TEXTEDITOR|
|降级|IDG_VS_EDITTOOLBAR_INDENT|
|注释|IDG_VS_EDITTOOLBAR_COMMENT|
|书签|IDG_VS_EDITTOOLBAR_TEMPBOOKMARKS|

### <a name="debug-toolbar-groups"></a>调试工具栏组

|名称|Id|
|----------|--------|
|执行|IDM_DEBUG_TOOLBAR|
|单步执行|IDG_DEBUG_TOOLBAR_STEPPING|
|监视|IDG_DEBUG_TOOLBAR_WATCH|
|Windows|IDG_DEBUG_TOOLBAR_WINDOWS|

### <a name="debug-location-toolbar-groups"></a>调试位置工具栏组

|名称|Id|
|----------|--------|
|调试位置|IDG_DEBUG_CONTEXT_TOOLBAR|

## <a name="tool-window-toolbars"></a>工具窗口工具栏
 工具栏可以如出现在 IDE 中直接或工具窗口中**解决方案资源管理器**。 由于中未定义工具窗口 *.vsct*文件，工具窗口工具栏执行未定义父级。 相反，它们都放在代码中。 下表显示了在 IDE 中，工具窗口显示的工具栏和它们所包含的命令组。

> [!NOTE]
> 工具栏和组使用的 GUID `guidSHLMainMenu`，除外另行指定通过使用 guid: id 语法。 其中 GUID 指定一个工具栏，则它也适用于源自该工具栏的组中。

|工具窗口|Toolbar|组|
|-----------------|-------------|------------|
|“解决方案资源管理器”|IDM_VS_TOOL_PROJWIN|IDG_VS_PROJ_TOOLBAR1..5|
|服务器资源管理器|guid_SE_MenuGroup:IDM_SE_TOOLBAR_SERVEREXPLORER|IDG_SE_TOOLBAR_REFRESH|
|属性|IDM_VS_TOOL_PROPERTIES|IDG_VS_PROPERTIES_SORT<br /><br /> IDG_VS_PROPERTIES_PAGES|
|类视图|IDM_VS_TOOL_CLASSVIEW|IDG_VS_CLASSVIEW_FOLDERS<br /><br /> IDG_VS_CLASSVIEW_SEARCH<br /><br /> IDG_VS_CLASSVIEW_SETTINGS|
|类视图|IDM_VS_TOOL_CLASSVIEW_GO|IDG_VS_CLASSVIEW_SEARCH2|
|对象浏览器|IDM_VS_TOOL_OBJBROWSER|IDG_VS_OBJBROWSER_SUBSETS<br /><br /> IDG_VS_OBJBROWSER_SEARCH<br /><br /> IDG_VS_OBJBROWSER_ADDREFERENCE<br /><br /> IDG_VS_OBJBROWSER_BROWSERSETTINGS|
|对象浏览器|IDM_VS_TOOL_OBJECT_BROWSER_GO|IDG_VS_OBJBROWSER_SEARCH2|
|Output|IDM_VS_TOOL_OUTPUTWINDOW|IDG_VS_OUTPUTWINDOW_SELECT<br /><br /> IDG_VS_OUTPUTWINDOW_GOTO<br /><br /> IDG_VS_OUTPUTWINDOW_NEXTPREV<br /><br /> IDG_VS_OUTPUTWINDOW_CLEAR<br /><br /> IDG_VS_OUTPUTWINDOW_WORDWRAP|
|查找和替换|IDM_VS_TOOL_UNIFIEDFIND|IDG_VS_FINDTAB<br /><br /> IDG_VS_REPLACETAB|
|查找结果 1|IDM_VS_TOOL_FINDRESULTS1|IDG_VS_FINDRESULTS1_GOTO<br /><br /> IDG_VS_FINDRESULTS1_NEXTPREV<br /><br /> IDG_VS_FINDRESULTS1_CLEAR<br /><br /> IDG_VS_FINDRESULTS1_STOPFIND|
|查找结果 2|IDM_VS_TOOL_FINDRESULTS2|IDG_VS_FINDRESULTS2_GOTO<br /><br /> IDG_VS_FINDRESULTS2_NEXTPREV<br /><br /> IDG_VS_FINDRESULTS2_CLEAR<br /><br /> IDG_VS_FINDRESULTS2_STOPFIND|
|代码片段|IDM_VS_TOOL_SNIPPETMENUS|IDG_VS_SNIPPET_REPL<br /><br /> IDG_VS_SNIPPET_REF<br /><br /> IDG_VS_SNIPPET_PROP|
|书签|IDM_VS_TOOL_BOOKMARKWIND|IDG_VS_BWNEWFOLDER<br /><br /> IDG_VS_BWNEXTBM<br /><br /> IDG_VS_BWNEXTBMF<br /><br /> IDG_VS_BWENABLE<br /><br /> IDG_VS_BWDELETE|
|任务列表|IDM_VS_TOOL_TASKLIST|IDG_VS_TASKLIST_PROVIDERLIST|
|用户任务|IDM_VS_TOOL_USERTASKS|IDG_VS_TASKLIST_PROVIDERLIST<br /><br /> IDG_VS_USERTASKS_EDIT|
|错误列表|IDM_VS_TOOL_ERRORLIST|IDG_VS_ERRORLIST_ERRORGROUP<br /><br /> IDG_VS_ERRORLIST_WARNINGGROUP<br /><br /> IDG_VS_ERRORLIST_MESSAGEGROUP|
|调用浏览器|IDM_VS_TOOL_CALLBROWSER1..16|IDG_VS_TOOLBAR_CALLBROWSER1_ACTIONS<br /><br /> IDG_VS_TOOLBAR_CALLBROWSER1_TYPE<br /><br /> IDG_VS_TOOLBAR_CALLBROWSER1_CBSETTINGS|
|断点|guidVSDebugGroup:IDM_BREAKPOINTS_WINDOW_TOOLBAR|IDG_BREAKPOINTS_WINDOW_NEW<br /><br /> IDG_BREAKPOINTS_WINDOW_DELETE<br /><br /> IDG_BREAKPOINTS_WINDOW_ALL<br /><br /> IDG_BREAKPOINTS_WINDOW_VIEW<br /><br /> IDG_BREAKPOINTS_WINDOW_EDIT<br /><br /> IDG_BREAKPOINTS_WINDOW_COLUMNS|
|反汇编|guidVSDebugGroup:IDM_DISASM_WINDOW_TOOLBAR|IDG_DISASM_WINDOW_TOOLBAR|
|内存 1-4|guidVSDebugGroup:IDM_MEMORY_WINDOW_TOOLBAR1...4|IDG_MEMORY_EXPRESSION1..4<br /><br /> IDG_MEMORY_COLUMNS1..4|
|进程|guidVSDebugGroup:IDM_ATTACHED_PROCS_TOOLBAR|IDG_ATTACHED_PROCS_EXECCNTRL IDG_ATTACHED_PROCS_STEPPING<br /><br /> IDG_ATTACHED_PROCS_EXECCNTRL2<br /><br /> IDG_ATTACHED_PROCS_ATTACH<br /><br /> IDG_ATTACHED_PROCS_COLUMNS|

## <a name="see-also"></a>请参阅
- [将菜单控制器添加到工具栏](../../extensibility/adding-a-menu-controller-to-a-toolbar.md)
- [将工具栏添加到工具窗口](../../extensibility/adding-a-toolbar-to-a-tool-window.md)
- [Guid 和 Id 的 Visual Studio 菜单](../../extensibility/internals/guids-and-ids-of-visual-studio-menus.md)