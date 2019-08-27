---
title: 注册项目类型 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], new project registry entries
- registry, new project types
- registration, new project types
ms.assetid: dfc0e231-6b4e-447d-9d64-0e66dea3394a
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: b950ea6dde73ecb7f20ef45e945106e8711aefb0
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66353354"
---
# <a name="registering-a-project-type"></a>注册项目类型
在创建新项目类型时，必须创建注册表项，使[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]来识别和处理您的项目类型。 您通常使用注册表脚本 (.rgs) 文件创建这些注册表项。

 在下面的示例中，从注册表语句提供默认路径和数据 （如果适用） 后, 跟的表包含每个语句的注册表脚本中的条目。 表提供了脚本条目和语句的附加信息。

> [!NOTE]
> 下面的注册表信息用于类型的示例和您将编写注册您的项目类型的注册表脚本中的条目的目的。 实际的条目和它们的用途可能因您的项目类型的特定要求。 您应查看可用于找到相似的项目进行开发，类型的一个示例，然后查看该示例注册表脚本。

 下面的示例是从 HKEY_CLASSES_ROOT。

## <a name="example"></a>示例

```
\.figp
   @="FigPrjFile"
   "Content Type"="text/plain"
\.figp\ShellNew
   "NullFile"=""
\FigPrjFile
   @="Figure Project File"
\DefaultIcon
   @="<Visual Studio SDK installation path>\\9.0VSIntegration\\SomeFolder\\FigPkgs\\FigPrj\\Debug\\FigPrj.dll,-206"
\shell\open
   @="&Open in Visual Studio"
\shell\open\command
   @="devenv.exe \"%1\""
```

|名称|类型|数据|描述|
|----------|----------|----------|-----------------|
|`@`|REG_SZ|`FigPrjFile`|具有扩展.figp 的文件类型名称和项目的说明。|
|`Content Type`|REG_SZ|`Text/plain`|项目文件的的内容类型。|
|`NullFile`|REG_SZ|`Null`||
|`@`|REG_SZ|`%MODULE%,-206`|用于此类型的项目的默认图标。 %模块 %语句完成到 DLL 的项目类型的默认位置在注册表中。|
|`@`|REG_SZ|`&Open in Visual Studio`|将在其中打开此项目类型的默认应用程序。|
|`@`|REG_SZ|`devenv.exe "%1"`|打开此类型的项目时将运行的默认命令。|

 下面的示例取自 HKEY_LOCAL_MACHINE 且位于注册表项 [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\99.0Exp\Packages] 下。

## <a name="example"></a>示例

```
\{ACEF4EB2-57CF-11D2-96F4-000000000000} (The CLSID for the VSPackage)
   @="FigPrj Project Package"
   "InprocServer32"="9.0<Visual Studio SDK installation path>\\VSIntegration\\Archive\\FigPkgs\\FigPrj\\                      Debug\\FigPrj.dll"
   "CompanyName"="Microsoft"
   "ProductName"="Figure Project Sample"
   "ProductVersion"="9.0"
   "MinEdition"="professional"
   "ID"=dword:00000001
\{ACEF4EB2-57CF-11D2-96F4-000000000000}\SatelliteDLL
   "DllName"="FigPrjUI.dll"
   "Path"="9.0<Visual Studio SDK installation path>\\VSIntegration\\Archive\\FigPkgs\\FigPrj\\Debug\\"
\{ACEF4EB2-57CF-11D2-96F4-000000000000}\Automation
   "FigProjects"=""
\{ACEF4EB2-57CF-11D2-96F4-000000000000}\AutomationEvents
   "FigProjectsEvents"="Returns the FigProjectsEvents Object"
   "FigProjectItemsEvents"="Returns the FigProjectItemsEvents Object"
```

|名称|类型|数据|描述|
|----------|----------|----------|-----------------|
|`@` （默认值）|REG_SZ|`FigPrj Project VSPackage`|这可本地化的名称注册 VSPackage （项目类型）。|
|`InprocServer32`|REG_SZ|`%MODULE%`|DLL 的项目类型的路径。 IDE 加载此 DLL，并将传递到 VSPackage CLSID`DllGetClassObject`若要获取<xref:Microsoft.VisualStudio.OLE.Interop.IClassFactory>构造<xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage>对象。|
|`CompanyName`|REG_SZ|`Microsoft`|开发项目类型的公司的名称。|
|`ProductName`|REG_SZ|`Figure Project Sample`|对于项目类型的名称。|
|`ProductVersion`|REG_SZ|`9.0`|发布的项目类型的版本号。|
|`MinEdition`|REG_SZ|`professional`|正在注册 VSPackage 的版本。|
|`ID`|REG_DWORD|`%IDS_PACKAGE_LOAD_KEY%`|包加载 VSPackage 项目的密钥。 环境已启动后加载项目时，该密钥进行验证。|
|`DllName`|REG_SZ|`%RESOURCE_DLL%`|附属 DLL，其中包含对于项目类型的本地化的资源文件名称。|
|`Path`|REG_SZ|`%RESOURCE_PATH%`|附属 DLL 的路径。|
|`FigProjectsEvents`|REG_SZ|请参阅值的语句。|确定此自动化事件返回的文本字符串。|
|`FigProjectItemsEvents`|REG_SZ|请参阅值的语句。|确定此自动化事件返回的文本字符串。|

 下面的所有示例都位于注册表项 [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\9.0Exp\Projects] 下。

## <a name="example"></a>示例

```
\{C061DB26-5833-11D2-96F5-000000000000} (The CLSID for projects of this type)
   @="FigPrj Project"
   "DisplayName"="#2"
   "Package"="{ACEF4EB2-57CF-11D2-96F4-000000000000}"
   "ProjectTemplatesDir"="C:\\Program Files\\VSIP 9.0\\EnvSDK\\FigPkgs\\                           FigPrj\\FigPrjProjects"
   "ItemTemplatesDir"="<Visual Studio SDK installation path>\\VSIntegration\\Archive9.0\\FigPkgs\\FigPrj\\                           FigPrjProjectItems"
   "DisplayProjectFileExtensions"="#3"
   "PossibleProjectExtensions"="figp"
   "DefaultProjectExtension"=".figp"
\{C061DB26-5833-11D2-96F5-000000000000}\Filters\1       (Folder 1 contains settings for Open Files filters.)
   @="#4"
   "CommonOpenFilesFilter"=dword:00000000
   "CommonFindFilesFilter"=dword:00000000
   "NotAddExistingItemFilter"=dword:00000000
   "FindInFilesFilter"=dword:00000000
   "NotOpenFileFilter"=dword:00000000
   "SortPriority"=dword:000003e8
\{C061DB26-5833-11D2-96F5-000000000000}\Filters\2
      (Folder 2 contains settings for Find in Files filters.)
   @="#5"
   "CommonOpenFilesFilter"=dword:00000000
   "CommonFindFilesFilter"=dword:00000000
   "NotAddExistingItemFilter"=dword:00000001
   "FindInFilesFilter"=dword:00000001
   "NotOpenFileFilter"=dword:00000000
   "SortPriority"=dword:000003e8
\{C061DB26-5833-11D2-96F5-000000000000}\AddItemTemplates\TemplateDirs\ {ACEF4EB2-57CF-11D2-96F4-000000000000}\1 (Second GUID indicates the registered project type for the Add Items templates.)
   @="#6"
   "TemplatesDir"="<Visual Studio SDK installation path>\\VSIntegration\\Archive9.0\\FigPkgs\\FigPrj\\                    FigPrjProjectItems"
   "SortPriority"=dword:00000064
```

|名称|类型|数据|描述|
|----------|----------|----------|-----------------|
|`@`|REG_SZ|`FigPrj Project`|此类型的项目的默认名称。|
|`DisplayName`|REG_SZ|`#%IDS_PROJECT_TYPE%`|包下注册的名称的资源 ID 来检索从附属 DLL。|
|`Package`|REG_SZ|`%CLSID_Package%`|包下注册的 vspackage 的类 ID。|
|`ProjectTemplatesDir`|REG_SZ|`%TEMPLATE_PATH%\FigPrjProjects`|默认项目模板文件的路径。 这些是所显示的新项目模板的文件。|
|`ItemTemplatesDir`|REG_SZ|`%TEMPLATE_PATH% \FigPrjProjectItems`|项目项模板文件的默认路径。 这些是添加新项模板显示的文件。|
|`DisplayProjectFileExtensions`|REG_SZ|`#%IDS_DISPLAY_PROJ_FILE_EXT%`|使 IDE 来实现**打开**对话框。|
|`PossibleProjectExtensions`|REG_SZ|`figp`|由 IDE 来确定是否正在打开的项目处理此项目类型 （项目工厂）。 多个条目的格式是以分号分隔列表。 例如"vdproj; vdp"。|
|`DefaultProjectExtension`|REG_SZ|`.figp`|由 IDE 用作默认文件扩展名为另存为操作。|
|`Filter Settings`|REG_DWORD|各种，请参阅语句和提出的意见下表。|这些设置用于设置各种筛选器，用于显示 UI 对话框中的文件。|
|`@`|REG_SZ|`#%IDS_ADDITEM_TEMPLATES_ENTRY%`|添加项模板的资源 ID。|
|`TemplatesDir`|REG_SZ|`%TEMPLATE_PATH%\FigPrjProjectItems`|在对话框中显示的项目项的路径**添加新项**模板。|
|`SortPriority`|REG_DWORD|`100 (vcprx64)`|确定文件中显示的树节点中的排序顺序**添加新项**对话框。|

 下表显示了前面的代码段中可用的筛选器选项。

|筛选器选项|描述|
|-------------------|-----------------|
|`CommonFindFilesFilter`|指示筛选器是中的常见筛选器之一**在文件中查找**对话框。 前面未标记为常见的筛选器的筛选器列表中列出了常用筛选器。|
|`CommonOpenFilesFilter`|指示筛选器是中的常见筛选器之一**打开的文件**对话框。 前面未标记为常见的筛选器的筛选器列表中列出了常用筛选器。|
|`FindInFilesFilter`|指示筛选器会在筛选器之一**在文件中查找**对话框框和常用筛选器后，会列出。|
|`NotOpenFileFilter`|表示筛选器将不在中使用**打开的文件**对话框。|
|`NotAddExistingItemFilter`|指示筛选器不会使用在添加**现有项**对话框。|

 默认情况下，如果筛选器不具有一个或多个标记集，使用筛选器中**添加现有项**对话框和**打开的文件**后列出了常用筛选器对话框的。 在未使用筛选器**在文件中查找**对话框。

 下面的所有示例都位于注册表项 [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\9.0Exp\Projects] 下。

## <a name="example"></a>示例

```
{FE3BBBB6-72D5-11d2-9ACE-00C04F79A2A4} (The CLSID for Enterprise Projects)
\{FE3BBBB6-72D5-11d2-9ACE-00C04F79A2A4}\AddItemTemplates\TemplateDirs\ {ACEF4EB2-57CF-11D2-96F4-000000000000}\1 (CLSID for projects of this type)
   @="#7"
   "TemplatesDir"="<Visual Studio SDK installation path>\\VSIntegration\\Archive9.0\\FigPrj\\FigPrjProjects"
   "SortPriority"=dword:00000029
   "NewProjectDialogOnly"=dword:00000000
```

|名称|类型|数据|描述|
|----------|----------|----------|-----------------|
|`@`|REG_SZ|`#%IDS_NEWPROJ_ TEMPLATES_ENTRY%`|新项目模板的资源 ID。|
|`TemplatesDir`|REG_SZ|`%TEMPLATE_PATH%\FigPrjProjects`|默认为已注册的项目类型的项目的路径。|
|`SortPriority`|REG_DWORD|`41 (x29)`|集的排序顺序中新项目向导对话框中显示的项目。|
|`NewProjectDialogOnly`|REG_DWORD|`0`|0 指示仅在新建项目对话框中显示此类型的项目。|

 下面的所有示例都位于注册表项 [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\9.0Exp\Projects] 下。

## <a name="example"></a>示例

```
\{A2FE74E1-B743-11d0-AE1A-00A0C90FFFC3} (CLSID for Miscellaneous Files projects)
   @="Miscellaneous Files Project"
\AddItemTemplates\TemplateDirs\{ACEF4EB2-57CF-11D2-96F4-000000000000}\1
                                 (CLSID for Figures Project projects)
   @="#6"
   "TemplatesDir"="<Visual Studio SDK installation path>\\VSIntegration\\Archive9.0\\FigPkgs\\FigPrj\\                    FigPrjProjectItems"
   "SortPriority"=dword:00000064
```

|名称|类型|数据|描述|
|----------|----------|----------|-----------------|
|`@`|REG_SZ|None|默认值，该值指示以下条目，是用于杂项文件项目项。|
|`@`|REG_SZ|`#%IDS_ADDITEM_TEMPLATES_ENTRY%`|添加新项模板文件的资源 ID 值。|
|`TemplatesDir`|REG_SZ|`%TEMPLATE_PATH%\FigPrjProjectItems`|将显示在项的默认路径**添加新项**对话框。|
|`SortPriority`|REG_DWORD|`100 (vcprx64)`|建立的树节点中显示的排序顺序**添加新项**对话框。|

 下面的示例位于注册表项 [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\9.0Exp\Menus] 下。

## <a name="example"></a>示例

```
"{ACEF4EB2-57CF-11D2-96F4-000000000000}"=",1000,1"
```

 菜单项指向用于检索菜单信息的资源的 IDE。 当此数据已合并到菜单数据库时，将注册表 MenusMerged 部分中添加相同的密钥。 VSPackage 应直接修改 MenusMerged 部分下的任何内容信息。 在下表中的数据字段中，有三个以逗号分隔的字段。 第一个字段用于标识菜单资源文件的完整路径：

- 如果省略第一个字段，则该菜单资源从附属 DLL VSPackage GUID 标识加载。

  第二个字段用于标识菜单资源 ID 为 CTMENU 类型：

- 如果指定的资源 ID，并且第一个参数提供的文件路径，从完整文件路径加载菜单资源。

- 如果提供的资源 ID，但不是文件路径，该菜单资源从附属 DLL 中加载。

- 如果提供的完整文件路径和省略资源 ID，要加载的文件应是首席技术官文件。

  最后一个字段标识 CTMENU 资源的版本号。 你可以通过更改版本号再次合并菜单。

|名称|类型|数据|描述|
|----------|----------|----------|-----------------|
|%CLSID_Package%|REG_SZ|`,1000,1`|要检索的菜单信息的资源。|

 下面的所有示例都位于注册表项 [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\9.0Exp\NewProjectTemplates] 下。

```
\TemplateDirs\{ACEF4EB2-57CF-11D2-96F4-000000000000}\1                (CLSID for Figures Project projects)
   @="#7"
   "TemplatesDir"="<Visual Studio SDK installation path>\\VSIntegration\\Archive9.0\\FigPkgs\\FigPrj\\FigPrjProjects"
   "SortPriority"=dword:00000029
   "NewProjectDialogOnly"=dword:00000000
```

|名称|类型|数据|描述|
|----------|----------|----------|-----------------|
|`@`|REG_SZ|`#%IDS_NEWPROJ_TEMPLATES_ENTRY%`|图项目新项目模板的资源 ID 值。|
|`TemplatesDir`|REG_SZ|`%TEMPLATE_PATH%\FigPrjProjects`|新的项目目录的默认路径。 此目录中的项将显示在**新建项目向导**对话框。|
|`SortPriority`|REG_DWORD|`41 (x29)`|建立项目将显示在树节点的顺序**新的项目**对话框。|
|`NewProjectDialogOnly`|REG_DWORD|`0`|0 指示仅在显示此类型的项目**新的项目**对话框。|

 下面的示例位于注册表项 [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\9.0Exp\InstalledProducts] 下。

```
\FiguresProductSample
   "Package"="{ACEF4EB2-57CF-11D2-96F4-000000000000}"
   "UseInterface"=dword:00000001
```

|名称|类型|数据|描述|
|----------|----------|----------|-----------------|
|`Package`|REG_SZ|`%CLSID_Package%`|类 ID 的已注册 VSPackage。|
|`UseInterface`|REG_DWORD|`1`|1 表示 UI 将用于与此项目进行交互。 0 表示没有 UI 界面。|

 频繁地控制新的项目类型的 The.vsz 文件包含 RELATIVE_PATH 条目。 此路径是相对于项目类型中的以下安装程序密钥的 \ProductDir 条目下指定路径：

 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\7.0Exp\Setup

 例如，企业版框架项目模板将添加以下注册表项：

 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\7.0Exp\Setup\EF\ProductDir = C:\Program Files\Microsoft Visual Studio\EnterpriseFrameworks\

 这意味着如果包括 PROJECT_TYPE = EF 在.vsz 文件中，环境会找到您.vsz 文件以前指定的 ProductDir 目录中的条目。

## <a name="see-also"></a>请参阅
- [清单：创建新的项目类型](../../extensibility/internals/checklist-creating-new-project-types.md)
- [项目模型的元素](../../extensibility/internals/elements-of-a-project-model.md)
- [使用项目工厂创建项目实例](../../extensibility/internals/creating-project-instances-by-using-project-factories.md)