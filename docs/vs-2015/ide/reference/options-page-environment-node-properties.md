---
title: “选项”页 ->“环境”节点属性 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- automation [Visual Studio], controlling Tools Options
- Tools Options settings, Environment node properties
ms.assetid: 26dca41f-91fc-4ca7-9103-3da402baa1d5
caps.latest.revision: 22
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 6c7b6370793068ff07f30066ddd51b72dcc924b3
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72668705"
---
# <a name="options-page-environment-node-properties"></a>“选项”页 ->“环境”节点属性
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

本文档描述了与“选项”  对话框的“环境”  类别 `DTE.Properties("Environment", <Property Page>)` 关联的页面（或属性集合）。 每个小节的标题都是用于访问属性集合的调用，而每个小节中的表列出了集合中的属性。

## <a name="general"></a>常规
 `DTE.Properties("Environment", "General")`

|属性项名称|值|说明|
|------------------------|-----------|-----------------|
|ShowStatusBar|Get/Set (Boolean)|确定状态栏是否可见。|
|WindowMenuContainsNItems|Get/Set (Short)|确定如何将文档窗口包含在窗口菜单的底部。|
|MRUListContainsNItems|Get/Set (Short)|确定“最近使用的”子菜单中显示的文件数量。|
|动画|Get/Set (Boolean)|确定集成开发环境 (IDE) 是否在状态栏中使用动画。|
|AnimationSpeed|Get/Set (Short)||
|AutoAdjustExperience|Get/Set (Boolean)|根据客户端性能自动调整视觉体验。|
|RichClientExperienceOptions|Get/Set (Enum)|使用 <xref:EnvDTE100.vsRichClientExperienceOptions> 中的值启用丰富的客户端视觉体验。|
|CloseButtonActiveTabOnly|Get/Set (Boolean)|确定“关闭”  按钮是否仅显示在活动选项卡上。|
|AutohidePinActiveTabOnly|Get/Set (Boolean)|确定“自动隐藏”  按钮是否仅影响活动选项卡。|

## <a name="add-inmacros-security"></a>外接程序/宏安全性
 `DTE.Properties("Environment", "AddinMacrosSecurity")`

|属性项名称|值|说明|
|------------------------|-----------|-----------------|
|MacrosEnabled|Get/Set (Boolean)|允许宏运行。|
|AddinsEnabled|Get/Set (Boolean)|允许外接程序加载。|
|LoadAddinsFromTheWeb|Get/Set (Boolean)|允许外接程序从 Web 上的 URL 进行加载。|

## <a name="documents"></a>文档
 `DTE.Properties("Environment", "Documents")`

|属性项名称|值|说明|
|------------------------|-----------|-----------------|
|ReuseSavedActiveDocWindow|Get/Set (Boolean)|确定打开一个新的文件是否会重新使用当前文档窗口（如果已保存当前的文档）。 `false` 意味着始终为每个打开的文档打开新的文档窗口。|
|DetectFileChangesOutsideIDE|Get/Set (Boolean)|确定当操作系统通知 IDE 文件已在磁盘上修改了时，环境是否会自动重新加载在 IDE 中打开的文件。|
|AutoloadExternalChanges|Get/Set (Boolean)|确定检测到的对打开的文档的外部修改是否会自动重新加载修改的文件（如果未修改打开的文档）。 如果打开的文档已修改并且此属性是 `true`，则 IDE 会将此属性作为 `false` 属性进行提示。|
|InitializeOpenFileFromCurrentDocument|Get/Set (Boolean)|确定 <xref:EnvDTE.DTEClass.OpenFile%2A> 命令是否从上一个活动文档或从上一次打开文件的位置设定目录和文件名称的种子。|
|MiscFilesProjectSavesLastNItems|Get/Set (Short)|确定杂项文件项目记录的文件数量。 因此，你可以在下一次使用 IDE 时看到你最近作为磁盘上的杂项文件打开的文件。|
|ShowMiscFilesProject|Get/Set (Boolean)|确定是否显示杂项文件项目。|
|CheckForConsisentLineEndings|Get/Set (Boolean)|检查文件负载的行尾是否一致。|
|SaveDocsAsUnicodeWhenDataLoss|Get/Set (Boolean)|无法将数据保存在代码页时将文档保存为 Unicode 格式。|
|DontShowGlobalUndoChangeLossDialog|Get/Set (Boolean)|当全局撤消会修改其他已编辑文件时显示警告。|
|AllowEditingReadOnlyFiles|Get/Set (Boolean)|尝试保存只读文件时，允许对其进行编辑，但发出警告。|
|DocumentDockPreference|Get/Set (Enum)|<xref:EnvDTE100.vsDocumentDockPreferenceOptions>。 要在其中插入已打开文档的选项卡条中的位置。|

## <a name="extension-manager"></a>扩展管理器
 `DTE.Properties("Environment", "ExtensionManager")`

|属性项名称|值|说明|
|------------------------|-----------|-----------------|
|EnableAdminExtensions|Get/Set (Boolean)|在管理员凭据下运行 Visual Studio 时加载每用户扩展。 更改此值后必须重新启动 visual Studio。|
|EnableOnline|Get/Set (Boolean)|允许访问 Visual Studio 库上的扩展。|
|AutomaticallyCheckForUpdates|Get/Set (Boolean)|自动检查已安装扩展的更新。|

## <a name="find-and-replace"></a>查找和替换
 `DTE.Properties("Environment", "FindAndReplace")`

|属性项名称|值|说明|
|------------------------|-----------|-----------------|
|ShowWarningMessages|Get/Set (Boolean)|显示警告消息。|
|InitializeFromEditor|Get/Set (Boolean)|使用编辑器中的文本自动填充“查找内容”  框。|
|ShowMessageBoxes|Get/Set (Boolean)|显示信息性消息。|
|HideWindowsAfterMatchFromQuickFindReplace|Get/Set (Boolean)|使用“快速查找”  或“快速替换”  定位匹配后，隐藏“查找和替换”  窗口。|

## <a name="import-and-export-settings"></a>导入和导出设置
 `DTE.Properties("Environment", "Import and Export Settings")`

|属性项名称|值|说明|
|------------------------|-----------|-----------------|
|TrackTeamSettings|Get/Set (Boolean)|使用通过 TeamSettingsFile 指定的文件中的设置。|
|TeamSettingsFile|Get/Set (String)|具有团队设置的文件的名称。|
|AutoSaveFile|Get/Set (String)|用户设置自动保存在其中的文件的名称。|

## <a name="international-settings"></a>国际设置
 `DTE.Properties("Environment", "International")`

|属性项名称|值|说明|
|------------------------|-----------|-----------------|
|语言|Get/Set (String)|Visual Studio 的当前语言的 LCID 值。|

## <a name="keyboard"></a>键盘
 `DTE.Properties("Environment", "Keyboard")`

|属性项名称|值|说明|
|------------------------|-----------|-----------------|
|方案|Get/Set (String)|返回一个字符串，它包含一个内置的方案、一个包含加载的或“（默认的）”（如果没有加载 .vsk 文件） .vsk 文件的完整路径的字符串。|

## <a name="projects-and-solution"></a>项目和解决方案
 `DTE.Properties("Environment", "ProjectsAndSolution")`

|属性项名称|值|说明|
|------------------------|-----------|-----------------|
|OnRunOrPreview|Get/Set (String)|确定在预览或运行生成的项目之前 IDE 是否保存所有内容。|
|ProjectsLocation|Get/Set (String)|确定默认目录，其中“添加项目”  对话框将保存新的项目。|
|ShowOutputWindowBeforeBuild|Get/Set (Boolean)|决定开始生成是否显示“输出”  窗口。|
|ShowTaskListAfterBuild|Get/Set (Boolean)|确定不成功的生成操作在生成完成时是否显示“任务列表”  。|
|TrackFileSelectionInExplorer|Get/Set (Boolean)|确定是否在“解决方案资源管理器”  中跟踪当前项。|
|AlwaysShowSolutionNode|Get/Set (Boolean)|确定是否显示解决方案节点。|
|OnlySaveStartupProjectsAndDependencies|Get/Set (Boolean)|确定保存操作是否仅限于启动项目及其依赖文件。|
|ShowAdvancedBuildConfigurations|Get/Set (Boolean)|确定是否显示高级生成配置。|
|ConcurrentBuilds|Get/Set (String)|确定可能发生的并行项目生成的最大数量。|
|SaveNewProjects|Get/Set (Boolean)|确定是否自动保存新创建的项目。|
|PromptForRenameSymbol|Get/Set (Boolean)|指定重命名文件时是否会提示符号重命名。|
|OnRunWhenErrors|Get/Set (Enum)|指定生成完成出错时运行中的行为。|
|OnRunWhenOutOfDate|Get/Set (Enum)|指定项目过期时运行中的行为。|
|ProjectTemplatesLocation|Get/Set (String)|包含用户项目模板的目录。|
|ProjectTemplatesLocation|Get/Set (String)|包含用户项模板的目录。|
|DefaultBehaviorForStartupProjects|Get/Set (String)||
|MSBuildOutputVerbosity|Get/Set (String)|指定生成输出的详细级别。|

## <a name="startup"></a>启动
 `DTE.Properties("Environment", "Startup")`

|属性项名称|值|说明|
|------------------------|-----------|-----------------|
|OnStartUp|Get/Set (Enum)|从 <xref:EnvDTE.vsStartUp> 启动时要进行的操作，值为 0 到 5：<br /><br /> -   0：打开主页<br />-   1：加载上次加载的解决方案<br />-   2：显示“打开项目”  对话框<br />-   3：显示“新建项目”  对话框<br />-   4：显示空环境<br />-   5：显示起始页|
|StartPageRSSUrl|Get/Set (String)|启动时使用的 RSS 源的 URL。|
|StartPageRefreshDownloadedContent|Get/Set (Boolean)|在每次经过 StartPageRefreshInterval 中指定的间隔后刷新起始页。|
|StartPageRefreshInterval|Get/Set (Short)|刷新起始页所需的间隔，以分钟为单位。|

## <a name="tasklist"></a>TaskList
 `DTE.Properties("Environment", "TaskList")`

|属性项名称|值|说明|
|------------------------|-----------|-----------------|
|ConfirmTaskDeletion|Get/Set (Boolean)|指定从“任务列表”  删除任务时是否显示确认框。|
|WarnOnAddingHiddenItem|Get/Set (Boolean)|指定在添加不会显示的用户任务时是否收到警告。|
|DontShowFilePaths|Get/Set (Boolean)|指定是否在任务列表中显示完整文件路径。|
|CommentTokens|SafeArray|返回注释标记值的 SafeArray。 每个都具有字段、`Name`（字符串）和 `Priority`（<xref:EnvDTE.vsTaskPriority>、高、中或低）。|

## <a name="web-browser"></a>Web 浏览器
 `DTE.Properties("Environment", "WebBrowser")`

|属性项名称|值|说明|
|------------------------|-----------|-----------------|
|HomePage|Get/Set (String)|表示主页 URL。|
|SearchPage|Get/Set (String)|表示搜索页 URL。|
|ViewSourceIn|Get/Set (Enum)|<xref:EnvDTE.vsBrowserViewSource>（源、设计、外部）。|
|ViewSourceExternalProgram|Get/Set (String)|外部源查看器的路径。|

## <a name="see-also"></a>另请参阅
 [控制选项设置](https://msdn.microsoft.com/library/a09ed242-7494-4cde-bbd1-7a8ec617965d)在 "选项页"[选项页、"字体和颜色" 节点属性](../../ide/reference/options-page-fonts-and-colors-node-properties.md)[选项页、"文本编辑器节点属性" "](../../ide/reference/options-page-text-editor-node-properties.md) [环境选项" 对话框](../../ide/reference/environment-options-dialog-box.md)中[确定属性项的名称](https://msdn.microsoft.com/library/d450422d-47c7-4eeb-9f9f-3286264bc5aa)
