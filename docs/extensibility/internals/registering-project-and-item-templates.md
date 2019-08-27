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
ms.openlocfilehash: 84beaf97bda8d94872be22c6f5d247a746d1ecd3
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66319501"
---
# <a name="registering-project-and-item-templates"></a>注册项目和项模板
项目类型必须注册其项目和项目项模板的位置的目录。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 使用与您的项目类型关联的注册信息以确定要在中显示**添加新项目**并**添加新项**对话框。

 有关模板的详细信息，请参阅[添加项目和项目项模板](../../extensibility/internals/adding-project-and-project-item-templates.md)。

## <a name="registry-entries-for-projects"></a>项目的注册表项
 下面的示例演示注册表项下 HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\\<*版本*>。 随附的表列出了在示例中使用的元素。

```
[Projects\{ProjectGUID}]
@="MyProjectType"
"DisplayName"="#2"
"Package"="{VSPackageGUID}"
"ProjectTemplatesDir"="C:\\MyProduct\\MyProjectTemplates"
```

|名称|类型|描述|
|----------|----------|-----------------|
|@|REG_SZ|这种类型的项目的默认名称。|
|DisplayName|REG_SZ|包下注册的名称的资源 ID 来检索从附属 DLL。|
|package|REG_SZ|在包下已注册包的类 ID。|
|ProjectTemplatesDir|REG_SZ|默认项目模板文件的路径。 项目模板文件将由**新的项目**模板。|

### <a name="registering-item-templates"></a>注册项模板
 必须注册您在其中存储项模板的目录。

```
[Projects\{ProjectGUID}\AddItemTemplates\TemplateDirs\{VSPackageGUID}\1]
@="#7"
"TemplatesDir"="C:\\MyProduct\\MyProjectItemTemplates "
"TemplatesLocalizedSubDir"="#10"
"SortPriority"=dword:00000064
```

| 名称 | 类型 | 描述 |
|--------------------------|-----------| - |
| @ | REG_SZ | 添加项模板的资源 ID。 |
| TemplatesDir | REG_SZ | 在对话框中显示的项目项的路径**添加新项**向导。 |
| TemplatesLocalizedSubDir | REG_SZ | 资源 ID 的字符串的名称的 TemplatesDir 子目录包含本地化的模板。 因为[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]负载中的字符串资源附属 Dll 时，每个附属 DLL 可以包含不同的本地化的子目录名称。 |
| SortPriority | REG_DWORD | 设置以控制模板中的显示的顺序的 SortPriority**添加新项**对话框。 模板列表中较早出现较大的 SortPriority 值。 |

### <a name="registering-file-filters"></a>注册文件筛选器
 （可选） 可以注册筛选器的[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]使用提示输入文件名。 例如，[!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)]筛选**打开文件**对话框：

 **Visual C# 文件 (\*.cs，\*.resx\*.settings，\*.xsd，\*.wsdl);\*。cs，\*.resx\*.settings，\*.xsd，\*.wsdl)**

 若要支持多个筛选器的注册，每个筛选器中注册其自己的子项下 HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\\<*版本*> \Projects\\{\< *ProjectGUID*>} \Filters\\<*子项*>。 子项名称是任意;[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]忽略子项的名称，并使用只是它的值。

 您可以控制在其中通过设置标志，如下表中所示使用筛选器的上下文。 如果筛选器没有设置任何标志，它将列中的常见筛选器后**添加现有项**对话框和**打开的文件**对话框中，但它不会在使用**在文件中查找**对话框。

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

|名称|类型|描述|
|----------|----------|-----------------|
|CommonFindFilesFilter|REG_DWORD|使常用筛选器之一中的筛选**在文件中查找**对话框。 前面未标记为常见的筛选器的筛选器列表中列出了常用筛选器。|
|CommonOpenFilesFilter|REG_DWORD|使常用筛选器之一中的筛选**打开的文件**对话框。 前面未标记为常见的筛选器的筛选器列表中列出了常用筛选器。|
|FindInFilesFilter|REG_DWORD|列出筛选器中的常见筛选器后**在文件中查找**对话框。|
|NotOpenFileFilter|REG_DWORD|指示中不使用筛选器**打开的文件**对话框。|
|NotAddExistingItemFilter|REG_DWORD|指示中不使用筛选器**添加现有项**对话框。|
|SortPriority|REG_DWORD|设置 SortPriority 来控制筛选器的显示的顺序。 筛选器列表中较早出现较大的 SortPriority 值。|

## <a name="directory-structure"></a>目录结构
 Vspackage 可以将模板文件和文件夹任意位置在本地或远程磁盘上，只要通过集成的开发环境 (IDE) 中注册的位置。 但是，为了便于组织，我们建议您的产品的安装路径下的以下目录结构。

 \Templates

 \Projects （包含的项目模板）

 \Applications

 \Components

 \ ...

 \ProjectItems （包含项目项）

 \Class

 \Form

 \Web Page

 \HelperFiles （包含多文件项目项中使用的文件）

 \WizardFiles

## <a name="see-also"></a>请参阅

- [添加项目和项目项模板](../../extensibility/internals/adding-project-and-project-item-templates.md)
- [向导](../../extensibility/internals/wizards.md)
- [本地化应用程序](../../ide/globalizing-and-localizing-applications.md)
- [通常用于扩展项目的对象的 CATID](../../extensibility/internals/catids-for-objects-that-are-typically-used-to-extend-projects.md)