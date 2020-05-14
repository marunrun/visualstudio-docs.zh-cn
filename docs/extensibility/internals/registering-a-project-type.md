---
title: 注册项目类型 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], new project registry entries
- registry, new project types
- registration, new project types
ms.assetid: dfc0e231-6b4e-447d-9d64-0e66dea3394a
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 05ac1f393632934f193f5f4efaaf9e5459ffbb14
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80705875"
---
# <a name="registering-a-project-type"></a>注册项目类型
创建新项目类型时，必须创建注册表项，以启用[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]以识别和处理项目类型。 通常使用注册表脚本 （.rgs） 文件创建这些注册表项。

 在下面的示例中，注册表中的语句提供默认路径和数据（如果适用），然后是包含每个语句注册表脚本中的条目的表。 这些表提供脚本条目和有关语句的其他信息。

> [!NOTE]
> 以下注册表信息旨在作为要编写注册项目类型的注册表脚本中条目的类型和用途的示例。 您的实际条目及其用途可能因项目类型的特定要求而异。 您应该查看可用的示例，以查找与您正在开发的项目类型非常相似的示例，然后查看该示例的注册表脚本。

 以下示例来自HKEY_CLASSES_ROOT。

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
|`@`|REG_SZ|`FigPrjFile`|具有扩展名 .figp 的项目类型文件的名称和说明。|
|`Content Type`|REG_SZ|`Text/plain`|项目文件的内容类型。|
|`NullFile`|REG_SZ|`Null`||
|`@`|REG_SZ|`%MODULE%,-206`|用于此类型项目的默认图标。 %MODULE% 语句在注册表中完成到项目类型 DLL 的默认位置。|
|`@`|REG_SZ|`&Open in Visual Studio`|将在其中打开此项目类型的默认应用程序。|
|`@`|REG_SZ|`devenv.exe "%1"`|打开此类型的项目时将运行的默认命令。|

 以下示例来自HKEY_LOCAL_MACHINE，位于密钥 [HKEY_LOCAL_MACHINE_软件_Microsoft_VisualStudio_99.0Exp_包]下的注册表中。

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
|`@`（默认值）|REG_SZ|`FigPrj Project VSPackage`|此已注册的 VSPackage（项目类型）的可本地化名称。|
|`InprocServer32`|REG_SZ|`%MODULE%`|项目类型 DLL 的路径。 IDE 加载此 DLL 并将 VSPackage CLSID `DllGetClassObject` <xref:Microsoft.VisualStudio.OLE.Interop.IClassFactory>传递给以用于<xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage>构造对象。|
|`CompanyName`|REG_SZ|`Microsoft`|开发项目类型的公司的名称。|
|`ProductName`|REG_SZ|`Figure Project Sample`|项目类型的名称。|
|`ProductVersion`|REG_SZ|`9.0`|项目类型版本的版本号。|
|`MinEdition`|REG_SZ|`professional`|正在注册的 VS 包版本。|
|`ID`|REG_DWORD|`%IDS_PACKAGE_LOAD_KEY%`|项目 VSPackage 的包加载键。 在环境启动后加载项目时验证密钥。|
|`DllName`|REG_SZ|`%RESOURCE_DLL%`|包含项目类型的本地化资源的卫星 DLL 的文件名。|
|`Path`|REG_SZ|`%RESOURCE_PATH%`|卫星 DLL 的路径。|
|`FigProjectsEvents`|REG_SZ|有关值，请参阅语句。|确定为此自动化事件返回的文本字符串。|
|`FigProjectItemsEvents`|REG_SZ|有关值，请参阅语句。|确定为此自动化事件返回的文本字符串。|

 以下所有示例都位于密钥 [HKEY_LOCAL_MACHINE_软件_Microsoft_VisualStudio_9.0Exp_项目]下的注册表中。

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
|`DisplayName`|REG_SZ|`#%IDS_PROJECT_TYPE%`|要从在"包"下注册的卫星 DLL 检索的名称的资源 ID。|
|`Package`|REG_SZ|`%CLSID_Package%`|在"包"下注册的 VS 包的类 ID。|
|`ProjectTemplatesDir`|REG_SZ|`%TEMPLATE_PATH%\FigPrjProjects`|项目模板文件的默认路径。 这些是新项目模板显示的文件。|
|`ItemTemplatesDir`|REG_SZ|`%TEMPLATE_PATH% \FigPrjProjectItems`|项目项目模板文件的默认路径。 这些是"添加新项目"模板显示的文件。|
|`DisplayProjectFileExtensions`|REG_SZ|`#%IDS_DISPLAY_PROJ_FILE_EXT%`|使 IDE 能够实现 **"打开"** 对话框。|
|`PossibleProjectExtensions`|REG_SZ|`figp`|IDE 用于确定要打开的项目是否由此项目类型（项目工厂）处理。 多个条目的格式是分号分隔列表。 例如"vdproj;vdp"。|
|`DefaultProjectExtension`|REG_SZ|`.figp`|IDE 用作"保存为"操作的默认文件名扩展名。|
|`Filter Settings`|REG_DWORD|各种，请参阅下表下的声明和注释。|这些设置用于设置用于在 UI 对话框中显示文件的各种筛选器。|
|`@`|REG_SZ|`#%IDS_ADDITEM_TEMPLATES_ENTRY%`|添加项目模板的资源 ID。|
|`TemplatesDir`|REG_SZ|`%TEMPLATE_PATH%\FigPrjProjectItems`|**"添加新项目**"模板的对话框中显示的项目项的路径。|
|`SortPriority`|REG_DWORD|`100 (vcprx64)`|确定"**添加新项目"** 对话框中显示的文件的树节点中的排序顺序。|

 下表显示了上一个代码段中可用的筛选器选项。

|筛选选项|描述|
|-------------------|-----------------|
|`CommonFindFilesFilter`|指示筛选器是"**在文件中查找**"对话框中的常见筛选器之一。 在筛选器未标记为公共之前，常见筛选器列在筛选器列表中。|
|`CommonOpenFilesFilter`|指示筛选器是 **"打开文件"** 对话框中的常见筛选器之一。 在筛选器未标记为公共之前，常见筛选器列在筛选器列表中。|
|`FindInFilesFilter`|指示筛选器将是"**在文件中查找**"对话框中的筛选器之一，并将列在常见筛选器之后。|
|`NotOpenFileFilter`|指示筛选器不会在 **"打开文件"** 对话框中使用。|
|`NotAddExistingItemFilter`|指示筛选器不会在"添加**现有项目**"对话框中使用。|

 默认情况下，如果筛选器没有设置一个或多个这些标志，则在列出公共筛选器后，"**添加现有项目**"对话框和 **"打开文件"** 对话框中使用筛选器。 筛选器不在"**在文件中查找"对话框中使用**。

 以下所有示例都位于密钥 [HKEY_LOCAL_MACHINE_软件_Microsoft_VisualStudio_9.0Exp_项目]下的注册表中。

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
|`TemplatesDir`|REG_SZ|`%TEMPLATE_PATH%\FigPrjProjects`|已注册项目类型的项目的默认路径。|
|`SortPriority`|REG_DWORD|`41 (x29)`|设置"新建项目"向导对话框中显示的项目的排序顺序。|
|`NewProjectDialogOnly`|REG_DWORD|`0`|0 表示此类型的项目仅在"新项目"对话框中显示。|

 以下所有示例都位于密钥 [HKEY_LOCAL_MACHINE_软件_Microsoft_VisualStudio_9.0Exp_项目]下的注册表中。

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
|`@`|REG_SZ|无|默认值，指示以下条目用于"杂项文件"项目条目。|
|`@`|REG_SZ|`#%IDS_ADDITEM_TEMPLATES_ENTRY%`|"添加新项目"模板文件的资源 ID 值。|
|`TemplatesDir`|REG_SZ|`%TEMPLATE_PATH%\FigPrjProjectItems`|将在"**添加新项目**"对话框中显示的项目的默认路径。|
|`SortPriority`|REG_DWORD|`100 (vcprx64)`|建立在 **"添加新项目**"对话框的树节点中的显示的排序顺序。|

 下面的示例位于注册表下的关键 [HKEY_LOCAL_MACHINE_软件_微软_VisualStudio_9.0Exp_Menus]。

## <a name="example"></a>示例

```
"{ACEF4EB2-57CF-11D2-96F4-000000000000}"=",1000,1"
```

 菜单条目将 IDE 指向用于检索菜单信息的资源。 当此数据合并到菜单数据库中时，注册表的"菜单合并"部分将添加相同的密钥。 VSPackage 不应直接修改"菜单合并"部分下的任何内容。 在下表中的"数据"字段中，有三个逗号分隔字段。 第一个字段标识菜单资源文件的完整路径：

- 如果省略了第一个字段，则菜单资源将从 VSPackage GUID 标识的卫星 DLL 加载。

  第二个字段标识 CTMENU 类型的菜单资源 ID：

- 如果指定了资源 ID，并且文件路径由第一个参数提供，则从完整文件路径加载菜单资源。

- 如果提供了资源 ID，但文件路径未提供，则菜单资源将从附属 DLL 加载。

- 如果提供了完整的文件路径，并且省略了资源 ID，则要加载的文件应为 CTO 文件。

  最后一个字段标识 CTMENU 资源的版本号。 您可以通过更改版本号再次合并菜单。

|名称|类型|数据|描述|
|----------|----------|----------|-----------------|
|%CLSID_Package%|REG_SZ|`,1000,1`|要检索菜单信息的资源。|

 以下所有示例都位于密钥 [HKEY_LOCAL_MACHINE_软件_Microsoft_VisualStudio_9.0Exp_NewProjectTemplates] 下的注册表中。

```
\TemplateDirs\{ACEF4EB2-57CF-11D2-96F4-000000000000}\1                (CLSID for Figures Project projects)
   @="#7"
   "TemplatesDir"="<Visual Studio SDK installation path>\\VSIntegration\\Archive9.0\\FigPkgs\\FigPrj\\FigPrjProjects"
   "SortPriority"=dword:00000029
   "NewProjectDialogOnly"=dword:00000000
```

|名称|类型|数据|描述|
|----------|----------|----------|-----------------|
|`@`|REG_SZ|`#%IDS_NEWPROJ_TEMPLATES_ENTRY%`|图形项目新项目模板的资源 ID 值。|
|`TemplatesDir`|REG_SZ|`%TEMPLATE_PATH%\FigPrjProjects`|"新项目"目录的默认路径。 此目录中的项目将显示在 **"新项目"向导**对话框中。|
|`SortPriority`|REG_DWORD|`41 (x29)`|确定项目将在 **"新项目"** 对话框的树节点中显示的顺序。|
|`NewProjectDialogOnly`|REG_DWORD|`0`|0 表示此类型的项目仅在 **"新项目**"对话框中显示。|

 下面的示例位于密钥 [HKEY_LOCAL_MACHINE_软件_Microsoft_VisualStudio_9.0Exp_已安装产品]下的注册表中。

```
\FiguresProductSample
   "Package"="{ACEF4EB2-57CF-11D2-96F4-000000000000}"
   "UseInterface"=dword:00000001
```

|名称|类型|数据|描述|
|----------|----------|----------|-----------------|
|`Package`|REG_SZ|`%CLSID_Package%`|已注册的 VSPackage 的类 ID。|
|`UseInterface`|REG_DWORD|`1`|1 表示 UI 将用于与此项目进行交互。 0 表示没有 UI 接口。|

 控制新项目类型的.vsz 文件通常包含RELATIVE_PATH项。 此路径与以下安装程序键中的项目类型的 #ProductDir 条目下指定的路径相关：

 HKEY_LOCAL_MACHINE_SOFTWARE_微软_VisualStudio_7.0Exp_安装程序

 例如，企业框架项目模板添加以下注册表项：

 HKEY_LOCAL_MACHINE_SOFTWARE_微软_VisualStudio_7.0Exp_安装程序_产品Dir = C：程序文件_微软视觉工作室_企业框架]

 这意味着，如果在 .vsz 文件中包含 PROJECT_TYPE_EF 条目，则环境将查找之前指定的 ProductDir 目录中的 .vsz 文件。

## <a name="see-also"></a>请参阅
- [清单：新建项目类型](../../extensibility/internals/checklist-creating-new-project-types.md)
- [项目模型的元素](../../extensibility/internals/elements-of-a-project-model.md)
- [使用项目工厂创建项目实例](../../extensibility/internals/creating-project-instances-by-using-project-factories.md)
