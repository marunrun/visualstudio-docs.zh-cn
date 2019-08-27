---
title: 如何：附加文档数据的视图 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], custom - attach views to document data
ms.assetid: f92c0838-45be-42b8-9c55-713e9bb8df07
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c42ccdb817ab4a7594922e90e9df3e345c693c11
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66340996"
---
# <a name="how-to-attach-views-to-document-data"></a>如何：将视图附加到文档数据
如果您有一个新的文档视图，您可能能够将其附加到现有的文档数据对象。

## <a name="to-determine-if-you-can-attach-a-view-to-an-existing-document-data-object"></a>若要确定是否可以将视图附加到现有的文档数据对象

1. 实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A>。

2. 中的实现`IVsEditorFactory::CreateEditorInstance`，调用`QueryInterface`现有文档的数据对象时 IDE 调用你`CreateEditorInstance`实现。

    调用`QueryInterface`，可以检查现有的文档数据对象，它指定在`punkDocDataExisting`参数。

    确切的接口必须查询，但是，取决于正在打开文档，编辑器在步骤 4 中所述。

3. 如果找不到现有的文档数据对象上的相应接口，然后返回到你，该值指示文档数据对象与您的编辑器不兼容的编辑器的错误代码。

    在 IDE 的实现中的<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A>，一个消息框会通知你，文档在另一个编辑器中打开，并询问您是否将其关闭。

4. 如果关闭此文档，然后 Visual Studio 调用编辑器工厂的第二次。 在此调用时，`DocDataExisting`参数等于 NULL。 编辑器工厂实现然后可以在自己的编辑器中打开文档数据对象。

   > [!NOTE]
   > 若要确定是否可以使用现有的文档数据对象，您还可以使用专用接口实现的知识通过强制转换为实际的指针[!INCLUDE[vcprvc](../code-quality/includes/vcprvc_md.md)]私有实现的类。 例如，所有的标准编辑器实现`IVsPersistFileFormat`，后者又继承<xref:Microsoft.VisualStudio.OLE.Interop.IPersist>。 因此，可以调用`QueryInterface`为<xref:Microsoft.VisualStudio.OLE.Interop.IPersist.GetClassID%2A>，并在现有的文档数据对象的类 ID 是否匹配你的实现的类 ID，然后可以使用文档数据对象。

## <a name="robust-programming"></a>可靠编程
 当 Visual Studio 调用的实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A>方法，它返回将指针传递到现有的文档数据对象中`punkDocDataExisting`参数，如果存在。 检查文档数据对象中返回`punkDocDataExisting`来确定文档数据对象是否适合于您的编辑器中的此主题中的过程步骤 4 中的说明所述。 如果合适，则编辑器工厂应提供第二个视图的数据中所述[支持多个文档视图](../extensibility/supporting-multiple-document-views.md)。 如果没有，则它应显示相应的错误消息。

## <a name="see-also"></a>请参阅
- [支持多个文档视图](../extensibility/supporting-multiple-document-views.md)
- [文档数据和自定义编辑器中的文档视图](../extensibility/document-data-and-document-view-in-custom-editors.md)