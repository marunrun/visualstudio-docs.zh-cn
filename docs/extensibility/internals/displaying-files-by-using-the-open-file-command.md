---
title: 使用打开文件命令显示文件 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project types, supporting Open File command
- Open File command
- persistence, supporting Open File command
ms.assetid: 4fff0576-b2f3-4f17-9769-930f926f273c
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 19fda87f0e2692d30b9a99777ca11edd7b3906f0
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66324338"
---
# <a name="display-files-by-using-the-open-file-command"></a>使用打开文件命令显示文件
以下步骤介绍如何处理 IDE**打开的文件**命令，可在找到**文件**菜单中的[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]。 步骤还说明项目应如何响应来自此命令的调用。

 当用户单击**打开的文件**命令**文件**菜单中，并选择从文件**打开的文件**对话框中，将发生以下过程：

1. 使用运行文档表，确定文件是否已在项目中打开 IDE。

    - 如果文件已打开，IDE 将 resurfaces 窗口。

    - 如果文件未打开，IDE 会调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.IsDocumentInProject%2A>来查询每个项目，以确定哪一个项目可以打开该文件。

        > [!NOTE]
        > 中的项目实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.IsDocumentInProject%2A>，提供一个优先级值，指示你的项目将打开该文件的级别。 中提供了优先级值<xref:Microsoft.VisualStudio.Shell.Interop.VSDOCUMENTPRIORITY>枚举。

2. 每个项目与优先级级别，用于指示重要性响应它置于所要打开该文件的项目。

3. IDE 使用以下条件来确定哪一个项目打开的文件：

    - 响应具有最高优先级的项目 (`DP_Intrinsic`) 打开该文件。 如果多个项目使用此优先级进行响应，响应的第一个项目打开的文件。

    - 如果没有项目使用的最高优先级进行响应 (`DP_Intrinsic`)，但具有相同、 低优先级，响应的所有项目活动的项目打开的文件。 如果没有项目处于活动状态，以响应的第一个项目打开的文件。

    - 如果没有项目声明文件的所有权 (`DP_Unsupported`)，杂项文件项目打开的文件。

         如果创建的杂项文件项目实例，则项目始终具有值响应`DP_CanAddAsExternal`。 此值指示该项目可以打开该文件。 使用此项目以容纳打开的文件不在任何其他项目中。 此项目中的项列表不会持久保留;此项目会显示在**解决方案资源管理器**仅当它用于打开文件。

         杂项文件项目并不表示它可以打开该文件，如果尚未创建项目的实例。 在这种情况下，IDE 将创建杂项文件项目的实例并通知项目以打开该文件。

4. 只要 IDE 确定哪一个项目打开的文件，它将调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.OpenItem%2A>在项目的方法。

5. 然后，项目已使用特定于项目的编辑器或标准编辑器打开该文件的选项。 有关详细信息，请参阅[如何：打开项目特定的编辑器](../../extensibility/how-to-open-project-specific-editors.md)和[如何：打开标准编辑器](../../extensibility/how-to-open-standard-editors.md)分别。

## <a name="see-also"></a>请参阅
- [使用打开方式命令显示文件](../../extensibility/internals/displaying-files-by-using-the-open-with-command.md)
- [打开和保存项目项](../../extensibility/internals/opening-and-saving-project-items.md)
- [如何：打开项目特定的编辑器](../../extensibility/how-to-open-project-specific-editors.md)
- [如何：打开标准编辑器](../../extensibility/how-to-open-standard-editors.md)