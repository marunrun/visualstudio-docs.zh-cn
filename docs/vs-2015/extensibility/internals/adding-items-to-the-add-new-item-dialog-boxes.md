---
title: 将项添加到添加新项对话框 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- Add New Item dialog box, adding items
ms.assetid: 2f70863b-425b-4e65-86b4-d6a898e29dc7
caps.latest.revision: 19
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: ecdacfc4ac65e0dc18512bfb56eb870545c66a9b
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63443478"
---
# <a name="adding-items-to-the-add-new-item-dialog-boxes"></a>将项添加到“添加新项”对话框
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

将项添加到的过程**添加新项**对话框的开头的注册表项。 以下注册表项中所示，AddItemTemplates 部分包含的路径和名称中提供的项中的目录**添加新项**放入对话框。  
  
> [!NOTE]
> 紧跟代码段的表包含有关注册表项的其他信息。  
  
 本部分位于 [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\14.0Exp\Projects] 下。  
  
 首个 GUID 是此类型; 的项目的 CLSID第二个 GUID 指示添加的项模板的已注册的项目类型。  
  
 \\{C061DB26-5833-11D2-96F5-000000000000}\AddItemTemplates\TemplateDirs\ {ACEF4EB2-57CF-11D2-96F4-000000000000}\1  
  
 @="#6"  
  
 "TemplatesDir"="\<Visual Studio SDK installation path\\\VSIntegration\\\SomeFolder\\\SomePackage\\\SomeProject\\\SomeProjectItems"  
  
 "SortPriority"=dword:00000064  
  
|名称|类型|（从.rgs 文件） 的数据|描述|  
|----------|----------|-----------------------------|-----------------|  
|@ （默认值）|REG_SZ|#%IDS_ADDITEM_TEMPLATES_ENTRY%|资源 ID**添加项**模板。|  
|Val TemplatesDir|REG_SZ|%TEMPLATE_PATH%\SomeProjectItems|在对话框中显示的项目项的路径**添加新项**向导。|  
|Val SortPriority|REG_DWORD|100 ([!INCLUDE[vcprx64](../../includes/vcprx64-md.md)])|确定文件中显示的树节点中的排序顺序**添加新项**对话框。|  
  
> [!NOTE]
> 对于 Visual C# 和 Visual Basic 项目类型 GUID 是按如下所示：[!INCLUDE[csprcs](../../includes/csprcs-md.md)]: {FAE04EC0-301F-11D3-BF4B-00C04F79EFBC}[!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]: {F184B08F-C81C-45F6-A57F-5ABD9991F28F}  
  
 该目录所列的 TemplateDirs，为 %template_path%\someprojectitems，是在左侧的节点**添加新项**对话框框树。 在树中的其他元素都基于该根目录中的子目录。 可用于添加到项目文件是在右窗格中的项**添加新项**对话框。  
  
 通常情况下，此文件夹将包含如模板 HTML 或.cpp 文件中，你的项目的模板文件并启动向导的任何.vsz 文件。 若要控制项的显示方式，还可以包括用于本地化的目录名称和图标的.vsdir 文件。 已本地化的字符串是在表示此节点中添加新项对话框中树的对话框中显示的标题。  
  
 但是，没有一个.vsdir 文件中将所有内容。 您可以在目录中的每个项的一个.vsdir 文件。 有关详细信息，请参阅[向导 (。在 Vsz) 文件](../../extensibility/internals/wizard-dot-vsz-file.md)和[模板目录说明 (。Vsdir) 文件](../../extensibility/internals/template-directory-description-dot-vsdir-files.md)。  
  
> [!NOTE]
> 模板目录中的.vsdir 文件是可选的。 如果只是想要将在目录中的项目元素和其显示在**添加新项**对话框中，可以将此文件放在 TemplatesDir 语句中指定的模板目录中。 然后，该文件将显示在右窗格中**添加新项**对话框中的为该项目。 但是，如果你想要显示的文件或图标的本地化的标题，则必须包含至少一个.vsdir 文件模板目录中。  
  
## <a name="grouping-project-items"></a>分组项目项  
 如果你想要包含在文件夹中的模板组**添加新项**对话框框树中，你必须使用项模板根目录下的子目录中。 当**添加新项**向用户显示对话框中，它们还可以查看子文件夹，并可以从中选择项目元素。  
  
 代码段中的排序优先级确定将其中相对于其他元素的树节点在树中创建此模板目录。 有关**添加新项**对话框中，排序优先级是所有必须包括，以便你的项将显示在对话框中正确的位置。  
  
 您还可以实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg2>接口以筛选器中显示的内容**添加新项**对话框。 通过实现此接口，您可以设置一个模板目录包含，例如，磁盘上 50 个模板和向导文件。 这种方式，您可以使用 20 个属于一个项目类型、 属于另一种项目类型，其他 30 文件和常规类型的项目中可用的所有文件的文件的不同项目类型。 在这种方式，具体取决于哪个项目创建模板，可以显示一组不同的模板文件。  
  
 例如，在 Visual Basic 项目中，可能会有 Web 项目和客户端项目。 Web 窗体不是有用的项将添加到客户端项目和 windows 窗体不是有用的项将添加到 Web 服务器项目。 因此，您可以创建一个包含两种类型的项目的所有文件的模板目录。 然后通过实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg2>，可以隐藏不应显示的项目或项目中的项目设置的类型的项。  
  
## <a name="filtering-project-items"></a>筛选项目项  
 `IVsFilterAddProjectItemDlg2` 提供了用于筛选元素树 （左窗格） 和项目文件 （右窗格） 中的以下方面：  
  
- 本地化的名称 （.vsdir 文件中包含的对话框中显示的标题） 通过提供`IVsFilterAddProjectItemDlg`。  
  
- 通过文件和磁盘上的文件夹的实际名称 (非本地化 — 没有.vsdir 文件) 提供的`IVsFilterAddProjectItemDlg`。  
  
- 按类别提供`IVsFilterAddProjectItemDlg2`。  
  
  若要按类别筛选，请提供连接到某个.vsdir 文件，如"Web 窗体"中的项或在 Visual Basic 中的"客户端项"中的类别字符串。 然后，对话框代码从.vsdir 文件中检索类别分类，并将其传递给你。 然后可以将该信息传递到你的实现`IVsFilterAddProjectItemDlg2`来筛选**添加新项**对话框中的类别。 为网页或客户端 Win32 应用程序的情况下，还可以筛选项。 此外，可以指定[!INCLUDE[vcprvc](../../includes/vcprvc-md.md)]标记为 Microsoft 基础类 (MFC) 或活动模板库 (ATL) 项的项。 时识别出这些项，项目系统可定义其自己的分类，以便系统可以根据类别和分类筛选。  
  
  如果你实现此筛选器功能，您无需映射应隐藏的每个项的表。 只需对项进行分类到类型并置于.vsdir 文件或文件的分类。 然后您可以隐藏任何通过实现接口中有某个特定分类的项。 在这种方式，可以进行中的项**添加新项**对话框框中动态根据项目中的状态。  
  
## <a name="see-also"></a>请参阅  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg2>   
 [注册项目和项模板](../../extensibility/internals/registering-project-and-item-templates.md)   
 [对象通常用于扩展项目的 Catid](../../extensibility/internals/catids-for-objects-that-are-typically-used-to-extend-projects.md)   
 [添加项目和项目项模板](../../extensibility/internals/adding-project-and-project-item-templates.md)   
 [模板目录说明 (。Vsdir) 文件](../../extensibility/internals/template-directory-description-dot-vsdir-files.md)   
 [向导 (.Vsz) 文件](../../extensibility/internals/wizard-dot-vsz-file.md)
