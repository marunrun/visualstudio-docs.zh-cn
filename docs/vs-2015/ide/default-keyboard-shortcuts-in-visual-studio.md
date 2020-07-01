---
title: 默认键盘快捷键
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- shortcut keys [Visual Studio], keyboard binding schemes
- keyboard binding schemes [Visual Studio]
- Help [Visual Studio], shortcut keys
- keyboard shortcuts [Visual Studio], keyboard binding schemes
- keyboard shortcuts
ms.assetid: c2c64648-00f8-4e48-a8a0-96c67cfd968c
caps.latest.revision: 59
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 2fb9fa4d9c4faaf01ec64e9eb722af8589de5588
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85548091"
---
# <a name="default-keyboard-shortcuts-in-visual-studio"></a>Visual Studio 中的默认键盘快捷键
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

你可以通过选择相应的键盘快捷键，更轻松地访问 Visual Studio 中的各种命令和窗口。 本主题列出了常规开发配置文件的默认快捷键，你在安装 Visual Studio 时可能已选择该配置文件。 无论选择哪个配置文件，都可以通过打开“选项”**** 对话框，展开“环境”**** 节点，然后选择“键盘”****，认识命令的快捷方式。 你还可以为任意给定命令分配不同的快捷键，以自定义你的快捷键。

 有关常见键盘快捷键列表和其他工作效率信息，请参阅[提示和技巧](../ide/tips-and-tricks-for-visual-studio.md)和[工作效率提示](../ide/productivity-tips-for-visual-studio.md)。

 以下列表中的各部分包含全局命令，你可以使用键盘快捷方式从 Visual Studio 中的任何位置访问它们：

- [分析](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_analyze)
- [编辑](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_edit)
- [项目](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_project)
- [考试](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_test)|
- [体系结构](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_architecture)
- [编辑器上下文菜单](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_editorContext)
- [项目和解决方案上下文菜单](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_projectContext)
- [测试资源管理器](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_testexplorerGLOBAL)
- [生成](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_build)
- [文件](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_file)
- [重构](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_refactor)
- [工具](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_tools)
- [类视图上下文菜单](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_classview)
- [帮助](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_help)
- [解决方案资源管理器](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_solutionexplorerGLOBAL)
- [视图](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_view)
- [调试](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_debug)
- [负载测试](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_loadtest)
- [组](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_team)
- [Window](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_window)
- [调试器上下文菜单](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_debugger)
- [其他上下文菜单](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_otherContext)
- [Team Foundation 上下文菜单](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_TFcontext)
- [Azure](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_windowsazure)
- [诊断中心](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_diagnostics)

 以下列表中的每一节都包含一些命令，这些命令的键盘快捷键特定于其命名节所针对的上下文。

- [ADO.NET 实体数据模型设计器](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_ADONET)
- [层关系图](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_layerDiagram)
- [设置设计器](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_SettingsDesigner)
- [VC 图像编辑器](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_vcimageeditor)
- [类图](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_classDiagram)
- [托管资源编辑器](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_managedResources)
- [解决方案资源管理器](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_SolutionExplorer)
- [VC 字符串编辑器](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_vcstringeditor)
- [编码的 UI 测试编辑器](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_codedUItest)
- [合并编辑器窗口](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_MergeEditor)
- [团队资源管理器](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_TeamExplorer)
- [视图设计器](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_viewDesigner)
- [数据集编辑器](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_dataset)
- [Microsoft SQL Server Data Tools，架构比较](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_SchemaCompare)
- [Team Foundation Build 详细信息编辑器](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_TFBuild)
- [Visual Studio](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_visualstudio)
- [差异查看器](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_diff)
- [Microsoft SQL Server Data Tools，表设计器](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_TableDesigner)
- [测试资源管理器](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_TestExplorer)
- [Windows Forms Designer — Windows 窗体设计器](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_wfdesigner)
- [DOM 资源管理器](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_DOM)
- [Microsoft SQL Server Data Tools，T-sql 编辑器](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_TSQLeditor)
- [文本编辑器](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_TextEditor)
- [工作项编辑器](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_workItemEditor)
- [F# Interactive](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_FSharp)
- [Microsoft SQL Server Data Tools，T-SQL PDW 编辑器](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_linkfix)
- [UML 活动图](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_UMLactivityDiagram)
- [工作项查询视图](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_WIqueryview)
- [关系图文档编辑器](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_graphDoc)
- [Page Inspector](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_PageInspector)
- [UML 类图](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_UMLclassDiagram)
- [工作项结果视图](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_WIresultsview)
- [图形诊断](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_graphicsDebugger)
- [查询设计器](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_QueryDesigner)
- [UML 组件图](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_UMLcomponentDiagram)
- [工作流设计器](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_workflowdesigner)
- [HTML 编辑器](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_HTMLeditor)
- [查询结果](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_QueryResults)
- [UML 用例图](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_UMLusecaseDiagram)
- [XAML 设计器](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_xamluidesigner)
- [HTML 编辑器设计视图](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_HTMLeditorDesign)
- [报表设计器](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_ReportDesigner)
- [VC 快捷键编辑器](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_vcaccelerator)
- [XML（文本）编辑器](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_xmlTextEditor)
- [HTML 编辑器源视图](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_HTMLeditorSource)
- [序列图](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_SequenceDiagram)
- [VC 对话框编辑器](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_vcdialogeditor)
- [XML 架构设计器](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_xmlSchemaDesigner)

## <a name="global"></a><a name="bkmk_global"></a>全局

### <a name="analyze"></a><a name="bkmk_analyze"></a>旁

|命令|键盘快捷键|
|--------------|------------------------|
|分析.向后定位|Shift+Alt+3|
|分析.向前定位|Shift+Alt+4|

### <a name="architecture"></a><a name="bkmk_architecture"></a>种

|命令|键盘快捷键|
|--------------|------------------------|
|体系结构.新建关系图|Ctrl+\\、Ctrl+N|

### <a name="build"></a><a name="bkmk_build"></a>构造

|命令|键盘快捷键|
|--------------|------------------------|
|生成.生成解决方案|Ctrl+Shift+B|
|生成.取消|Ctrl+Break|
|生成.编译|Ctrl+F7|
|生成.对解决方案运行代码分析|Alt+F11|

### <a name="class-view-context-menus"></a><a name="bkmk_classview"></a>类视图上下文菜单

|命令|键盘快捷键|
|--------------|------------------------|
|类视图上下文菜单.类视图多选项目引用项.属性|Alt+Enter|

### <a name="debug"></a><a name="bkmk_debug"></a>Debug.exe

|命令|键盘快捷键|
|--------------|------------------------|
|调试.应用代码更改|Alt+F10|
|调试.自动窗口|Ctrl+Alt+V、A|
|调试.全部中断|Ctrl+Alt+Break|
|调试.在函数处中断|Ctrl+B|
|调试.断点|Ctrl+Alt+B|
|调试.调用堆栈|Ctrl+Alt+C|
|调试.删除所有断点|Ctrl+Shift+F9|
|调试.诊断中心.启动|Alt+F2|
|调试.反汇编|Ctrl+Alt+D|
|调试.DOM 资源管理器|Ctrl+Alt+V、D|
|调试.启用断点|Ctrl+F9|
|调试.异常|Ctrl+Alt+E|
|调试.转到上一个调用或 IntelliTrace 事件|Ctrl+Shift+F11|
|调试.图形.启动诊断|Alt+F5|
|调试.即时|Ctrl+Alt+I|
|调试.IntelliTrace 调用|Ctrl+Alt+Y、T|
|调试.IntelliTrace 事件|Ctrl+Alt+Y、F|
|调试.JavaScript 控制台|Ctrl+Alt+V、C|
|调试.局部变量|Ctrl+Alt+V、L|
|调试.位置工具栏.进程组合框|Ctrl+5|
|调试.位置工具栏.堆栈帧组合框|Ctrl+7|
|调试.位置工具栏.线程组合框|Ctrl+6|
|调试.位置工具栏.切换当前线程标志状态|Ctrl+8|
|调试.位置工具栏.切换标记的线程|Ctrl+9|
|调试.内存1|Ctrl+Alt+M、1|
|调试.内存2|Ctrl+Alt+M、2|
|调试.内存3|Ctrl+Alt+M、3|
|调试.内存4|Ctrl+Alt+M、4|
|调试.模块|Ctrl+Alt+U|
|调试.并行堆栈|Ctrl+Shift+D、S|
|调试.并行监视 1|Ctrl+Shift+D、1|
|调试.并行监视 2|Ctrl+Shift+D、2|
|调试.并行监视 3|Ctrl+Shift+D、3|
|调试.并行监视 4|Ctrl+Shift+D、4|
|调试.进程|Ctrl+Alt+Z|
|调试.快速监视|Shift+F9<br /><br /> 或<br /><br /> Ctrl+Alt+Q|
|Debug.RefreshWindowsapp|Ctrl+Shift+R|
|调试.寄存器|Ctrl+Alt+G|
|调试.重新启动|Ctrl+Shift+F5|
|调试.运行到光标处|Ctrl+F10|
|调试.设置下一语句|Ctrl+Shift+F10|
|调试.在代码图上显示调用堆栈|Ctrl+Shift+`|
|调试.显示下一语句|Alt+Num *|
|调试.启动|F5|
|调试.启动 Windows Phone 应用程序分析|Alt+F1|
|调试.开始执行不调试|Ctrl+F5|
|调试.逐语句|F11|
|调试.进入并单步执行当前进程|Ctrl+Alt+F11|
|调试.单步执行特定函数|Shift+Alt+F11|
|调试.跳出|Shift+F11|
|调试.跳出当前进程|Ctrl+Shift+Alt+F11|
|调试.逐过程|F10|
|调试.逐过程执行当前进程|Ctrl+Alt+F10|
|调试.停止调试|Shift+F5|
|调试.停止性能分析|Shift+Alt+F2|
|调试.任务|Ctrl+Shift+D、K|
|调试.线程|Ctrl+Alt+H|
|调试.切换断点|F9|
|调试.切换反汇编|Ctrl+F11|
|调试.监视 1|Ctrl+Alt+W、1|
|调试.监视2|Ctrl+Alt+W、2|
|调试.监视3|Ctrl+Alt+W、3|
|调试.监视4|Ctrl+Alt+W、4|

### <a name="debugger-context-menus"></a><a name="bkmk_debugger"></a>调试器上下文菜单

|命令|键盘快捷键|
|--------------|------------------------|
|调试器上下文菜单.断点窗口.删除|Alt+F9、D|
|调试器上下文菜单.断点窗口.转到反汇编|Alt+F9、A|
|调试器上下文菜单.断点窗口.转到源代码|Alt+F9、S|

### <a name="diagnostics-hub"></a><a name="bkmk_diagnostics"></a>诊断中心

|Command|键盘快捷方式|
|-------------|-----------------------|
|诊断中心.停止收集|Ctrl+Alt+F2|

### <a name="edit"></a><a name="bkmk_edit"></a>编辑

|命令||
|--------------|-|
|编辑.复制|Ctrl+C<br /><br /> 或<br /><br /> Ctrl+Ins|
|编辑.剪切|Ctrl+X<br /><br /> 或<br /><br /> Shift+Delete|
|编辑.循环应用剪贴板中的复制项|Ctrl+Shift+V<br /><br /> 或<br /><br /> Ctrl+Shift+Ins|
|编辑.删除|删除|
|编辑.查找|Ctrl+F|
|编辑.查找所有引用|Shift+F12|
|编辑.在文件中查找|Ctrl+Shift+F|
|编辑.查找下一个|F3|
|编辑.查找下一个选定项|Ctrl+F3|
|编辑.查找上一个|Shift+F3|
|编辑.查找上一个选定项|Ctrl+Shift+F3|
|编辑.生成方法|Ctrl+K、Ctrl+M|
|编辑.转到|Ctrl+G|
|编辑.转到声明|Ctrl+F12|
|编辑.转到定义|F12|
|编辑.转到查找组合框|Ctrl+D|
|编辑.转到下一个位置|F8|
|编辑.转到上一个位置|Shift+F8|
|编辑.插入代码片段|Ctrl+K、Ctrl+X|
|编辑.下移控件|Ctrl+向下键|
|编辑.将控件移动到下侧网格|向下键|
|编辑.左移控件|Ctrl+向左键|
|编辑.将控件移动到左侧网格|向左键|
|编辑.右移控件|Ctrl+向右键|
|编辑.将控件移动到右侧网格|向右键|
|编辑.上移控件|Ctrl+向上键|
|编辑.将控件移动到上侧网格|向上键|
|Edit.NavigateTo|Ctrl+,|
|编辑.下一书签|Ctrl+K、Ctrl+N|
|编辑.文件夹中的下一书签|Ctrl+Shift+K、Ctrl+Shift+N|
|编辑.打开文件|Ctrl+Shift+G|
|编辑.粘贴|Ctrl+V<br /><br /> 或<br /><br /> Shift+Ins|
|编辑.上一书签|Ctrl+K、Ctrl+P|
|编辑.文件夹中的上一书签|Ctrl+Shift+K、Ctrl+Shift+P|
|编辑.快速查找符号|Shift+Alt+F12|
|编辑.重做|Ctrl+Y<br /><br /> 或<br /><br /> Ctrl+Shift+Z<br /><br /> 或<br /><br /> Shift+Alt+Backspace|
|编辑.刷新远程引用|Ctrl+Shift+J|
|编辑.替换|Ctrl+H|
|编辑.在文件中替换|Ctrl+Shift+H|
|编辑.全选|Ctrl+A|
|编辑.选择下一个控件|选项卡|
|编辑.选择上一个控件|Shift+Tab|
|编辑.显示平铺网格|Enter|
|编辑.向下调大控件大小|Ctrl+Shift+向下键|
|编辑.将控件调大到下侧网格|Shift+向下键|
|编辑.向左调整控件大小|Ctrl+Shift+向左键|
|编辑.将控件调大到左侧网格|Shift+向左键|
|编辑.向右调整控件大小|Ctrl+Shift+向右键|
|编辑.将控件调大到右侧网格|Shift+向右键|
|编辑.向上调整控件大小|Ctrl+Shift+向上键|
|编辑.将控件调大到上侧网格|Shift+向上键|
|编辑.停止搜索|Alt+F3、S|
|编辑.外侧代码|Ctrl+K、Ctrl+S|
|编辑.取消|Ctrl+Z<br /><br /> 或<br /><br /> Alt+Backspace|

### <a name="editor-context-menus"></a><a name="bkmk_editorContext"></a>编辑器上下文菜单

|命令|键盘快捷键|
|--------------|------------------------|
|编辑器上下文菜单.代码窗口.断点.断点编辑标签|Alt+F9、L|
|编辑器上下文菜单.代码窗口.代码图.显示项|Ctrl+`|
|编辑器上下文菜单.代码窗口.执行|Ctrl+Alt+F5|
|编辑器上下文菜单.代码窗口.转到视图|Ctrl+M、Ctrl+G|
|编辑器上下文菜单.代码窗口.切换标头代码文件|Ctrl+K、Ctrl+O|
|编辑器上下文菜单.代码窗口.查看调用层次结构|Ctrl+K、Ctrl+T<br /><br /> 或<br /><br /> Ctrl+K、T|

### <a name="file"></a><a name="bkmk_file"></a>文件

|命令|键盘快捷键|
|--------------|------------------------|
|文件.退出|Alt+F4|
|文件.新建文件|Ctrl+N|
|文件.新建项目|Ctrl+Shift+N|
|文件.新建网站|Shift+Alt+N|
|文件.打开文件|Ctrl+O|
|文件.打开项目|Ctrl+Shift+O|
|文件.打开网站|Shift+Alt+O|
|文件.打印|Ctrl+P|
|文件.全部保存|Ctrl+Shift+S|
|文件.保存选定项|Ctrl+S|
|文件.在浏览器中查看|Ctrl+Shift+W|

### <a name="help"></a><a name="bkmk_help"></a>帮助

|命令|键盘快捷键|
|--------------|------------------------|
|帮助.添加和移除帮助内容|Ctrl+Alt+F1|
|帮助.F1 帮助|F1|
|Help.ViewHelp|Ctrl+F1|
|帮助.窗口帮助|Shift+F1|

### <a name="load-test"></a><a name="bkmk_loadtest"></a>负载测试

|Command|键盘快捷方式|
|-------------|-----------------------|
|负载测试.跳至计数器窗格|Ctrl+R、Q|

### <a name="other-context-menus"></a><a name="bkmk_otherContext"></a>其他上下文菜单

|Command|键盘快捷方式|
|-------------|-----------------------|
|其他上下文菜单.Microsoft 数据实体设计上下文.添加新关系图|插入|

### <a name="project"></a><a name="bkmk_project"></a>项目

|命令|键盘快捷键|
|--------------|------------------------|
|项目.添加现有项|Shift+Alt+A|
|项目.添加新项|Ctrl+Shift+A|
|项目.类向导|Ctrl+Shift+X|
|项目.重写|Ctrl+Alt+Ins|
|项目.预览更改|Alt+;、Alt+C|
|项目.发布选定文件|Alt+;、Alt+P|
|项目.替换服务器上的选定文件|Alt+;、Alt+R|

### <a name="project-and-solution-context-menus"></a><a name="bkmk_projectContext"></a>项目和解决方案上下文菜单

|命令|键盘快捷键|
|--------------|------------------------|
|项目和解决方案上下文菜单.项.下移|Alt+向下键|
|项目和解决方案上下文菜单.项.上移|Alt+向上键|

### <a name="refactor"></a><a name="bkmk_refactor"></a>重构

|命令|键盘快捷键|
|--------------|------------------------|
|重构.封装字段|Ctrl+R、Ctrl+E|
|重构.提取接口|Ctrl+R、Ctrl+I|
|重构.提取方法|Ctrl+R、Ctrl+M|
|重构.移除参数|Ctrl+R、Ctrl+V|
|重构.重命名|Ctrl+R、Ctrl+R|
|重构.重新排列参数|Ctrl+R、Ctrl+O|

### <a name="solution-explorer"></a><a name="bkmk_solutionexplorerGLOBAL"></a>解决方案资源管理器

|命令|键盘快捷键|
|--------------|------------------------|
|解决方案资源管理器.打开文件筛选器|Ctrl+[、O<br /><br /> 或<br /><br /> Ctrl+[、Ctrl+O|
|解决方案资源管理器.挂起更改筛选器|Ctrl+[、P<br /><br /> 或<br /><br /> Ctrl+[、Ctrl+P|
|解决方案资源管理器.与活动文档同步|Ctrl+[、S<br /><br /> 或<br /><br /> Ctrl+[、Ctrl+S|

### <a name="team"></a><a name="bkmk_team"></a>项目

|命令|键盘快捷键|
|--------------|------------------------|
|团队.Git.转到 Git 分支|Ctrl+0、Ctrl+N<br /><br /> 或<br /><br /> Ctrl+0、N|
|团队.Git.转到 Git 更改|Ctrl+0、Ctrl+G<br /><br /> 或<br /><br /> Ctrl+0、G|
|团队.Git.转到 Git 提交|Ctrl+0、Ctrl+O<br /><br /> 或<br /><br /> Ctrl+0、O|
|团队.团队资源管理器搜索|Ctrl+'|

### <a name="team-foundation-context-menus"></a><a name="bkmk_TFcontext"></a>Team Foundation 上下文菜单

|命令|键盘快捷键|
|--------------|------------------------|
|Team Foundation 上下文菜单.命令.转到生成|Ctrl+0、Ctrl+B<br /><br /> 或<br /><br /> Ctrl+0、B|
|Team Foundation 上下文菜单.命令.转到连接|Ctrl+0、Ctrl+C<br /><br /> 或<br /><br /> Ctrl+0、C|
|Team Foundation 上下文菜单.命令.转到文档|Ctrl+0、Ctrl+D<br /><br /> 或<br /><br /> Ctrl+0、D|
|Team Foundation 上下文菜单.命令.转到主页|Ctrl+0、Ctrl+H<br /><br /> 或<br /><br /> Ctrl+0、H|
|Team Foundation 上下文菜单.命令.转到我的工作|Ctrl+0、Ctrl+M<br /><br /> 或<br /><br /> Ctrl+0、M|
|Team Foundation 上下文菜单.命令.转到挂起的更改|Ctrl+0、Ctrl+P<br /><br /> 或<br /><br /> Ctrl+0、P|
|Team Foundation 上下文菜单.命令.转到报告|Ctrl+0、Ctrl+R<br /><br /> 或<br /><br /> Ctrl+0、R|
|Team Foundation 上下文菜单.命令.转到设置|Ctrl+0、Ctrl+S<br /><br /> 或<br /><br /> Ctrl+0、S|
|Team Foundation 上下文菜单.命令.转到 Web 访问|Ctrl+0、Ctrl+A<br /><br /> 或<br /><br /> Ctrl+0、A|
|Team Foundation 上下文菜单.命令.转到工作项|Ctrl+0、Ctrl+W<br /><br /> 或<br /><br /> Ctrl+0、W|

### <a name="test"></a><a name="bkmk_test"></a>考试

|命令|键盘快捷键|
|--------------|------------------------|
|测试.使用编码的 UI 测试生成器|Ctrl+\\、Ctrl+C|
|测试.使用现有的操作录制|Ctrl+\\、Ctrl+A|

### <a name="test-explorer"></a><a name="bkmk_testexplorerGLOBAL"></a>测试资源管理器

|命令|键盘快捷键|
|--------------|------------------------|
|测试资源管理器.调试所有测试|Ctrl+R、Ctrl+A|
|测试资源管理器.调试上下文中的所有测试|Ctrl+R、Ctrl+T|
|测试资源管理器.重复上次运行|Ctrl+R、L|
|测试资源管理器.运行所有测试|Ctrl+R、Ａ|
|测试资源管理器.运行上下文中的所有测试|Ctrl+R、T|

### <a name="tools"></a><a name="bkmk_tools"></a> 工具

|命令|键盘快捷键|
|--------------|------------------------|
|工具.附加到进程|Ctrl+Alt+P|
|工具.代码段管理器|Ctrl+K、Ctrl+B|
|工具.强制 GC|Ctrl+Shift+Alt+F12、Ctrl+Shift+Alt+F12|
|工具.转到命令行|Ctrl+/|

### <a name="view"></a><a name="bkmk_view"></a>显示

|命令|键盘快捷键|
|--------------|------------------------|
|视图.所有窗口|Shift+Alt+M|
|视图.体系结构资源管理器|Ctrl+\\、Ctrl+R|
|视图.向后|Alt + 向左键|
|视图.书签窗口|Ctrl+K、Ctrl+W|
|视图.浏览下一个|Ctrl+Shift+1|
|视图.浏览上一个|Ctrl+Shift+2|
|视图.调用层次结构|Ctrl+Alt+K|
|视图.类视图|Ctrl+Shift+C|
|视图.类视图转到搜索组合框|Ctrl+K、Ctrl+V|
|视图.代码定义窗口|Ctrl+\\、D<br /><br /> 或<br /><br /> Ctrl+\\、Ctrl+D|
|视图.命令窗口|Ctrl+Alt+A|
|View.DataSources|Shift+Alt+D|
|视图.文档大纲|Ctrl+Alt+T|
|视图.编辑标签|F2|
|视图.错误列表|Ctrl+\\、E<br /><br /> 或<br /><br /> Ctrl+\\、Ctrl+E|
|视图.F# Interactive|Ctrl+Alt+F|
|视图.查找符号结果|Ctrl+Alt+F12|
|视图.向前|Alt + 向右键|
|视图.向前浏览上下文|Ctrl+Shift+7|
|视图.全屏|Shift+Alt+Enter|
|视图.向后定位|Ctrl+-|
|视图.向前定位|Ctrl+Shift+-|
|视图.下一个错误|Ctrl+Shift+F12|
|视图.通知|Ctrl+W、N<br /><br /> 或<br /><br /> Ctrl+W、Ctrl+N|
|视图.对象浏览器|Ctrl+Alt+J|
|视图.对象浏览器转到搜索组合框|Ctrl+K、Ctrl+R|
|视图.输出|Ctrl+Alt+O|
|视图.弹出浏览上下文|Ctrl+Shift+8|
|视图.属性窗口|F4|
|视图.属性页|Shift+F4|
|视图.资源视图|Ctrl+Shift+E|
|视图.服务器资源管理器|Ctrl+Alt+S|
|视图.显示智能标记|Shift+Alt+F10<br /><br /> 或<br /><br /> Ctrl+.|
|视图.解决方案资源管理器|Ctrl+Alt+L|
|视图.SQL Server 对象浏览器|Ctrl+\\、Ctrl+S|
|视图.任务列表|Ctrl+\\、T<br /><br /> 或<br /><br /> Ctrl+\\、Ctrl+T|
|视图.Tfs 团队资源管理器|Ctrl+\\、Ctrl+M|
|视图.工具箱|Ctrl+Alt+X|
|视图.UML 模型资源管理器|Ctrl+\\、Ctrl+U|
|视图.查看代码|F7|
|视图.视图设计器|Shift+F7|
|视图.Web浏览器|Ctrl+Alt+R|
|视图.放大|Ctrl+Shift+.|
|视图.缩小|Ctrl+Shift+,|

### <a name="window"></a><a name="bkmk_window"></a>窗口

|命令|键盘快捷键|
|--------------|------------------------|
|窗口.激活文档窗口|Esc|
|窗口.将选项卡添加到所选内容|Ctrl+Shift+Alt+空格键|
|窗口.关闭文档窗口|Ctrl+F4|
|窗口.关闭工具窗口|Shift+Esc|
|窗口.将选项卡保持打开状态|Ctrl+Alt+Home|
|窗口.移动到导航栏|Ctrl+F2|
|窗口.下一个文档窗口|Ctrl+F6|
|窗口.下一个文档窗口导航栏|Ctrl+Tab|
|窗口.下一窗格|Alt+F6|
|窗口.下一个拆分窗格|F6|
|窗口.下一选项卡|Ctrl+Alt+PgDn<br /><br /> 或<br /><br /> Ctrl+PgDn|
|Window.NextTabandAddtoSelection|Ctrl+Shift+Alt+PgDn|
|窗口.下一个工具窗口导航栏|Alt+F7|
|窗口.上一个文档窗口|Ctrl+Shift+F6|
|窗口.上一个文档窗口导航栏|Ctrl+Shift+Tab|
|窗口.上一窗格|Shift+Alt+F6|
|窗口.上一个拆分窗格|Shift+F6|
|窗口.上一选项卡|Ctrl+Alt+PgUp<br /><br /> 或<br /><br /> Ctrl+PgUp|
|Window.PreviousTabandAddtoSelection|Ctrl+Shift+Alt+PgUp|
|窗口.上一个工具窗口导航栏|Shift+Alt+F7|
|窗口.快速启动|Ctrl+Q|
|窗口.快速启动以前分类|Ctrl+Shift+Q|
|窗口.显示停靠菜单|Alt+-|
|窗口.显示EzMDI文件列表|Ctrl+Alt+向下键|
|窗口.解决方案资源管理器搜索|Ctrl+;|
|窗口.窗口搜索|Alt+`|

### <a name="azure"></a><a name="bkmk_windowsazure"></a>Microsoft

|命令|键盘快捷键|
|--------------|------------------------|
|WindowsAzure.重试移动服务脚本操作|Ctrl+Num *、Ctrl+R|
|WindowsAzure.显示移动服务脚本错误详细信息|Ctrl+Num *、Ctrl+D|

## <a name="adonet-entity-data-model-designer"></a><a name="bkmk_ADONET"></a>ADO.NET 实体数据模型设计器

|命令|键盘快捷键|
|--------------|------------------------|
|其他上下文菜单.Microsoft 数据实体设计上下文.移动属性.向下|Alt+向下键|
|其他上下文菜单.Microsoft 数据实体设计上下文.移动属性.向下 5|Alt+PgDn|
|其他上下文菜单.Microsoft 数据实体设计上下文.移动属性.到底部|Alt+End|
|其他上下文菜单.Microsoft 数据实体设计上下文.移动属性.到顶部|Alt+Home|
|其他上下文菜单.Microsoft 数据实体设计上下文.移动属性.向上|Alt+向上键|
|其他上下文菜单.Microsoft 数据实体设计上下文.移动属性.向上 5|Alt+PgUp|
|其他上下文菜单.Microsoft 数据实体设计上下文.重构.重命名|Ctrl+R、R|
|其他上下文菜单.Microsoft 数据实体设计上下文.从关系图中移除|Shift+Del|
|视图.实体数据模型资源浏览器|Ctrl+1|
|视图.实体数据模型映射详细信息|Ctrl+2|

## <a name="class-diagram"></a><a name="bkmk_classDiagram"></a>类图

|命令|键盘快捷键|
|--------------|------------------------|
|类图.折叠|Num -|
|类图.展开|Num +|
|编辑.删除|Ctrl+Del|
|编辑.展开折叠基类型列表|Shift+Alt+B|
|编辑.定位到棒糖形|Shift+Alt+L|
|编辑.从关系图中移除|删除|
|视图.查看代码|Enter|

## <a name="coded-ui-test-editor"></a><a name="bkmk_codedUItest"></a>编码的 UI 测试编辑器

|命令|键盘快捷键|
|--------------|------------------------|
|其他上下文菜单.UI 测试编辑器上下文菜单.将引用复制到剪贴板|Ctrl+C|
|其他上下文菜单.UI 测试编辑器上下文菜单.在前面插入延迟|Ctrl+Alt+D|
|其他上下文菜单.UI 测试编辑器上下文菜单.查找全部|Shift+Alt+L|
|其他上下文菜单.UI 测试编辑器上下文菜单.查找 UI 控件|Ctrl+Shift+L|
|其他上下文菜单.UI 测试编辑器上下文菜单.移动代码|Ctrl+Alt+C|
|其他上下文菜单.UI 测试编辑器上下文菜单.拆分成新方法|Ctrl+Shift+T|

## <a name="dataset-editor"></a><a name="bkmk_dataset"></a>数据集编辑器

|命令|键盘快捷键|
|--------------|------------------------|
|OtherContextMenus.ColumnContext.InsertColumn|插入|
|OtherContextMenus.DbTableContext.Add.Column|Ctrl+L|

## <a name="difference-viewer"></a><a name="bkmk_diff"></a>差异查看器

|命令|键盘快捷键|
|-|-|
|差异.忽略修整空白|Ctrl+\\、Ctrl+空格键|
|差异.内联视图|Ctrl+\\、Ctrl+1|
|差异.仅左视图|Ctrl+\\、Ctrl+3|
|差异.下一个差异|F8|
|差异.上一个差异|Shift+F8|
|差异.仅右视图|Ctrl+\\、Ctrl+4|
|差异.并列视图|Ctrl+\\、Ctrl+2|
|差异.在左视图和右视图之间切换|Ctrl+\\、Ctrl+Tab|
|差异.同步视图切换|Ctrl+\\、Ctrl+向下键|
|编辑器上下文菜单.代码窗口.添加注释|Ctrl+Shift+K|
|编辑器上下文菜单.代码窗口.编辑本地文件|Ctrl+Shift+P|

## <a name="dom-explorer"></a><a name="bkmk_DOM"></a>DOM 资源管理器

|命令|键盘快捷键|
|--------------|------------------------|
|DOM 资源管理器.刷新|F5|
|DOM 资源管理器.选择元素|Ctrl+B|
|DOM 资源管理器.显示布局|Ctrl+Shift+I|

## <a name="f-interactive"></a><a name="bkmk_FSharp"></a>F# 交互窗口

|Command|键盘快捷方式|
|-------------|-----------------------|
|其他上下文菜单.FSI 控制台上下文.取消交互评估|Ctrl+Break|

## <a name="graph-document-editor"></a><a name="bkmk_graphDoc"></a>关系图文档编辑器

|命令|键盘快捷键|
|--------------|------------------------|
|体系结构上下文菜单.定向关系图上下文菜单.高级.添加.添加节点|插入|
|体系结构上下文菜单.定向关系图上下文菜单.高级.选择.两个依赖项|B|
|体系结构上下文菜单.定向关系图上下文菜单.高级.选择.传入依赖项|I|
|体系结构上下文菜单.定向关系图上下文菜单.高级.选择.传出依赖项|O|
|体系结构上下文菜单.定向关系图上下文菜单.新注释|Ctrl+Shift+K<br /><br /> 或<br /><br /> Ctrl+E、C|
|体系结构上下文菜单.定向关系图上下文菜单.删除|删除|
|体系结构上下文菜单.定向关系图上下文菜单.重命名|F2|

## <a name="graphics-diagnostics"></a><a name="bkmk_graphicsDebugger"></a>图形诊断

|命令|键盘快捷键|
|--------------|------------------------|
|调试.图形.捕获帧|无|
|Graphics.MovePixelSelectionDown|Shift+Alt+向下键|
|Graphics.MovePixelSelectionLeft|Shift+Alt+向左键|
|Graphics.MovePixelSelectionRight|Shift+Alt+向右键|
|Graphics.MovePixelSelectionUp|Shift+Alt+向上键|
|Graphics.ZoomToActualSize|Shift+Alt+0|
|Graphics.ZoomToFitInWindow|Shift+Alt+9|
|Graphics.ZoomIn|Shift+Alt+=|
|Graphics.ZoomOut|Shift+Alt+-|

## <a name="html-editor"></a><a name="bkmk_HTMLeditor"></a>HTML 编辑器

|Command|键盘快捷方式|
|-------------|-----------------------|
|其他上下文菜单.HTML 上下文.转到控制器|Ctrl+M、Ctrl+G|

## <a name="html-editor-design-view"></a><a name="bkmk_HTMLeditorDesign"></a>HTML 编辑器设计视图

|命令|键盘快捷键|
|--------------|------------------------|
|编辑.下移控件|Ctrl+向下键|
|编辑.上移控件|Ctrl+向上键|
|格式.粗体|Ctrl+B|
|格式.转换为超链接|Ctrl+L|
|格式.插入书签|Ctrl+Shift+L|
|格式.斜体|Ctrl+I|
|格式.下划线|Ctrl+U|
|项目.添加内容页|Ctrl+M、Ctrl+C|
|表.左侧列|Ctrl+Alt+向左键|
|表.右侧列|Ctrl+Alt+向右键|
|表.上面的行|Ctrl+Alt+向上键|
|表.下面的行|Ctrl+Alt+向下键|
|视图.ASP.NET 非可视控件|Ctrl+Shift+N|
|视图.编辑主表|Ctrl+M、Ctrl+M|
|视图.下一个视图|Ctrl+PgDn|
|视图.显示智能标记|Shift+Alt+F10|
|视图.查看标记|Shift+F7|
|窗口.上一选项卡|Ctrl+PgUp|

## <a name="html-editor-source-view"></a><a name="bkmk_HTMLeditorSource"></a>HTML 编辑器源视图

|命令|键盘快捷键|
|--------------|------------------------|
|其他上下文菜单.HTML 上下文.转到控制器|Ctrl+M、Ctrl+G|
|视图.下一个视图|Ctrl+PgDn|
|视图.同步视图|Ctrl+Shift+Y|
|视图.视图设计器|Shift+F7|
|窗口.上一选项卡|Ctrl+PgUp|

## <a name="layer-diagram"></a><a name="bkmk_layerDiagram"></a>层关系图

|Command|键盘快捷方式|
|-------------|-----------------------|
|编辑.删除|Shift+Delete|

## <a name="managed-resources-editor"></a><a name="bkmk_managedResources"></a>托管资源编辑器

|命令|键盘快捷键|
|--------------|------------------------|
|编辑.编辑单元格|F2|
|编辑.移除|删除|
|编辑.移除行|Ctrl+Delete|
|编辑.取消选定|Escape|
|资源.音频|Ctrl+4|
|资源.文件|Ctrl+5|
|资源.图标|Ctrl+3|
|资源.图像|Ctrl+2|
|资源.其他|Ctrl+6|
|资源.字符串|Ctrl+1|

## <a name="merge-editor-window"></a><a name="bkmk_MergeEditor"></a>合并编辑器窗口

|命令|键盘快捷键|
|--------------|------------------------|
|Team Foundation 上下文菜单.合并上下文菜单.在左侧窗口上设置焦点|Alt+1|
|Team Foundation 上下文菜单.合并上下文菜单.在结果窗口上设置焦点|Alt+2|
|Team Foundation 上下文菜单.合并上下文菜单.在右侧窗口上设置焦点|Alt+3|

## <a name="microsoft-sql-server-data-tools-schema-compare"></a><a name="bkmk_SchemaCompare"></a>Microsoft SQL Server Data Tools，架构比较

|命令|键盘快捷键|
|--------------|------------------------|
|SQL.SSDT 架构比较比较|Shift+Alt+C|
|SQL.SSDT 架构比较生成脚本|Shift+Alt+G|
|SQL.SSDT 架构比较下一个更改|Shift+Alt+.|
|SQL.SSDT 架构比较上一个更改|Shift+Alt+,|
|SQL.SSDT 架构比较停止|Alt+Break|
|SQL.SSDT 架构比较写入更新|Shift+Alt+U|

## <a name="microsoft-sql-server-data-tools-table-designer"></a><a name="bkmk_TableDesigner"></a>Microsoft SQL Server Data Tools，表设计器

|命令|键盘快捷键|
|--------------|------------------------|
|提交所有编辑|Shift+Alt+U|
|SQL.展开通配符|Ctrl+R、E<br /><br /> or<br /><br /> Ctrl+R、Ctrl+E|
|SQL.完全限定名称|Ctrl+R、Q<br /><br /> or<br /><br /> Ctrl+R、Ctrl+Q|
|SQL.移至架构|Ctrl+R、M<br /><br /> or<br /><br /> Ctrl+R、Ctrl+M|
|SQL.重命名|F2<br /><br /> 或<br /><br /> Ctrl+R、R<br /><br /> 或<br /><br /> Ctrl+R、Ctrl+R|
|在脚本面板中查看文件|Shift+Alt+PgDn|

## <a name="microsoft-sql-server-data-tools-t-sql-editor"></a><a name="bkmk_TSQLeditor"></a>Microsoft SQL Server Data Tools，T-SQL 编辑器

|命令|键盘快捷键|
|--------------|------------------------|
|提交所有编辑|Shift+Alt+U|
|SQL.使用调试器执行|Alt+F5|
|SQL.展开通配符|Ctrl+R、E<br /><br /> 或<br /><br /> Ctrl+R、Ctrl+E|
|SQL.完全限定名称|Ctrl+R、Q<br /><br /> 或<br /><br /> Ctrl+R、Ctrl+Q|
|SQL.移至架构|Ctrl+R、M<br /><br /> 或<br /><br /> Ctrl+R、Ctrl+M|
|SQL.重命名|F2<br /><br /> 或<br /><br /> Ctrl+R、R<br /><br /> 或<br /><br /> Ctrl+R、Ctrl+R|
|SQL.TSql 编辑器取消查询|Alt+Break|
|SQL.TSql 编辑器执行查询|Ctrl+Shift+E|
|SQL.TSql 编辑器结果显示为文件|Ctrl+D、F|
|SQL.TSql 编辑器结果显示为网格|Ctrl+D、G|
|SQL.TSql 编辑器结果显示为文本|Ctrl+D、T|
|SQL.TSql 编辑器显示估计计划|Ctrl+D、E|
|SQL.TSql 编辑器切换执行计划|Ctrl+D、A|
|SQL.TSql 编辑器切换结果窗格|Ctrl+D、R|
|TSql 编辑器克隆查询|Ctrl+Alt+N|
|TSql 编辑器数据库组合|Shift+Alt+PgDn|

## <a name="microsoft-sql-server-data-tools-t-sql-pdw-editor"></a><a name="bkmk_linkfix"></a>Microsoft SQL Server Data Tools，T-sql PDW 编辑器

|命令|键盘快捷键|
|--------------|------------------------|
|SQL.TSql 编辑器取消查询|Alt+Break|
|SQL.TSql 编辑器执行查询|Ctrl+Shift+E|
|SQL.TSql 编辑器结果显示为文件|Ctrl+D、F|
|SQL.TSql 编辑器结果显示为网格|Ctrl+D、G|
|SQL.TSql 编辑器结果显示为文本|Ctrl+D、T|
|SQL.TSql 编辑器显示估计计划|Ctrl+D、E|
|SQL.TSql 编辑器切换执行计划|Ctrl+D、A|
|SQL.TSql 编辑器切换结果窗格|Ctrl+D、R|
|TSql 编辑器克隆查询|Ctrl+Alt+N|
|TSql 编辑器数据库组合|Shift+Alt+PgDn|

## <a name="page-inspector"></a><a name="bkmk_PageInspector"></a>Page Inspector

|Command|键盘快捷方式|
|-------------|-----------------------|
|PageInspector.最小化|F12|

## <a name="query-designer"></a><a name="bkmk_QueryDesigner"></a>查询设计器

|命令|键盘快捷键|
|--------------|------------------------|
|查询设计器.取消检索数据|Ctrl+T|
|查询设计器.条件|Ctrl+2|
|查询设计器.关系图|Ctrl+1|
|查询设计器.执行SQL|Ctrl+R|
|查询设计器.转到行|Ctrl+G|
|查询设计器.联接模式|Ctrl+Shift+J|
|查询设计器.结果|Ctrl+4|
|查询设计器.SQL|Ctrl+3|

## <a name="query-results"></a><a name="bkmk_QueryResults"></a>查询结果

|命令|键盘快捷键|
|--------------|------------------------|
|SQL.查询结果新行|Alt+End|
|SQL.查询结果刷新|Shift+Alt+R|
|SQL.查询结果停止|Alt+Break|

## <a name="report-designer"></a><a name="bkmk_ReportDesigner"></a>报表设计器

|命令|键盘快捷键|
|--------------|------------------------|
|编辑.分行|Enter|
|编辑.左移字符|向左键|
|编辑.向左扩展一个字符|Shift+向左键|
|编辑.右移字符|向右键|
|编辑.向右扩展一个字符|Shift+向右键|
|编辑.插入制表符|选项卡|
|编辑.向下移动一行|向下键|
|编辑.向下扩展一行|Shift+向下键|
|编辑.向上移动一行|向上键|
|编辑.向上扩展一行|Shift+向上键|
|编辑.下移控件|Ctrl+向下键|
|编辑.左移控件|Ctrl+向左键|
|编辑.右移控件|Ctrl+向右键|
|编辑.上移控件|Ctrl+向上键|
|编辑.取消选定|Esc|
|编辑.向下调大控件大小|Ctrl+Shift+向下键|
|编辑.向左调整控件大小|Ctrl+Shift+向左键|
|编辑.向右调整控件大小|Ctrl+Shift+向右键|
|编辑.向上调整控件大小|Ctrl+Shift+向上键|
|编辑.左缩进|Shift+Tab|
|视图.报告数据|Ctrl+Alt+D|

## <a name="sequence-diagram"></a><a name="bkmk_SequenceDiagram"></a>序列图

|命令|键盘快捷键|
|--------------|------------------------|
|体系结构设计器.序列.导航到代码|F12|
|编辑.删除|Shift+Del|

## <a name="settings-designer"></a><a name="bkmk_SettingsDesigner"></a>设置设计器

|命令|键盘快捷键|
|--------------|------------------------|
|编辑.编辑单元格|F2|
|编辑.移除行|Ctrl+Delete|
|编辑.取消选定|Esc|
|视图.查看代码|F7|

## <a name="solution-explorer"></a><a name="bkmk_SolutionExplorer"></a>解决方案资源管理器

|Command|键盘快捷方式|
|-------------|-----------------------|
|类视图上下文菜单.类视图项目.查看.在 Page Inspector 中查看|Ctrl+K、Ctrl+G|

## <a name="team-explorer"></a><a name="bkmk_TeamExplorer"></a>团队资源管理器

|Command|键盘快捷方式|
|-------------|-----------------------|
|编辑.删除|删除|
|文件.重命名|F2|
|Team Foundation 上下文菜单.命令.转到团队资源管理器导航|Alt+Home|
|Team Foundation 上下文菜单.命令.转到团队资源管理器下一节内容|Alt+向下键|
|Team Foundation 上下文菜单.命令.转到团队资源管理器页面内容|Alt+0|
|Team Foundation 上下文菜单.命令.转到团队资源管理器上一节内容|Alt+向上键|
|Team Foundation 上下文菜单.命令.转到团队资源管理器第 1 节内容|Alt+1|
|Team Foundation 上下文菜单.命令.转到团队资源管理器第 2 节内容|Alt+2|
|Team Foundation 上下文菜单.命令.转到团队资源管理器第 3 节内容|Alt+3|
|Team Foundation 上下文菜单.命令.转到团队资源管理器第 4 节内容|Alt+4|
|Team Foundation 上下文菜单.命令.转到团队资源管理器第 5 节内容|Alt+5|
|Team Foundation 上下文菜单.命令.转到团队资源管理器第 6 节内容|Alt+6|
|Team Foundation 上下文菜单.命令.转到团队资源管理器第 7 节内容|Alt+7|
|Team Foundation 上下文菜单.命令.转到团队资源管理器第 8 节内容|Alt+8|
|Team Foundation 上下文菜单.命令.转到团队资源管理器第 9 节内容|Alt+9|
|Team Foundation 上下文菜单.命令.团队资源管理器向后定位|Alt + 向左键|
|Team Foundation 上下文菜单.命令.团队资源管理器向前定位|Alt + 向右键|
|Team Foundation 上下文菜单.我的工作页正在进行.Tfs 上下文我的工作页创建副本 WI|Shift+Alt+C|
|Team Foundation 上下文菜单.我的工作页正在进行.Tfs 上下文我的工作页新建链接 WI|Shift+Alt+L|
|视图.刷新|F5|

## <a name="team-foundation-build-detail-editor"></a><a name="bkmk_TFBuild"></a>Team Foundation Build 详细信息编辑器

|Command|键盘快捷方式|
|-------------|-----------------------|
|视图.刷新|F5|

## <a name="test-explorer"></a><a name="bkmk_TestExplorer"></a>测试资源管理器

|Command|键盘快捷方式|
|-------------|-----------------------|
|测试资源管理器.打开测试|F12|

## <a name="text-editor"></a><a name="bkmk_TextEditor"></a>文本编辑器

|                             命令                              |                  键盘快捷键                   |
|-------------------------------------------------------------------|-------------------------------------------------------|
|                          编辑.分行                           |     Enter<br /><br /> 或<br /><br /> Shift+Enter      |
|                           编辑.左移字符                           |                      向左键                       |
|                        编辑.向左扩展一个字符                        |                   Shift+向左键                    |
|                     编辑.向左扩展一个字符列                     |                 Shift+Alt+向左键                  |
|                          编辑.右移字符                           |                      向右键                      |
|                       编辑.向右扩展一个字符                        |                   Shift+向右键                   |
|                    编辑.向右扩展一个字符列                     |                 Shift+Alt+向右键                 |
|                        编辑.字符转置                         |                        Ctrl+T                         |
|                        编辑.清除书签                        |                    Ctrl+K、Ctrl+L                     |
|                     编辑.折叠所有大纲显示                     |                    Ctrl+M、Ctrl+A                     |
|                    编辑.折叠当前区域                     |                    Ctrl+M、Ctrl+S                     |
|                         编辑.折叠标记                          |                    Ctrl+M、Ctrl+T                     |
|                    编辑.折叠到定义                     |                    Ctrl+M、Ctrl+O                     |
|                       编辑.注释选定内容                       |                    Ctrl+K、Ctrl+C                     |
|                         编辑.完成单词                         | Ctrl+空格键<br /><br /> 或<br /><br /> Alt + 向右键 |
|                       编辑.复制参数提示                       |                   Ctrl+Shift+Alt+C                    |
|                     编辑.减少筛选器级别                      |                         Alt+,                         |
|                       编辑.向后删除                        |   Backspace<br /><br /> 或<br /><br /> Shift+Bkspce   |
|                  编辑.删除水平空白                  |                    Ctrl+K、Ctrl+\                     |
|                         编辑.文档结尾                          |                       Ctrl+End                        |
|                      编辑.文档结尾扩展                       |                    Ctrl+Shift+End                     |
|                        编辑.文档开始                         |                       Ctrl+Home                       |
|                     编辑.文档开始扩展                      |                    Ctrl+Shift+Home                    |
|                      编辑.展开所有大纲显示                      |                    Ctrl+M、Ctrl+X                     |
|                     编辑.展开当前区域                      |                    Ctrl+M、Ctrl+E                     |
|                        编辑.编排文档格式                        |                    Ctrl+K、Ctrl+D                     |
|                       编辑.格式化选定内容                        |                    Ctrl+K、Ctrl+F                     |
|                          编辑.转到大括号                           |                        Ctrl+]                         |
|                       编辑.扩展转到大括号                        |                     Ctrl+Shift+]                      |
|                        编辑.隐藏选定内容                         |                    Ctrl+M、Ctrl+H                     |
|                     编辑.增加筛选器级别                      |                         Alt+.                         |
|                      编辑.渐进式搜索                       |                        Ctrl+I                         |
|                          编辑.插入制表符                           |                          选项卡                          |
|                           编辑.剪切行                            |                        Ctrl+L                         |
|                          编辑.删除行                          |                     Ctrl+Shift+L                      |
|                           编辑.向下移动一行                           |                      向下键                       |
|                        编辑.向下扩展一行                        |                   Shift+向下键                    |
|                     编辑.向下扩展列                     |                 Shift+Alt+向下键                  |
|                           编辑.行尾                            |                          结束                          |
|                        编辑.扩展到行尾                         |                       Shift+End                       |
|                     编辑.行尾扩展列                      |                     Shift+Alt+End                     |
|                        编辑.上开新行                         |                      Ctrl+Enter                       |
|                        编辑.下开新行                         |                   Ctrl+Shift+Enter                    |
|                          编辑.行首                           |                         Home                          |
|                       编辑.扩展到行首                        |                      Shift+Home                       |
|                    编辑.行首扩展列                     |                    Shift+Alt+Home                     |
|                        编辑.行转置                         |                      Shift+Alt+T                      |
|                            编辑.向上移动一行                            |                       向上键                        |
|                         编辑.向上扩展一行                         |                    Shift+向上键                     |
|                      编辑.向上扩展列                      |                  Shift+Alt+向上键                   |
|                         编辑.列出成员                          |                        Ctrl+J                         |
|                        编辑.转换为小写                         |                        Ctrl+U                         |
|                        编辑.转换为大写                         |                     Ctrl+Shift+U                      |
|                    编辑.将选定行下移                     |                    Alt+向下键                     |
|                     编辑.将选定行上移                      |                     Alt+向上键                      |
|                   编辑.下一个突出显示的引用                   |                 Ctrl+Shift+向下键                 |
|                         编辑.改写模式                         |                        插入                         |
|                           编辑.向下翻页                           |                         PgDn                          |
|                        编辑.向下扩展一页                        |                      Shift+PgDn                       |
|                            编辑.向上翻页                            |                         PgUp                          |
|                         编辑.向上扩展一页                         |                      Shift+PgUp                       |
|                        编辑.参数信息                         |                  Ctrl+Shift+空格键                  |
|                      编辑.粘贴参数提示                       |                   Ctrl+Shift+Alt+P                    |
|                         编辑.向后查看                         |                      Ctrl+Alt+-                       |
|                        编辑.查看定义                        |                        Alt+F12                        |
|                         编辑.向前查看                          |                      Ctrl+Alt+=                       |
|                 编辑.上一个突出显示的引用                 |                  Ctrl+Shift+向上键                  |
|                          编辑.快速信息                           |                    Ctrl+K、Ctrl+I                     |
|                   编辑.反向渐进式搜索                   |                     Ctrl+Shift+I                      |
|                        编辑.向下滚动一行                        |                    Ctrl+向下键                    |
|                         编辑.向上滚动一行                         |                     Ctrl+向上键                     |
|                      编辑.选择当前字                       |                        Ctrl+W                         |
|                       编辑.取消选定                        |                        Escape                         |
|                      编辑.选择到最后一个返回                      |                        Ctrl+=                         |
|                       编辑.显示 CodeLens 菜单                       |                        Alt+\`                         |
|                      编辑.停止隐藏当前区域                       |                    Ctrl+M、Ctrl+U                     |
|                        编辑.停止大纲显示                         |                    Ctrl+M、Ctrl+P                     |
|                          编辑.交换定位点                          |                    Ctrl+K、Ctrl+A                     |
|                           编辑.左缩进                            |                       Shift+Tab                       |
|                      编辑.切换所有大纲显示                      |                    Ctrl+M、Ctrl+L                     |
|                        编辑.切换书签                        |                    Ctrl+K、Ctrl+K                     |
|                     Edit.ToggleCompletionMode                     |                    Ctrl+Alt+空格键                     |
|                   编辑.切换大纲显示展开                   |                    Ctrl+M、Ctrl+M                     |
|                    编辑.切换任务列表快捷方式                    |                    Ctrl+K、Ctrl+H                     |
|                        编辑.切换自动换行                        |                    Ctrl+E、Ctrl+W                     |
|                      编辑.取消注释选定内容                      |                    Ctrl+K、Ctrl+U                     |
|                          编辑.视图底部                          |                       Ctrl+PgDn                       |
|                       编辑.扩展到视图底部                       |                    Ctrl+Shift+PgDn                    |
|                           编辑.视图顶部                            |                       Ctrl+PgUp                       |
|                        编辑.扩展到视图顶部                         |                    Ctrl+Shift+PgUp                    |
|                        编辑.查看空白                        |                    Ctrl+R、Ctrl+W                     |
|                       编辑.字删除直至结尾处                        |                      Ctrl+Delete                      |
|                      编辑.字删除直至开始处                       |                    Ctrl+Backspace                     |
|                           编辑.下一字                           |                   Ctrl+向右键                    |
|                        编辑.扩展到下一字                        |                Ctrl+Shift+向右键                 |
|                     编辑.向后扩展一个字列                     |              Ctrl+Shift+Alt+向右键               |
|                         编辑.上一字                         |                    Ctrl+向左键                    |
|                      编辑.扩展到上一字                      |                 Ctrl+Shift+向左键                 |
|                   编辑.向前扩展一个字列                   |               Ctrl+Shift+Alt+向左键               |
|                        编辑.字转置                         |                     Ctrl+Shift+T                      |
|        编辑器上下文菜单.代码窗口.交互执行         |                       Alt+Enter                       |
|      编辑器上下文菜单.代码窗口.交互执行行       |                         Alt+'                         |
|         其他上下文菜单.HTML 上下文.在 Page Inspector 中查看         |                    Ctrl+K、Ctrl+G                     |
|   Team Foundation 上下文菜单.批注.Tfs 批注移动下一个区域   |                       Alt+PgDn                        |
| Team Foundation 上下文菜单.批注.Tfs 批注移动上一个区域 |                       Alt+PgUp                        |

## <a name="uml-activity-diagram"></a><a name="bkmk_UMLactivityDiagram"></a>UML 活动图

|Command|键盘快捷键|
|-------------|-----------------------|
|编辑.删除|Shift+Del|

## <a name="uml-class-diagram"></a><a name="bkmk_UMLclassDiagram"></a>UML 类图

|Command|键盘快捷键|
|-------------|-----------------------|
|编辑.从模型中删除|Shift+Del|

## <a name="uml-component-diagram"></a><a name="bkmk_UMLcomponentDiagram"></a>UML 组件图

|Command|键盘快捷键|
|-------------|-----------------------|
|编辑.从模型中删除|Shift+Del|

## <a name="uml-use-case-diagram"></a><a name="bkmk_UMLusecaseDiagram"></a>UML 用例图

|Command|键盘快捷键|
|-------------|-----------------------|
|编辑.从模型中删除|Shift+Del|

## <a name="vc-accelerator-editor"></a><a name="bkmk_vcaccelerator"></a>VC 快捷键编辑器

|命令|键盘快捷键|
|--------------|------------------------|
|编辑.新建快捷键|插入|
|编辑.键入的下一个键|Ctrl+W|

## <a name="vc-dialog-editor"></a><a name="bkmk_vcdialogeditor"></a>VC 对话框编辑器

|命令|键盘快捷键|
|--------------|------------------------|
|编辑.下移控件|向下键|
|编辑.左移控件|向左键|
|编辑.右移控件|向右键|
|编辑.上移控件|向上键|
|编辑.向左滚动一列|Ctrl+向左键|
|编辑.向右滚动一列|Ctrl+向右键|
|编辑.向下滚动一行|Ctrl+向下键|
|编辑.向上滚动一行|Ctrl+向上键|
|编辑.向下调大控件大小|Shift+向下键|
|编辑.向左调整控件大小|Shift+向左键|
|编辑.向右调整控件大小|Shift+向右键|
|编辑.向上调整控件大小|Shift+向上键|
|格式.底部对齐|Ctrl+Shift+向下键|
|格式.居中对齐|Shift+F9|
|格式.左对齐|Ctrl+Shift+向左键|
|格式.中间对齐|F9|
|格式.右对齐|Ctrl+Shift+向右键|
|格式.顶部对齐|Ctrl+Shift+向上键|
|格式.按钮下|Ctrl+B|
|格式.按钮右|Ctrl+R|
|格式.水平居中|Ctrl+Shift+F9|
|格式.垂直居中|Ctrl+F9|
|格式.检查助记键|Ctrl+M|
|格式.按内容调整大小|Shift+F7|
|格式.横向间隔|Alt + 向右键<br /><br /> 或<br /><br /> Alt + 向左键|
|格式.纵向间隔|Alt+向上键<br /><br /> 或<br /><br /> Alt+向下键|
|格式.Tab 键顺序|Ctrl+D|
|格式.测试对话框|Ctrl+T|
|格式.切换辅助线|Ctrl+G|

## <a name="vc-image-editor"></a><a name="bkmk_vcimageeditor"></a>VC 图像编辑器

|命令|键盘快捷键|
|--------------|------------------------|
|图像.喷枪工具|Ctrl+A|
|图像.画笔工具|Ctrl+B|
|图像.复制选定内容并绘制其轮廓|Ctrl+Shift+U|
|图像.不透明处理|Ctrl+J|
|图像.椭圆工具|Alt+P|
|图像.清除工具|Ctrl+Shift+I|
|图像.实心椭圆工具|Ctrl+Shift+Alt+P|
|图像.实心矩形工具|Ctrl+Shift+Alt+R|
|图像.实心圆角矩形工具|Ctrl+Shift+Alt+W|
|图像.填充工具|Ctrl+F|
|图像.水平翻转|Ctrl+H|
|图像.垂直翻转|Shift+Alt+H|
|图像.较大画笔|Ctrl+=|
|图像.直线工具|Ctrl+L|
|图像.放大工具|Ctrl+M|
|图像.放大|Ctrl+Shift+M|
|图像.新建图像类型|插入|
|图像.下一种颜色|Ctrl+]<br /><br /> or<br /><br /> Ctrl+向右键|
|Image.NextRightColor|Ctrl+Shift+]<br /><br /> or<br /><br /> Ctrl+Shift+向右键|
|图像.空心椭圆工具|Shift+Alt+P|
|图像.空心矩形工具|Shift+Alt+R|
|图像.空心圆角矩形工具|Shift+Alt+W|
|图像.铅笔工具|Ctrl+I|
|图像.上一种颜色|Ctrl+[<br /><br /> 或<br /><br /> Ctrl+向左键|
|Image.PreviousRightColor|Ctrl+Shift+[<br /><br /> 或<br /><br /> Ctrl+Shift+向左键|
|图像.矩形选择工具|Shift+Alt+S|
|图像.矩形工具|Alt+R|
|图像.旋转 90 度|Ctrl+Shift+H|
|图像.圆角矩形工具|Alt+W|
|图像.网格|Ctrl+Alt+S|
|图像.显示平铺网格|Ctrl+Shift+Alt+S|
|图像.小画笔|Ctrl+.|
|图像.较小画笔|Ctrl+-|
|图像.文本工具|Ctrl+T|
|图像.将所选内容用作画笔|Ctrl+U|
|图像.放大|Ctrl+Shift+.<br /><br /> 或<br /><br /> Ctrl+向上键|
|图像.缩小|Ctrl+Shift+,<br /><br /> 或<br /><br /> Ctrl+向下键|

## <a name="vc-string-editor"></a><a name="bkmk_vcstringeditor"></a>VC 字符串编辑器

|Command|键盘快捷方式|
|-------------|-----------------------|
|编辑.新建字符串|插入|

## <a name="view-designer"></a><a name="bkmk_viewDesigner"></a>视图设计器

|命令|键盘快捷键|
|--------------|------------------------|
|查询设计器.取消检索数据|Ctrl+T|
|查询设计器.条件|Ctrl+2|
|查询设计器.关系图|Ctrl+1|
|查询设计器.执行SQL|Ctrl+R|
|查询设计器.转到行|Ctrl+G|
|查询设计器.联接模式|Ctrl+Shift+J|
|查询设计器.结果|Ctrl+4|
|查询设计器.SQL|Ctrl+3|

## <a name="visual-studio"></a><a name="bkmk_visualstudio"></a>Visual Studio

|Command|键盘快捷方式|
|-------------|-----------------------|
|其他上下文菜单.或设计器上下文.隐藏方法窗格|Ctrl+1|

## <a name="windows-forms-designer"></a><a name="bkmk_wfdesigner"></a>Windows 窗体设计器

|命令|键盘快捷键|
|--------------|------------------------|
|编辑.分行|Enter|
|编辑.左移字符|向左键|
|编辑.向左扩展一个字符|Shift+向左键|
|编辑.右移字符|向右键|
|编辑.向右扩展一个字符|Shift+向右键|
|编辑.文档结尾|结束|
|编辑.文档结尾扩展|Shift+End|
|编辑.文档开始|Home|
|编辑.文档开始扩展|Shift+Home|
|编辑.插入制表符|选项卡|
|编辑.向下移动一行|向下键|
|编辑.向下扩展一行|Shift+向上键|
|编辑.向上移动一行|向上键|
|编辑.向上扩展一行|Shift+向下键|
|编辑.下移控件|Ctrl+向下键|
|编辑.左移控件|Ctrl+向左键|
|编辑.右移控件|Ctrl+向右键|
|编辑.上移控件|Ctrl+向上键|
|编辑.取消选定|Escape|
|编辑.向下调大控件大小|Ctrl+Shift+向下键|
|编辑.向左调整控件大小|Ctrl+Shift+向左键|
|编辑.向右调整控件大小|Ctrl+Shift+向右键|
|编辑.向上调整控件大小|Ctrl+Shift+向上键|
|编辑.左缩进|Shift+Tab|

## <a name="work-item-editor"></a><a name="bkmk_workItemEditor"></a>工作项编辑器

|命令|键盘快捷键|
|--------------|------------------------|
|编辑.创建工作项的副本|Shift+Alt+C|
|编辑.刷新工作项|F5|
|团队.新建链接工作项|Shift+Alt+L|

## <a name="work-item-query-view"></a><a name="bkmk_WIqueryview"></a>工作项查询视图

|命令|键盘快捷键|
|--------------|------------------------|
|编辑.创建工作项的副本|Shift+Alt+C|
|编辑.缩进|Shift+Alt+向右键|
|编辑.升级|Shift+Alt+向左键|
|团队.新建链接工作项|Shift+Alt+L|
|团队.刷新|F5|
|窗口.切换|Shift+Alt+V|

## <a name="work-item-results-view"></a><a name="bkmk_WIresultsview"></a>工作项结果视图

|命令|键盘快捷键|
|--------------|------------------------|
|编辑.创建工作项的副本|Shift+Alt+C|
|编辑.缩进|Shift+Alt+向右键|
|编辑.升级|Shift+Alt+向左键|
|团队.转到下一个工作项|Shift+Alt+N|
|团队.转到上一个工作项|Shift+Alt+P|
|团队.新建链接工作项|Shift+Alt+L|
|团队.刷新|F5|
|窗口.切换|Shift+Alt+V|

## <a name="workflow-designer"></a><a name="bkmk_workflowdesigner"></a>工作流设计器

|命令|键盘快捷键|
|--------------|------------------------|
|编辑.完成单词|Ctrl+K、W<br /><br /> 或<br /><br /> Ctrl+K、Ctrl+W<br /><br /> or<br /><br /> Ctrl+空格键<br /><br /> or<br /><br /> Alt + 向右键|
|编辑.减少筛选器级别|Alt+,|
|编辑.增加筛选器级别|Alt+.|
|编辑.列出成员|Ctrl+K、L<br /><br /> or<br /><br /> Ctrl+K、Ctrl+L<br /><br /> 或<br /><br /> Ctrl+J|
|编辑.参数信息|Ctrl+K、P<br /><br /> or<br /><br /> Ctrl+K、Ctrl+P<br /><br /> 或<br /><br /> Ctrl+Shift+空格键|
|编辑.快速信息|Ctrl+K、I<br /><br /> 或<br /><br /> Ctrl+K、Ctrl+I|
|工作流设计器.折叠|Ctrl+E、Ctrl+C<br /><br /> 或<br /><br /> Ctrl+E、C|
|工作流设计器.全部折叠|或|
|工作流设计器.连接节点|Ctrl+E、Ctrl+F<br /><br /> or<br /><br /> Ctrl+E、F|
|工作流设计器.创建变量|Ctrl+E、Ctrl+N<br /><br /> or<br /><br /> Ctrl+E、N|
|工作流设计器.全部展开|Ctrl+E、Ctrl+X<br /><br /> 或<br /><br /> Ctrl+E、X|
|工作流设计器.就地展开|Ctrl+E、Ctrl+E<br /><br /> 或<br /><br /> Ctrl+E、E|
|工作流设计器.转到父级|Ctrl+E、Ctrl+P<br /><br /> 或<br /><br /> Ctrl+E、P|
|工作流设计器.移动焦点|Ctrl+E、Ctrl+M<br /><br /> 或<br /><br /> Ctrl+E、M|
|工作流设计器.在设计器中导航|Ctrl+Alt+F6|
|工作流设计器.还原|Ctrl+E、Ctrl+R<br /><br /> or<br /><br /> Ctrl+E、R|
|工作流设计器.显示隐藏参数设计器|Ctrl+E、Ctrl+A<br /><br /> or<br /><br /> Ctrl+E、A|
|工作流设计器.显示隐藏导入设计器|Ctrl+E、Ctrl+I<br /><br /> 或<br /><br /> Ctrl+E、I|
|工作流设计器.显示隐藏摘要图|Ctrl+E、Ctrl+O<br /><br /> 或<br /><br /> Ctrl+E、O|
|工作流设计器.显示隐藏变量设计器|Ctrl+E、Ctrl+V<br /><br /> 或<br /><br /> Ctrl+E、V|
|工作流设计器.切换选择|Ctrl+E、Ctrl+Ｓ<br /><br /> 或<br /><br /> Ctrl+E、S|
|工作流设计器.放大|Ctrl+Num +|
|工作流设计器.缩小|Ctrl+Num -|

## <a name="xaml-ui-designer"></a><a name="bkmk_xamluidesigner"></a>XAML UI 设计器

|命令|键盘快捷键|
|--------------|------------------------|
|设计.适应全部|Ctrl+0|
|设计.显示手柄|F9|
|设计.放大|Ctrl+Alt+=|
|设计.缩小|Ctrl+Alt+-|
|格式.编辑文本|F2|
|格式.重置布局.全部|Ctrl+Shift+R|
|视图.向左移动左边缘|Ctrl+Shift+,|
|视图.向右移动左边缘|Ctrl+Shift+.|
|视图.向左移动右边缘|Ctrl+Shift+Alt+,|
|视图.向右移动右边缘|Ctrl+Shift+Alt+.|
|运行项目代码|Ctrl+F9|

## <a name="xml-text-editor"></a><a name="bkmk_xmlTextEditor"></a>XML （文本）编辑器

|命令|键盘快捷键|
|--------------|------------------------|
|XML.启动 XSLT (调试)|Alt+F5|
|XML.启动 XSLT (不调试)|Ctrl+Alt+F5|

## <a name="xml-schema-designer"></a><a name="bkmk_xmlSchemaDesigner"></a>XML 架构设计器

|命令|键盘快捷键|
|--------------|------------------------|
|关系图视图.从下到上|Alt+向上键|
|关系图视图.从左到右|Alt + 向右键|
|关系图视图.从右到左|Alt + 向左键|
|关系图视图.从上到下|Alt+向下键|
|其他上下文菜单.图形视图.从工作区中删除|删除|
|Xsd 设计器.显示内容模型视图|Ctrl+2|
|Xsd 设计器.显示图形视图|Ctrl+3|
|Xsd 设计器.显示起始视图|Ctrl+1|

## <a name="see-also"></a>另请参阅
 [图标的图像编辑器](https://msdn.microsoft.com/library/586d2b8b-0348-4883-a85d-1ff0ddbf14dd) [使用 IntelliSense](../ide/using-intellisense.md)
