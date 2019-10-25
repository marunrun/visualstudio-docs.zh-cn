---
title: 注册项目和项模板 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], adding items
- registry, Add New Item dialog box
- Add New Item dialog box
- Add New Project dialog box
- registry, Add New Project dialog box
ms.assetid: 6b909f93-d7f5-4aec-81c6-ee9ff0f31638
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 2e35a476ab8fe8d8de3ce11dd117de4c84a3befa
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72724629"
---
# <a name="registering-project-and-item-templates"></a>注册项目和项模板
项目类型必须注册其项目和项目项模板所在的目录。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 使用与项目类型关联的注册信息来确定要在 "**添加新项目**" 和 "**添加新项**" 对话框中显示的内容。

 有关模板的详细信息，请参阅[添加项目和项目项模板](../../extensibility/internals/adding-project-and-project-item-templates.md)。

## <a name="registry-entries-for-projects"></a>项目的注册表项
 以下示例显示 HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio \\ <*版本*> 下的注册表项。 随附的表解释了示例中使用的元素。

```
[Projects\{ProjectGUID}]
@="MyProjectType"
"DisplayName"="#2"
"Package"="{VSPackageGUID}"
"ProjectTemplatesDir"="C:\\MyProduct\\MyProjectTemplates"
```

|“属性”|键入|描述|
|----------|----------|-----------------|
|@|REG_SZ|此类型的项目的默认名称。|
|DisplayName|REG_SZ|要从在包下注册的附属 DLL 检索的名称的资源 ID。|
|Package|REG_SZ|包中注册的包的类 ID。|
|ProjectTemplatesDir|REG_SZ|项目模板文件的默认路径。 项目模板文件由**新项目**模板显示。|

### <a name="registering-item-templates"></a>注册项模板
 必须注册存储项模板的目录。

```
[Projects\{ProjectGUID}\AddItemTemplates\TemplateDirs\{VSPackageGUID}\1]
@="#7"
"TemplatesDir"="C:\\MyProduct\\MyProjectItemTemplates "
"TemplatesLocalizedSubDir"="#10"
"SortPriority"=dword:00000064
```

| “属性” | 键入 | 描述 |
|--------------------------|-----------| - |
| @ | REG_SZ | 添加项模板的资源 ID。 |
| TemplatesDir | REG_SZ | 显示在 "**添加新项**向导" 对话框中的项目项的路径。 |
| TemplatesLocalizedSubDir | REG_SZ | 命名包含本地化模板的 TemplatesDir 子目录的字符串的资源 ID。 由于 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 从附属 Dll 加载字符串资源（如果有），因此每个附属 DLL 都可以包含一个不同的本地化子目录名称。 |
| SortPriority | REG_DWORD | 设置 SortPriority 以控制模板在 "**添加新项**" 对话框中的显示顺序。 较大的 SortPriority 值将显示在模板列表中较早的值。 |

### <a name="registering-file-filters"></a>注册文件筛选器
 或者，你可以注册 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 在提示输入文件名时使用的筛选器。 例如，"**打开文件**" 对话框的 "[!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] 筛选器是：

 **视觉C#文件（\* .cs、\* .resx \*、\*、\*）;\* .cs，\* .resx \*，0 .xsd，1）**

 为了支持注册多个筛选器，每个筛选器都在 HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio \\ <*Version*> \Projects \\ {\<*ProjectGUID*>} \Filters<*子项*> \\。 子项名称为任意; [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 忽略子项的名称，并只使用其值。

 您可以通过设置标志来控制使用筛选器的上下文，如下表所示。 如果筛选器没有设置任何标志，则该筛选器将在 "**添加现有项**" 对话框和 "**打开文件**" 对话框中的常见筛选器后列出，但不会在 "在**文件中查找**" 对话框中使用。

```
[Projects\{ProjectGUID}\Filters\MyLanguageFilter]
@="#3"
"CommonOpenFilesFilter"=dword:00000000
"CommonFindFilesFilter"=dword:00000000
"FindInFilesFilter"=dword:00000000
"NotOpenFileFilter"=dword:00000000
"NotAddExistingItemFilter"=dword:00000000
"SortPriority"=dword:00000064
```

|“属性”|键入|描述|
|----------|----------|-----------------|
|CommonFindFilesFilter|REG_DWORD|使筛选器在 "**在文件中查找**" 对话框中的一个公共筛选器。 筛选器列表中会列出常见筛选器，然后筛选器才会标记为公用筛选器。|
|CommonOpenFilesFilter|REG_DWORD|使筛选器 "**打开文件**" 对话框中的一个公共筛选器。 筛选器列表中会列出常见筛选器，然后筛选器才会标记为公用筛选器。|
|FindInFilesFilter|REG_DWORD|列出 "在**文件中查找**" 对话框中常见筛选器之后的筛选器。|
|NotOpenFileFilter|REG_DWORD|指示 "**打开文件**" 对话框中未使用筛选器。|
|NotAddExistingItemFilter|REG_DWORD|指示 "**添加现有项**" 对话框中未使用筛选器。|
|SortPriority|REG_DWORD|设置 SortPriority 来控制筛选器的显示顺序。 较大的 SortPriority 值将显示在筛选器列表中较早的值。|

## <a name="directory-structure"></a>目录结构
 只要通过集成开发环境（IDE）注册位置，Vspackage 就可以将模板文件和文件夹放置在本地或远程磁盘上的任何位置。 但是，为了便于组织，我们建议你在产品的安装路径下安装以下目录结构。

 \Templates

 \Projects （包含项目模板）

 \Applications and

 \Components

 \ ...

 \ProjectItems （包含项目项）

 \Class

 \Form

 \Web 页

 \HelperFiles （包含多文件项目项中使用的文件）

 \WizardFiles

## <a name="see-also"></a>请参阅

- [添加项目和项目项模板](../../extensibility/internals/adding-project-and-project-item-templates.md)
- [向导](../../extensibility/internals/wizards.md)
- [本地化应用程序](../../ide/globalizing-and-localizing-applications.md)
- [通常用于扩展项目的对象的 CATID](../../extensibility/internals/catids-for-objects-that-are-typically-used-to-extend-projects.md)