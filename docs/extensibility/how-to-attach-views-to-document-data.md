---
title: 如何：将视图附加到文档数据 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], custom - attach views to document data
ms.assetid: f92c0838-45be-42b8-9c55-713e9bb8df07
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 1d8bd586a9d67996389f3cb6a2b0f13f0afec3bd
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80711090"
---
# <a name="how-to-attach-views-to-document-data"></a>如何：将视图附加到文档数据
如果您有新的文档视图，则可以将其附加到现有文档数据对象。

## <a name="to-determine-if-you-can-attach-a-view-to-an-existing-document-data-object"></a>确定是否可以将视图附加到现有文档数据对象

1. 实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A>。

2. 在实现 中`IVsEditorFactory::CreateEditorInstance`，当`QueryInterface`IDE 调用您的`CreateEditorInstance`实现时调用现有文档数据对象。

    调用`QueryInterface`使您能够检查现有文档数据对象，该对象在 参数中`punkDocDataExisting`指定。

    但是，您必须查询的确切接口取决于打开文档的编辑器，如步骤 4 中所述。

3. 如果在现有文档数据对象上找不到适当的接口，则向编辑器返回错误代码，指示文档数据对象与编辑器不兼容。

    在 IDE 的 实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A>中，一个消息框会通知您文档在另一个编辑器中处于打开状态，并询问您是否要关闭它。

4. 如果关闭此文档，则 Visual Studio 会第二次调用编辑器工厂。 在此调用中，`DocDataExisting`参数等于 NULL。 然后，编辑器工厂实现可以在您自己的编辑器中打开文档数据对象。

   > [!NOTE]
   > 要确定是否可以使用现有文档数据对象，还可以通过强制将指针强制转换到私有实现的实际[!INCLUDE[vcprvc](../code-quality/includes/vcprvc_md.md)]类来使用接口实现的私有知识。 例如，所有标准编辑器实现`IVsPersistFileFormat`从 继承 。 <xref:Microsoft.VisualStudio.OLE.Interop.IPersist> 因此，您可以调用`QueryInterface` <xref:Microsoft.VisualStudio.OLE.Interop.IPersist.GetClassID%2A>，如果现有文档数据对象的类 ID 与实现的类 ID 匹配，则可以使用文档数据对象。

## <a name="robust-programming"></a>可靠编程
 当 Visual Studio 调用方法<xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A>的实现时，它会传递指向`punkDocDataExisting`参数中现有文档数据对象的指针（如果存在）。 检查返回`punkDocDataExisting`的文档数据对象，以确定文档数据对象是否适合您的编辑器，本主题中的步骤 4 中的注释中所述。 如果合适，则编辑器工厂应提供[支持多个文档视图](../extensibility/supporting-multiple-document-views.md)中概述的数据的第二个视图。 如果没有，则它应该显示相应的错误消息。

## <a name="see-also"></a>请参阅
- [支持多个文档视图](../extensibility/supporting-multiple-document-views.md)
- [自定义编辑器中的文档数据和文档视图](../extensibility/document-data-and-document-view-in-custom-editors.md)
