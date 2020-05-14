---
title: 使用打开的文件命令显示文件 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project types, supporting Open File command
- Open File command
- persistence, supporting Open File command
ms.assetid: 4fff0576-b2f3-4f17-9769-930f926f273c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: cc18442c55b6989c4d8668e1425fdd62a2d4b1b6
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80708599"
---
# <a name="display-files-by-using-the-open-file-command"></a>使用"打开文件"命令显示文件
以下步骤描述 IDE 如何处理**打开文件**命令，该命令在 中的 **"文件"** 菜单中[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]可用。 这些步骤还描述了项目应如何响应源自此命令的调用。

 当用户单击 **"文件**"菜单上的 **"打开文件"** 命令，并从 **"打开文件"** 对话框中选择文件时，将发生以下过程：

1. 使用正在运行的文档表，IDE 确定文件是否已在项目中打开。

    - 如果文件处于打开状态，IDE 将重新显示窗口。

    - 如果文件未打开，IDE 将调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.IsDocumentInProject%2A>查询每个项目以确定哪个项目可以打开该文件。

        > [!NOTE]
        > 在 的项目实现中<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.IsDocumentInProject%2A>，提供了一个优先级值，指示项目打开文件的水平。 枚举中<xref:Microsoft.VisualStudio.Shell.Interop.VSDOCUMENTPRIORITY>提供了优先级值。

2. 每个项目都响应一个优先级，指示它是打开文件的项目的重要性。

3. IDE 使用以下条件来确定哪个项目打开文件：

    - 使用最高优先级 （`DP_Intrinsic`） 响应的项目将打开该文件。 如果多个项目响应此优先级，则第一个响应的项目将打开该文件。

    - 如果没有项目以最高优先级 （）`DP_Intrinsic`响应，但所有项目都响应相同的较低优先级，则活动项目将打开该文件。 如果没有项目处于活动状态，则第一个响应的项目将打开该文件。

    - 如果没有项目声明文件的所有权 （），`DP_Unsupported`则"杂项文件"项目将打开该文件。

         如果创建了"杂项文件"项目的实例，则项目始终响应该值`DP_CanAddAsExternal`。 此值指示项目可以打开该文件。 此项目用于容纳不在任何其他项目中的打开文件。 此项目中的项目列表不持久化;因此，该项目中的项目列表不会保留。仅当此项目用于打开文件时，该项目才在**解决方案资源管理器**中可见。

         如果"杂项文件"项目未指示可以打开该文件，则尚未创建该项目的实例。 在这种情况下，IDE 将创建"杂项文件"项目的实例，并告诉项目打开该文件。

4. 一旦 IDE 确定哪个项目打开该文件，它将调用该项目上<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.OpenItem%2A>的方法。

5. 然后，项目可以选择使用特定于项目的编辑器或标准编辑器打开文件。 有关详细信息，请参阅[如何：打开特定于项目的编辑器](../../extensibility/how-to-open-project-specific-editors.md)和[如何：分别打开标准编辑器](../../extensibility/how-to-open-standard-editors.md)。

## <a name="see-also"></a>请参阅
- [使用"打开使用"命令显示文件](../../extensibility/internals/displaying-files-by-using-the-open-with-command.md)
- [打开并保存项目项目项](../../extensibility/internals/opening-and-saving-project-items.md)
- [如何：打开特定于项目的编辑器](../../extensibility/how-to-open-project-specific-editors.md)
- [如何：打开标准编辑器](../../extensibility/how-to-open-standard-editors.md)
