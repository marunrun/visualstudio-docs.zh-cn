---
title: 支持多个文档视图 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], custom - multiple document views
ms.assetid: c7ec2366-91c4-477f-908d-e89068bdb3e3
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a952414fa7156d80675564e519e556ccedd524a3
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80699541"
---
# <a name="supporting-multiple-document-views"></a>支持多个文档视图
您可以通过为编辑器创建单独的文档数据和文档视图对象来提供文档的多个视图。 在附加文档视图有用的一些情况下，有以下情况：

- 新的窗口支持：您希望编辑器提供两个或多个相同类型的视图，以便已在编辑器中打开窗口的用户可以通过从 **"窗口"** 菜单中选择 **"新建窗口**"命令打开新窗口。

- 窗体和代码视图支持：您希望编辑器提供不同类型的视图。 [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)]例如，提供窗体视图和代码视图。

  有关此的详细信息，请参阅 Visual Studio 包模板创建的自定义编辑器项目中EditorFactory.cs文件中的 CreateEditorInstance 过程。 有关此项目的详细信息，请参阅[演练：创建自定义编辑器](../extensibility/walkthrough-creating-a-custom-editor.md)。

## <a name="synchronizing-views"></a>同步视图
 实现多个视图时，文档数据对象负责使所有视图与数据保持同步。 您可以使用 事件<xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer>处理接口将多个视图与数据同步。

 如果不使用<xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer>对象同步多个视图，则必须实现自己的事件系统来处理对文档数据对象所做的更改。 您可以使用不同级别的粒度来使多个视图保持最新。 使用最大粒度设置，当您在一个视图中键入时，其他视图将立即更新。 以最小的粒度，其他视图在激活之前不会更新它们。

## <a name="determining-whether-document-data-is-already-open"></a>确定文档数据是否已打开
 集成开发环境 （IDE） 中的正在运行的文档表 （RDT） 可帮助跟踪文档的数据是否已打开，如下图所示。

 ![文档数据视图图形](../extensibility/media/docdataview.gif "文档数据视图")多个视图

 默认情况下，每个视图（文档视图对象）都包含在其自己的窗口框架中 。<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame> 但是，如前所述，文档数据可以显示在多个视图中。 为此，Visual Studio 会检查 RDT 以确定有问题的文档是否已在编辑器中打开。 当 IDE<xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A>调用以创建编辑器时，`punkDocDataExisting`参数中返回的非 NULL 值指示文档已在另一个编辑器中打开。 有关 RDT 如何工作的详细信息，请参阅[运行文档表](../extensibility/internals/running-document-table.md)。

 <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory>在实现中，检查返回的文档数据对象`punkDocDataExisting`，以确定文档数据是否适合编辑器。 （例如，HTML 编辑器只能显示 HTML 数据。如果合适，则编辑器工厂应为数据提供第二个视图。 如果`punkDocDataExisting`参数不是`NULL`，则文档数据对象可能在另一个编辑器中打开，或者文档数据可能已在具有相同编辑器的不同视图中打开。 如果文档数据在编辑器工厂不支持的不同编辑器中打开，则 Visual Studio 无法打开编辑器工厂。 有关详细信息，请参阅[如何：将视图附加到文档数据](../extensibility/how-to-attach-views-to-document-data.md)。
