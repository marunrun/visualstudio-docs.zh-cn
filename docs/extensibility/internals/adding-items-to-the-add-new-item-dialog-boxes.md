---
title: 将项添加到添加新项对话框 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Add New Item dialog box, adding items
ms.assetid: 2f70863b-425b-4e65-86b4-d6a898e29dc7
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 61a9921103bf5954061fbb61c405ba1d36ffb782
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66328055"
---
# <a name="add-items-to-the-add-new-item-dialog-box"></a>将项目添加到添加新项对话框
将项添加到的过程**添加新项**对话框的开头的注册表项。 以下注册表项中所示**AddItemTemplates**部分包含的路径和名称的目录中提供哪些项**添加新项**放入对话框。

> [!NOTE]
> 紧跟代码段的表包含有关注册表项的其他信息。

 本部分位于**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\14.0Exp\Projects**。

 首个 GUID 是此类型; 的项目的 CLSID第二个 GUID 指示添加的项模板的已注册的项目类型：

 **\\{C061DB26-5833-11D2-96F5-000000000000}\\AddItemTemplates\\TemplatesDir\\{ACEF4EB2-57CF-11D2-96F4-000000000000}\\1**

 **@** = #6

 **TemplatesDir** = \\&lt;Visual Studio SDK 安装路径&gt;\\VSIntegration\\&lt;SomeFolder&gt; \\&lt;SomePackage&gt;\\&lt;SomeProject&gt;\\&lt;SomeProjectItems&gt;

 **SortPriority** = dword:00000064

| 名称 | 类型 | 数据 (从 *.rgs*文件) | 描述 |
|------------------|-----------| - | - |
| @ （默认值） | REG_SZ | #%IDS_ADDITEM_TEMPLATES_ENTRY% | 资源 ID**添加项**模板。 |
| Val TemplatesDir | REG_SZ | %TEMPLATE_PATH%\\&lt;SomeProjectItems&gt; | 在对话框中显示的项目项的路径**添加新项**向导。 |
| Val SortPriority | REG_DWORD | 100 ([!INCLUDE[vcprx64](../../extensibility/internals/includes/vcprx64_md.md)]) | 确定文件中显示的树节点中的排序顺序**添加新项**对话框。 |

> [!NOTE]
> Visual C# 和 Visual Basic 项目类型的 GUID 如下所示：
> - [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)]: {FAE04EC0-301F-11D3-BF4B-00C04F79EFBC}
> - [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)]: {F184B08F-C81C-45F6-A57F-5ABD9991F28F}

 为列出的目录**TemplatesDir**，即 *%template_path%\\&lt;SomeProjectItems&gt;* ，是在左侧的节点**添加新项**对话框框树。 在树中的其他元素都基于该根目录中的子目录。 可用于添加到项目文件是在右窗格中的项**添加新项**对话框。

 通常情况下，此文件夹将包含模板文件，例如模板 HTML 项目或 *.cpp*文件，以及任何 *.vsz*文件用于启动向导。 若要控制项的显示方式，还可以包括 *.vsdir*用于本地化的目录名称和图标的文件。 已本地化的字符串是在对话框中，表示此节点中的显示的标题**添加新项**对话框框树。

 但是，不需要已做好所有之一 *.vsdir*文件。 您可以将一个 *.vsdir*目录中的每个项的文件。 有关详细信息，请参阅[向导 (.vsz) 文件](../../extensibility/internals/wizard-dot-vsz-file.md)并[模板目录说明 (.vsdir) 文件](../../extensibility/internals/template-directory-description-dot-vsdir-files.md)。

> [!NOTE]
> *.Vsdir*模板目录中的文件是可选的。 如果只是想要将在目录中的项目元素和其显示在**添加新项**对话框中，可以将该文件放入中指定的模板目录**TemplatesDir**语句。 然后，该文件将显示在右窗格中**添加新项**对话框中的为该项目。 但是，如果你想要显示的文件或图标的本地化的标题，您必须包含至少一个 *.vsdir*模板目录中的文件。

## <a name="group-project-items"></a>项目项进行分组
 如果你想要包含在文件夹中的模板组**添加新项**对话框框树中，你必须使用项模板根目录下的子目录中。 当**添加新项**向用户显示对话框中，它们还可以查看子文件夹，并可以从中选择项目元素。

 代码段中的排序优先级确定将其中相对于其他元素的树节点在树中创建此模板目录。 有关**添加新项**对话框中，排序优先级是所有必须包括，以便你的项将显示在对话框中正确的位置。

 您还可以实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg2>接口以筛选器中显示的内容**添加新项**对话框。 通过实现此接口，您可以设置一个模板目录包含，例如，磁盘上 50 个模板和向导文件。 这种方式，您可以使用 20 个属于一个项目类型、 属于另一种项目类型，其他 30 文件和常规类型的项目中可用的所有文件的文件的不同项目类型。 在这种方式，具体取决于哪个项目创建模板，可以显示一组不同的模板文件。

 例如，在 Visual Basic 项目中，可能会有 Web 项目和客户端项目。 Web 窗体不是有用的项将添加到客户端项目和 windows 窗体不是有用的项将添加到 Web 服务器项目。 因此，您可以创建一个包含两种类型的项目的所有文件的模板目录。 然后，通过实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg2>，可以隐藏不应显示的项目或项目中的项目设置的类型的项。

## <a name="filter-project-items"></a>筛选器项目项
 `IVsFilterAddProjectItemDlg2` 提供了用于筛选元素树 （左窗格） 和项目文件 （右窗格） 中的以下方面：

- 本地化名称 (包含在对话框中显示的隐藏式字幕 *.vsdir*文件) 提供的`IVsFilterAddProjectItemDlg`。

- 通过文件和磁盘上的文件夹的实际名称 (非本地化 — 无 *.vsdir*文件) 提供的`IVsFilterAddProjectItemDlg`。

- 按类别提供`IVsFilterAddProjectItemDlg2`。

  若要按类别筛选，请提供中的项的类别字符串 *.vsdir*文件，如*Web 窗体*或*客户端项*在 Visual Basic 中。 对话框代码然后检索从类别分类 *.vsdir*文件，并将其传递给你。 然后可以将该信息传递到你的实现`IVsFilterAddProjectItemDlg2`来筛选**添加新项**对话框中的类别。 为网页或客户端 Win32 应用程序的情况下，还可以筛选项。 此外，可以指定[!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)]标记为 Microsoft 基础类 (MFC) 或活动模板库 (ATL) 项的项。 时识别出这些项，项目系统可定义其自己的分类，以便系统可以根据类别和分类筛选。

  如果你实现此筛选器功能，您无需映射应隐藏的每个项的表。 只需对项进行分类到类型并将分类放入 *.vsdir*文件。 然后您可以隐藏任何通过实现接口中有某个特定分类的项。 在这种方式，可以进行中的项**添加新项**对话框框中动态根据项目中的状态。

## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg2>
- [注册项目和项模板](../../extensibility/internals/registering-project-and-item-templates.md)
- [对象通常用于扩展项目的 Catid](../../extensibility/internals/catids-for-objects-that-are-typically-used-to-extend-projects.md)
- [添加项目和项目项模板](../../extensibility/internals/adding-project-and-project-item-templates.md)
- [模板目录说明 (.vsdir) 文件](../../extensibility/internals/template-directory-description-dot-vsdir-files.md)
- [向导 (.vsz) 文件](../../extensibility/internals/wizard-dot-vsz-file.md)