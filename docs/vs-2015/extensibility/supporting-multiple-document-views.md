---
title: 支持多个文档视图 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], custom - multiple document views
ms.assetid: c7ec2366-91c4-477f-908d-e89068bdb3e3
caps.latest.revision: 26
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 9377fc12db8cedba65a418fd32b82a1421bd9b43
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68160522"
---
# <a name="supporting-multiple-document-views"></a>支持多个文档视图
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可以通过为编辑器创建单独的文档数据和文档视图对象来提供文档的多个视图。 在某些情况下，其他文档视图会很有用：  
  
- 新窗口支持：你希望编辑器提供同一类型的两个或多个视图，以便在编辑器中打开一个窗口的用户可以通过在 "**窗口**" 菜单中选择 "**新建窗口**" 命令来打开一个新窗口。  
  
- 窗体和代码视图支持：希望编辑器提供不同类型的视图。 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)]例如，同时提供了窗体视图和代码视图。  
  
  有关此操作的详细信息，请参阅 Visual Studio 包模板创建的自定义编辑器项目中的 EditorFactory.cs 文件中的 CreateEditorInstance 过程。 有关此项目的详细信息，请参阅 [演练：创建自定义编辑器](../extensibility/walkthrough-creating-a-custom-editor.md)。  
  
## <a name="synchronizing-views"></a>同步视图  
 当您实现多个视图时，文档数据对象负责保持所有视图都与数据同步。 您可以使用中的事件处理接口 <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer> ，将多个视图与数据同步。  
  
 如果不使用 <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer> 对象来同步多个视图，则必须实现自己的事件系统以处理对文档数据对象所做的更改。 可以使用不同的粒度级别，使多个视图保持最新。 设置为最大粒度后，当你在一个视图中键入时，将立即更新其他视图。 对于最小粒度，其他视图在激活之前不会更新。  
  
## <a name="determining-whether-document-data-is-already-open"></a>确定文档数据是否已打开  
 正在运行的文档表在集成开发环境 (IDE) 中 (RDT) ，有助于跟踪文档的数据是否已打开，如下图所示。  
  
 ![DocDataView 图](../extensibility/media/docdataview.gif "Docdataview")  
多视图  
  
 默认情况下，每个视图 (文档视图对象) 包含在其自己的窗口框架 (<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame>) 中。 但正如前文所述，文档数据可以显示在多个视图中。 若要启用此项，Visual Studio 将检查 RDT 以确定是否已在编辑器中打开了相关文档。 当 IDE 调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A> 创建编辑器时，在参数中返回的非 NULL 值 `punkDocDataExisting` 表示文档已在另一个编辑器中打开。 有关 RDT 函数的详细信息，请参阅 [运行文档表](../extensibility/internals/running-document-table.md)。  
  
 在您的 <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory> 实现中，检查中返回的文档数据对象， `punkDocDataExisting` 以确定文档数据是否适合您的编辑器。  (例如，HTML 编辑器应该只显示 HTML 数据。 ) 如果适用，则编辑器工厂应提供数据的另一个视图。 如果 `punkDocDataExisting` 参数不为 `NULL` ，则可能是在另一个编辑器中打开了文档数据对象，或者，如果文档数据已在具有相同编辑器的不同视图中打开，则可能是如此。 如果文档数据在编辑器工厂不支持的其他编辑器中打开，则 Visual Studio 将无法打开编辑器工厂。 有关详细信息，请参阅 [如何：将视图附加到文档数据](../extensibility/how-to-attach-views-to-document-data.md)。
