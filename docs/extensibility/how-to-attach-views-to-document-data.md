---
title: 如何：将视图附加到文档数据 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- editors [Visual Studio SDK], custom - attach views to document data
ms.assetid: f92c0838-45be-42b8-9c55-713e9bb8df07
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: d5437e3a5d4fb0d6d33d570eb4d8923245cb287b
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85905900"
---
# <a name="how-to-attach-views-to-document-data"></a>如何：将视图附加到文档数据
如果有新的文档视图，则可以将其附加到现有的文档数据对象。

## <a name="to-determine-if-you-can-attach-a-view-to-an-existing-document-data-object"></a>确定是否可以将视图附加到现有的文档数据对象

1. 实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A>。

2. 在的实现中 `IVsEditorFactory::CreateEditorInstance` ， `QueryInterface` 当 IDE 调用实现时，对现有文档数据对象调用 `CreateEditorInstance` 。

    通过调用， `QueryInterface` 可以检查在参数中指定的现有文档数据对象 `punkDocDataExisting` 。

    但是，必须查询的确切接口取决于打开文档的编辑器，如步骤4中所述。

3. 如果在现有文档数据对象上找不到相应的接口，则会将错误代码返回到编辑器，指出文档数据对象与编辑器不兼容。

    在 IDE 的实现中 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A> ，消息框通知您文档已在另一个编辑器中打开，并询问您是否要将其关闭。

4. 如果关闭此文档，则 Visual Studio 将再次调用编辑器工厂。 在此调用中， `DocDataExisting` 参数等于 NULL。 然后，您的编辑器工厂实现可以在您自己的编辑器中打开文档数据对象。

   > [!NOTE]
   > 若要确定是否可以使用现有的文档数据对象，还可以通过将指针转换为私有实现的实际类，来使用接口实现的私有知识 [!INCLUDE[vcprvc](../code-quality/includes/vcprvc_md.md)] 。 例如，所有标准编辑器都实现 `IVsPersistFileFormat` ，它们继承自 <xref:Microsoft.VisualStudio.OLE.Interop.IPersist> 。 因此，你可以调用 `QueryInterface` <xref:Microsoft.VisualStudio.OLE.Interop.IPersist.GetClassID%2A> ，如果现有文档数据对象上的类 id 与实现的类 id 匹配，则可以使用文档数据对象。

## <a name="robust-programming"></a>可靠编程
 当 Visual Studio 调用方法的实现时 <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A> ，它会传递回 `punkDocDataExisting` 参数（如果存在）中的现有文档数据对象的指针。 检查中返回的文档数据对象 `punkDocDataExisting` ，以确定文档数据对象是否适用于你的编辑器，如本主题中的过程的步骤4中所述。 如果合适，编辑器工厂应为[支持多文档视图](../extensibility/supporting-multiple-document-views.md)中所述的数据提供另一个视图。 如果不是，则它应显示适当的错误消息。

## <a name="see-also"></a>另请参阅
- [支持多个文档视图](../extensibility/supporting-multiple-document-views.md)
- [自定义编辑器中的文档数据和文档视图](../extensibility/document-data-and-document-view-in-custom-editors.md)
