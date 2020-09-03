---
title: 使用 "打开文件" 命令显示文件 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80708599"
---
# <a name="display-files-by-using-the-open-file-command"></a>使用 "打开文件" 命令显示文件
以下步骤介绍了 IDE 如何处理 **打开文件** 命令，该命令可在中的 " **文件** " 菜单上找到 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。 这些步骤还说明了项目应如何响应源自此命令的调用。

 当用户单击 "**文件**" 菜单上的 "**打开文件**" 命令并从 "**打开文件**" 对话框中选择文件时，将发生以下过程：

1. IDE 使用正在运行的文档表来确定文件是否已在项目中打开。

    - 如果文件已打开，则 IDE resurfaces 窗口。

    - 如果该文件未打开，IDE 将调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.IsDocumentInProject%2A> 以查询每个项目，以确定可以打开该文件的项目。

        > [!NOTE]
        > 在的项目实现中 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.IsDocumentInProject%2A> ，提供一个优先级值，用于指示项目打开文件的级别。 在枚举中提供了优先级值 <xref:Microsoft.VisualStudio.Shell.Interop.VSDOCUMENTPRIORITY> 。

2. 每个项目都有一个优先级别，用于指示在项目中打开文件的重要性。

3. IDE 使用以下条件来确定打开文件的项目：

    - 用最高优先级 (进行响应的项目 `DP_Intrinsic`) 打开该文件。 如果有多个项目以此优先级进行响应，则第一个响应项目将打开文件。

    - 如果没有任何项目以优先级最高的 (`DP_Intrinsic`) ，但所有项目都以相同的低优先级进行响应，则活动项目将打开该文件。 如果没有活动的项目，则第一个响应项目将打开文件。

    - 如果没有项目声明文件 () 的所有权 `DP_Unsupported` ，则杂项文件项目会打开该文件。

         如果创建了杂项文件项目的实例，则该项目始终使用值进行响应 `DP_CanAddAsExternal` 。 此值指示项目可以打开文件。 此项目用于承载不在任何其他项目中的打开的文件。 此项目中的项列表不是持久的;仅当使用此项目打开文件时，此项目才会显示在 **解决方案资源管理器** 中。

         如果杂项文件项目不指示它可以打开文件，则表示尚未创建项目的实例。 在这种情况下，IDE 将创建杂项文件项目的实例，并通知项目打开该文件。

4. IDE 一旦确定打开文件的项目，就会 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.OpenItem%2A> 在该项目上调用方法。

5. 然后，该项目可以选择使用特定于项目的编辑器或标准编辑器打开文件。 有关详细信息，请参阅 [如何：打开项目特定的编辑器](../../extensibility/how-to-open-project-specific-editors.md) 和 [如何：打开标准编辑器](../../extensibility/how-to-open-standard-editors.md)。

## <a name="see-also"></a>请参阅
- [使用 "打开方式" 命令显示文件](../../extensibility/internals/displaying-files-by-using-the-open-with-command.md)
- [打开并保存项目项](../../extensibility/internals/opening-and-saving-project-items.md)
- [如何：打开项目特定的编辑器](../../extensibility/how-to-open-project-specific-editors.md)
- [如何：打开标准编辑器](../../extensibility/how-to-open-standard-editors.md)
