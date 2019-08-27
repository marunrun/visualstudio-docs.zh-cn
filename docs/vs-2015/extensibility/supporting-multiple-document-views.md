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
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68160522"
---
# <a name="supporting-multiple-document-views"></a>支持多个文档视图
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

通过为您的编辑器创建单独的文档数据和文档视图对象，可以提供多个文档的视图。 一些额外的文档视图会非常有用的情况是：  
  
- 新的窗口支持：您希望您的编辑器提供的相同类型的两个或多个视图，以便已在编辑器中打开一个窗口的用户可以通过选择打开一个新的窗口**新的窗口**命令**窗口**菜单。  
  
- 窗体和代码视图支持：希望您编辑器来提供不同类型的视图。 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)]例如，提供窗体视图和代码视图。  
  
  有关此的详细信息，请参阅由 Visual Studio 包模板创建的自定义编辑器项目中的 EditorFactory.cs 文件中的 CreateEditorInstance 过程。 有关此项目的详细信息，请参阅[演练：创建自定义编辑器](../extensibility/walkthrough-creating-a-custom-editor.md)。  
  
## <a name="synchronizing-views"></a>同步视图  
 当实现多个视图时，文档数据对象负责保持与数据同步的所有视图。 可以使用的事件处理接口上<xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer>以多个视图的数据同步的。  
  
 如果不使用<xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer>对象来同步多个视图，然后，必须实现你自己的事件系统来处理对文档数据对象所做的更改。 可以使用不同的粒度级别以保持多个视图最新。 使用的最大粒度设置，如在一个视图中键入其他视图是立即更新。 最小粒度，与其他视图不会更新直到它们被激活。  
  
## <a name="determining-whether-document-data-is-already-open"></a>确定是否文档数据是已打开  
 在集成的开发环境 (IDE) 中正在运行文档表 (RDT) 可帮助跟踪文档的数据是已打开，如以下关系图中所示。  
  
 ![DocDataView 图](../extensibility/media/docdataview.gif "Docdataview")  
多视图  
  
 默认情况下，每个视图 （文档视图对象） 包含在其自己的窗口框架 (<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame>)。 如先前所述，但是，文档数据可以显示多个视图中。 若要启用此功能，Visual Studio，请检查 RDT 以确定有问题的文档是否已在编辑器中打开。 当调用 IDE<xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A>若要创建编辑器中中, 非 NULL 值返回`punkDocDataExisting`参数指示文档已在另一个编辑器中打开。 有关详细了解如何 RDT 函数，请参阅[运行文档表](../extensibility/internals/running-document-table.md)。  
  
 在你<xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory>实现中，检查文档数据对象中返回`punkDocDataExisting`以确定是否适合你的编辑器的文档数据。 （例如，仅 HTML 数据应显示 HTML 编辑器。）如果适用，编辑器工厂应为数据提供第二个视图。 如果`punkDocDataExisting`参数不是`NULL`，很可能也文档数据对象是在另一个编辑器中打开，或者可在更有可能，文档数据已在具有相同编辑器中的不同视图中打开。 如果编辑器工厂不支持的其他编辑器中打开的文档数据时，Visual Studio 无法打开编辑器工厂。 有关详细信息，请参阅[如何：将视图文档数据附加](../extensibility/how-to-attach-views-to-document-data.md)。
