---
title: 注册项目和项目模板 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], adding items
- registry, Add New Item dialog box
- Add New Item dialog box
- Add New Project dialog box
- registry, Add New Project dialog box
ms.assetid: 6b909f93-d7f5-4aec-81c6-ee9ff0f31638
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: b64504c39b1fc3c4a82530b265cfd0e96832b4f2
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80705827"
---
# <a name="registering-project-and-item-templates"></a>注册项目和项模板
项目类型必须注册其项目和项目项目模板所在的目录。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]使用与项目类型关联的注册信息来确定要在 **"添加新项目和****添加新项目**"对话框中显示的内容。

 有关模板的详细信息，请参阅[添加项目和项目项目模板](../../extensibility/internals/adding-project-and-project-item-templates.md)。

## <a name="registry-entries-for-projects"></a>项目的注册表项
 以下示例显示HKEY_LOCAL_MACHINE\软件\微软_VisualStudio\\<*版本*>下的注册表项。 随附的表说明了示例中使用的元素。

```
[Projects\{ProjectGUID}]
@="MyProjectType"
"DisplayName"="#2"
"Package"="{VSPackageGUID}"
"ProjectTemplatesDir"="C:\\MyProduct\\MyProjectTemplates"
```

|名称|类型|说明|
|----------|----------|-----------------|
|@|REG_SZ|此类项目的默认名称。|
|DisplayName|REG_SZ|要从在"包"下注册的卫星 DLL 检索的名称的资源 ID。|
|程序包|REG_SZ|在"包"下注册的包的类 ID。|
|项目模板Dir|REG_SZ|项目模板文件的默认路径。 项目模板文件由**新项目**模板显示。|

### <a name="registering-item-templates"></a>注册项目模板
 您必须注册存储项目模板的目录。

```
[Projects\{ProjectGUID}\AddItemTemplates\TemplateDirs\{VSPackageGUID}\1]
@="#7"
"TemplatesDir"="C:\\MyProduct\\MyProjectItemTemplates "
"TemplatesLocalizedSubDir"="#10"
"SortPriority"=dword:00000064
```

| 名称 | 类型 | 说明 |
|--------------------------|-----------| - |
| @ | REG_SZ | 添加项目模板的资源 ID。 |
| 模板迪尔 | REG_SZ | **"添加新项目**"向导的对话框中显示的项目项的路径。 |
| 模板本地化子 Dir | REG_SZ | 命名保存本地化模板的 TemplatesDir 子目录的字符串的资源 ID。 由于[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]如果具有附属 DLL，则从附属 DLL 加载字符串资源，因此每个附属 DLL 可以包含不同的本地化子目录名称。 |
| 排序优先级 | REG_DWORD | 设置排序优先级以控制模板在"**添加新项目**"对话框中的显示顺序。 较大的排序优先级值出现在模板列表中的较早位置。 |

### <a name="registering-file-filters"></a>注册文件筛选器
 或者，您可以注册在提示文件名时[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]使用的筛选器。 例如，"[!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)]**打开文件"** 对话框的筛选器是：

 **可视化 C#\*文件（.cs、.resx、.\*\*设置、.xsd、.wsdl）;\*\*\*.cs，\*.resx，\*.\*设置， .xsd，\*.wsdl）**

 为了支持多个筛选器的注册，每个\\<筛选器在HKEY_LOCAL_MACHINE\软件\Microsoft_VisualStudio*版本*>_项目\\[\<*ProjectGUID*>]\\<下>"下注册自己的子*键*。 子键名称是任意的;[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]忽略子键的名称，只使用其值。

 您可以通过设置标记来控制使用筛选器的上下文，如下表所示。 如果筛选器未设置任何标志，它将在"**添加现有项目**"对话框和 **"打开文件"** 对话框中的常用筛选器之后列出，但不会在"**在文件中查找**"对话框中使用。

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

|名称|类型|说明|
|----------|----------|-----------------|
|常见查找文件筛选器|REG_DWORD|使筛选器成为"**在文件中查找**"对话框中的常见筛选器之一。 在筛选器未标记为公共筛选器之前，筛选器将列在筛选器列表中。|
|常见打开文件筛选器|REG_DWORD|使筛选器成为 **"打开文件"** 对话框中常见的筛选器之一。 在筛选器未标记为公共筛选器之前，筛选器将列在筛选器列表中。|
|查找文件筛选器|REG_DWORD|在"**在文件中查找**"对话框中列出常见筛选器后筛选器。|
|未打开文件筛选器|REG_DWORD|指示筛选器未在 **"打开文件"** 对话框中使用。|
|未添加现有项目筛选器|REG_DWORD|指示筛选器未在 **"添加现有项目"** 对话框中使用。|
|排序优先级|REG_DWORD|设置排序优先级以控制筛选器的显示顺序。 较大的排序优先级值出现在筛选器列表中的较早位置。|

## <a name="directory-structure"></a>目录结构
 只要位置是通过集成开发环境 （IDE） 注册，VS包就可以将模板文件和文件夹放在本地或远程磁盘上的任意位置。 但是，为了便于组织，我们建议在产品的安装路径下采用以下目录结构。

 *模板

 *项目（包含项目模板）

 *应用

 *组件

 \ ...

 *项目项目（包含项目项）

 *类

 *表格

 *网页

 •帮助文件（包含多文件项目项中使用的文件）

 *向导文件

## <a name="see-also"></a>请参阅

- [添加项目和项目项模板](../../extensibility/internals/adding-project-and-project-item-templates.md)
- [向导](../../extensibility/internals/wizards.md)
- [本地化应用程序](../../ide/globalizing-and-localizing-applications.md)
- [通常用于扩展项目的对象的 CATID](../../extensibility/internals/catids-for-objects-that-are-typically-used-to-extend-projects.md)
