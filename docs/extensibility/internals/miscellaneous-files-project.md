---
title: 杂项文件项目 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- files, adding existing files to solutions
- Miscellaneous Files project
- Solution Items folder
- files, opening with Miscellaneous Files project
ms.assetid: 93a278a8-d4f4-400b-8945-4f1b0a2b5bac
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 95cc1312fb7b381e1e20df834698480295fadcc8
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80707102"
---
# <a name="miscellaneous-files-project"></a>杂项文件项目
当用户打开项目项时，IDE 会分配给"杂项文件"项目不是解决方案中任何项目的成员的任何项。

 项目在确定用户打开项目项时使用哪个编辑器方面发挥着重要作用。 项目可以设计为使用特定于项目的编辑器或标准编辑器打开某些文件。

 特定于项目的编辑器通常要求用户具有特殊知识或使用项目的特殊接口。 有关详细信息，请参阅[如何：打开特定于项目的编辑器](../../extensibility/how-to-open-project-specific-editors.md)。

 标准编辑器可以在任何项目中打开特定扩展名的任何文件。 用户可以为项目自定义一些标准编辑器（如[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]文本编辑器），但仍保留其公共字符。 使用<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A>方法创建标准编辑器。

 如果解决方案中没有项目响应它可以打开项目项，IDE 会提供一个名为"杂项文件"项目的特殊项目，该项目将打开任何文件。

 此特殊项目提供在项目上下文之外打开文件。 在处理<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenDocumentViaProject%2A>该方法期间，"杂项文件"项目始终以非常低的优先级响应。 因此，杂项文件项目始终生成给任何可以打开文件的更高优先级的项目。

 "杂项文件"项目不要求用户使用 **"新项目**"对话框显式创建它。 此外，杂项文件项目不会永久管理项目成员的列表。 它使用可选功能为每个用户记录最近使用的文件的列表。

## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument>
- <xref:Microsoft.VisualStudio.Shell.Interop.VSDOCUMENTPRIORITY>
- [如何：打开项目特定的编辑器](../../extensibility/how-to-open-project-specific-editors.md)
- [如何：打开标准编辑器](../../extensibility/how-to-open-standard-editors.md)
- [添加项目和项目项模板](../../extensibility/internals/adding-project-and-project-item-templates.md)
- [添加项目和项目项模板](../../extensibility/internals/adding-project-and-project-item-templates.md)
