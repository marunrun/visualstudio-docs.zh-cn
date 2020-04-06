---
title: 将项目添加到"添加新项目"对话框 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Add New Item dialog box, adding items
ms.assetid: 2f70863b-425b-4e65-86b4-d6a898e29dc7
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: af7f9e5c792785a23ad1674a50abeb4eb6d3cba9
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80710218"
---
# <a name="add-items-to-the-add-new-item-dialog-box"></a>将项目添加到"添加新项目"对话框
向"**添加新项目**"对话框添加项的过程从注册表项开始。 如以下注册表项所示 **，"AddItemTemplates"** 部分包含目录的路径和名称，其中放置了"**添加新项目"** 对话框中提供的项。

> [!NOTE]
> 代码段紧接的表包含有关注册表项的其他信息。

 此部分位于**HKEY_LOCAL_MACHINE_SOFTWARE_微软[VisualStudio]14.0Exp_项目**下。

 第一个 GUID 是此类项目的 CLSID;第二个 GUID 指示"添加项目"模板的已注册项目类型：

 **\\[C061DB26-5833-11D2-96F5-0000000000]\\添加项目\\模板模板Dir\\[ACEF4EB2-57CF-11D2-96F4-00000000000000]\\1**

 **@**• #6

 **模板Dir** = \\&gt;\\\\&lt;&gt;\\&lt;&gt;\\&lt;&gt;\\可视化工作室 SDK 安装路径 VS集成一些文件夹一些包一些项目&lt;&lt;&gt;

 **排序优先级**= dword：00000064

| 名称 | 类型 | 数据（来自 *.rgs*文件） | 描述 |
|------------------|-----------| - | - |
| * （默认） | REG_SZ | ±%IDS_ADDITEM_TEMPLATES_ENTRY% | **添加项目**模板的资源 ID。 |
| 瓦尔模板Dir | REG_SZ | %TEMPLATE_PATH%\\&lt;某些项目项目&gt; | **"添加新项目**"向导的对话框中显示的项目项的路径。 |
| Val 排序优先级 | REG_DWORD | 100[!INCLUDE[vcprx64](../../extensibility/internals/includes/vcprx64_md.md)]（ ） | 确定"**添加新项目"** 对话框中显示的文件的树节点中的排序顺序。 |

> [!NOTE]
> Visual C# 和可视化基本项目类型的 GUIDS 如下所示：
> - [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)]： [FAE04EC0-301F-11D3-BF4B-00C04F79EFBC]
> - [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)]：[F184B08F-C81C-45F6-A57F-5ABD9991F28F]

 **TemplatesDir**列出的目录*\\&lt;（%TEMPLATE_PATH% 某些项目项目&gt;*）是 **"添加新项目"** 对话框树左侧的节点。 树中的其他元素基于该根目录中的子目录。 可添加到项目中的文件是 **"添加新项目"** 对话框右侧窗格中的项。

 通常，此文件夹将包含项目的模板文件，如模板 HTML 或 *.cpp*文件，以及用于启动向导的任何 *.vsz*文件。 要控制项目的显示方式，还可以包括用于本地化目录名称和图标的 *.vsdir*文件。 本地化字符串是显示在"**添加新项目"** 对话框树中表示此节点的对话框中显示的标题。

 但是，您不必在一个 *.vsdir*文件中拥有所有内容。 对于目录中的每个项目，可以有一个 *.vsdir*文件。 有关详细信息，请参阅向导[（.vsz） 文件和](../../extensibility/internals/wizard-dot-vsz-file.md)[模板目录说明 （.vsdir） 文件](../../extensibility/internals/template-directory-description-dot-vsdir-files.md)。

> [!NOTE]
> 模板目录中的 *.vsdir*文件是可选的。 如果只想将项目元素放在目录中并在 **"添加新项目"** 对话框中显示，则可以将该文件放在**模板表**表中指定的模板目录中。 然后，该文件将显示在该项目的"**添加新项目"** 对话框的右侧窗格中。 但是，如果要显示文件的本地化标题或图标，则必须在模板目录中至少包含一个 *.vsdir*文件。

## <a name="group-project-items"></a>组项目项
 如果要在 **"添加新项目"** 对话框树中的文件夹中包含模板组，则必须在根模板目录下具有包含其中项的子目录。 向用户显示"**添加新项目**"对话框时，他们还会看到子文件夹，并能够从这些文件夹中选择项目元素。

 代码段中的排序优先级确定在树中相对于树节点的其他元素创建此模板目录的位置。 对于"**添加新项目"** 对话框，排序优先级是必须包含的，以便项目将显示在对话框中的正确位置。

 您还可以实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg2>该接口来筛选"**添加新项目"** 对话框中显示的内容。 通过实现此接口，可以在磁盘上设置一个模板目录，其中包含 50 个模板和向导文件。 这样，您可以具有不同的项目类型，其中 20 个文件属于一个项目类型，其他 30 个文件属于另一个项目类型，所有文件都位于一般类型的项目中。 这样，根据创建的项目模板，可以显示一组不同的模板文件。

 例如，在可视化基本项目中，您可能具有 Web 项目和客户端项目。 Web 窗体不是要添加到客户端项目的有用项，并且窗口窗体不是要添加到 Web 服务器项目的有用项。 因此，您可以创建一个模板目录，其中包含这两种类型的项目的所有文件。 然后，通过实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg2>，可以隐藏不应根据项目中的项目或项目设置类型显示的项目。

## <a name="filter-project-items"></a>筛选项目项
 `IVsFilterAddProjectItemDlg2`提供以下列方式筛选树（左窗格）和项目文件（右窗格）中的元素：

- 由 提供的本地化名称（显示在 *.vsdir*文件中的对话框中显示的标题）。 `IVsFilterAddProjectItemDlg`

- 按 磁盘上的文件和文件夹（非本地化 = 没有 *.vsdir*文件）提供`IVsFilterAddProjectItemDlg`的实际名称。

- 按类别，由`IVsFilterAddProjectItemDlg2`提供。

  要按类别进行筛选，请向 *.vsdir*文件中的项（如 Visual Basic 中的*Web 窗体*或*客户端项*）提供类别字符串。 然后，对话框代码从 *.vsdir*文件检索类别分类并将其传递给您。 然后，您可以将该信息传递给 您的实现，`IVsFilterAddProjectItemDlg2`以按类别筛选"**添加新项目**"对话框。 您还可以筛选网页的项目或作为客户端 Win32 应用程序案例。 此外，您可以将标记的项目[!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)]标识为 Microsoft 基础类 （MFC） 或活动模板库 （ATL） 项。 标识这些项目时，项目系统可以定义自己的分类，以便可以根据类别和分类筛选系统。

  如果实现此筛选器功能，则不必映射应隐藏的每个项的表。 只需将项分类为类型，并将分类放在 *.vsdir*文件或文件中即可。 然后，您可以通过实现接口来隐藏具有特定分类的任何项。 这样，您可以根据项目中的状态使"**添加新项目"** 对话框中的项保持动态。

## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg2>
- [注册项目和项目模板](../../extensibility/internals/registering-project-and-item-templates.md)
- [通常用于扩展项目的对象的 CATID](../../extensibility/internals/catids-for-objects-that-are-typically-used-to-extend-projects.md)
- [添加项目和项目项目模板](../../extensibility/internals/adding-project-and-project-item-templates.md)
- [模板目录描述 （.vsdir） 文件](../../extensibility/internals/template-directory-description-dot-vsdir-files.md)
- [向导 （.vsz） 文件](../../extensibility/internals/wizard-dot-vsz-file.md)
